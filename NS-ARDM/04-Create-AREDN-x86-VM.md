# Create a New AREDN Node VM (x86_64) on Proxmox

**Applies to:** Proxmox VE **9.2.x** jumpboxes  
**Goal:** Create a new AREDN virtual node from the official **x86_64** disk image.

This is **not** a Mikrotik router image. Mikrotik hardware and x86 VMs both run AREDN, but you must download the **x86/64** files.

Official overview: [AREDN Virtual Machine Installs](https://docs.arednmesh.org/en/latest/arednHow-toGuides/vm-install.html)

---

## What you need

- Access to the Proxmox UI (`https://JUMPBOX-IP:8006`) — see `01-Connect-to-Jumpbox.md`
- Ability to open the node **Shell** as `root`
- Internet on the jumpbox (to download the image), **or** a way to copy the `.img` onto the jumpbox
- A free VM ID (example below uses `120` — pick an unused number)
- A plan for networking (bridge names, how many NICs). **Easiest:** open an existing working AREDN VM → **Hardware** and copy its NIC count and bridges

### Minimum resources (AREDN docs)

| Resource | Minimum | Practical starting point |
|----------|---------|---------------------------|
| vCPU | 2 | 2 |
| RAM | 64 MB | **256–512 MB** |
| Disk | 128 MB | Image size grows after import — use the imported disk as-is (often ~300 MB+); enlarge later only if needed |

---

## Part A — Choose the correct image

1. Open the AREDN downloads site: [https://downloads.arednmesh.org/](https://downloads.arednmesh.org/)  
2. Prefer a **stable release** under `releases/…/targets/x86/64/` unless your mesh group standardizes on nightlies.  
   Example release folder style:  
   `https://downloads.arednmesh.org/releases/4/26/4.26.7.0/targets/x86/64/`  
3. Download **one** of these (names include the version):

| File | Use when |
|------|----------|
| `…-x86-64-generic-ext4-combined-efi.img.gz` | Proxmox VM BIOS = **OVMF (UEFI)** — **recommended for new VMs** |
| `…-x86-64-generic-ext4-combined.img.gz` | Proxmox VM BIOS = **SeaBIOS** (legacy) |

4. Do **not** download Mikrotik / ath79 / ipq files for a Proxmox VM.

**Tip:** Match an existing AREDN VM: select it → **Hardware** / **Options** → note whether **BIOS** is OVMF or SeaBIOS, then pick the matching image type.

---

## Part B — Put the image on the jumpbox

### Option 1 — Download on the jumpbox (Shell)

1. Proxmox UI → select the **node** → **Shell**.  
2. Create a work folder and download (adjust the URL to the exact file you chose):

```bash
mkdir -p /var/lib/vz/template/iso
cd /var/lib/vz/template/iso
wget -O aredn-x86.img.gz 'https://downloads.arednmesh.org/releases/4/26/4.26.7.0/targets/x86/64/aredn-4.26.7.0-x86-64-generic-ext4-combined-efi.img.gz'
```

3. Decompress:

```bash
gunzip -k aredn-x86.img.gz
# or, if -k unsupported:
# gunzip -c aredn-x86.img.gz > aredn-x86.img
ls -lh aredn-x86.img
```

You need a raw `.img` file for the import step.

### Option 2 — Download on your PC, then upload

1. Download the `.img.gz` on your PC.  
2. Extract to `.img` (on Windows, 7-Zip sometimes mishandles `.gz` — use another gzip tool or extract on Linux if needed).  
3. Copy `aredn-x86.img` to the jumpbox, for example with `scp`, WinSCP, or Proxmox storage upload into a place you can reach from Shell (e.g. `/var/lib/vz/template/iso/`).

---

## Part C — Create the VM shell and import the disk

In the Proxmox **Shell**, set variables (change IDs/names/storage to match your jumpbox):

```bash
VMID=120
VMNAME=aredn-new
STORAGE=local-lvm
BRIDGE=vmbr0
IMG=/var/lib/vz/template/iso/aredn-x86.img
```

Check unused ID and storage names:

```bash
qm list
pvesm status
```

### C1 — Create an empty VM (UEFI / EFI image — recommended)

```bash
qm create $VMID \
  --name "$VMNAME" \
  --machine q35 \
  --bios ovmf \
  --cpu host \
  --cores 2 \
  --memory 512 \
  --scsihw virtio-scsi-pci \
  --net0 virtio,bridge=$BRIDGE \
  --agent enabled=1
```

Add EFI vars disk (required for OVMF):

```bash
qm set $VMID --efidisk0 ${STORAGE}:1,efitype=4m,pre-enrolled-keys=0
```

### C2 — Create an empty VM (SeaBIOS / non-EFI image)

Only if you downloaded the **non-efi** `combined.img.gz`:

```bash
qm create $VMID \
  --name "$VMNAME" \
  --machine q35 \
  --bios seabios \
  --cpu host \
  --cores 2 \
  --memory 512 \
  --scsihw virtio-scsi-pci \
  --net0 virtio,bridge=$BRIDGE \
  --agent enabled=1
```

### C3 — Import the AREDN disk image

```bash
qm importdisk $VMID "$IMG" $STORAGE
```

Proxmox prints the new disk name (often `vm-<ID>-disk-1` or similar). Attach it as SCSI and set boot order:

```bash
# Adjust disk name if importdisk printed something different
qm set $VMID --scsi0 ${STORAGE}:vm-${VMID}-disk-1
qm set $VMID --boot order=scsi0
```

If `vm-${VMID}-disk-1` fails, list disks:

```bash
qm config $VMID
```

Use the unused disk reference shown (e.g. `unused0: local-lvm:vm-120-disk-0`) and set:

```bash
qm set $VMID --scsi0 local-lvm:vm-120-disk-0
qm set $VMID --boot order=scsi0
```

(Replace storage/disk names with yours.)

### C4 — Extra network ports (optional)

AREDN starts in **single-port** mode even if you add NICs; you can reassign WAN / DtD / LAN later in the AREDN UI.

To copy a multi-NIC layout from an existing node, add more nets (example):

```bash
qm set $VMID --net1 virtio,bridge=vmbr0
qm set $VMID --net2 virtio,bridge=vmbr0
```

Use the **same bridges** as your working AREDN VMs. Wrong bridges = no mesh / no LAN access.

---

## Part D — First boot and basic AREDN setup

1. In the Proxmox UI, select the new VM → **Start**.  
2. Open **Console**.  
3. Wait for boot. You may see BusyBox / AREDN messages (similar to your other nodes).  
4. From a PC on the LAN that can reach the node:
   - Try the first-boot / default access method your group uses (often a link-local or LAN DHCP address shown in Console, or temporary `192.168.1.1` style access depending on image/mode).  
   - Or use Console-only until networking is understood.  
5. Complete first-time AREDN setup in the web UI:
   - Node name / callsign conventions for your mesh  
   - Password  
   - WAN / LAN / DtD as required  
   - Save / reboot when prompted  

Exact first-login URL depends on your NIC bridging. If the web UI is unreachable, compare **Hardware → Network** with a working AREDN VM and fix bridges first.

---

## Part E — Record what you built

Write down for later upgrades (`05-Update-AREDN-VM.md`):

| Item | Your value |
|------|------------|
| VMID / name | |
| BIOS (OVMF vs SeaBIOS) | |
| Image file used (`combined-efi` vs `combined`) | |
| AREDN version after setup | |
| Bridges / NIC count | |
| How you reach Admin UI | |

---

## Troubleshooting

| Problem | What to try |
|---------|-------------|
| UEFI shell / no boot | Wrong image for BIOS, or boot order not `scsi0`, or missing `efidisk0`. |
| Boots then no network | Bridge name wrong; compare with a working AREDN VM. |
| `importdisk` fails | Path to `.img` wrong; storage name wrong (`pvesm status`). |
| Out of memory | Raise RAM to 512 MB. |
| Created Mikrotik image by mistake | Delete VM disk and redo with **x86/64** combined image. |

---

## Related

- Connect / Console: `01-Connect-to-Jumpbox.md`  
- Shutdown AREDN (`HALT` then Stop): `03-Proper-Shutdown.md`  
- Upgrade firmware later: `05-Update-AREDN-VM.md`
