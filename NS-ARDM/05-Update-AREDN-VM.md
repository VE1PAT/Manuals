# Update an Existing AREDN Node VM

**Applies to:** AREDN **x86_64** guest VMs on Proxmox VE 9.2.x  
**Goal:** Move an existing virtual AREDN node to a newer firmware safely.

Updating Proxmox (`02-Update-Proxmox-No-Subscription.md`) does **not** update AREDN.  
Each AREDN VM must be updated on its own.

---

## Know what you are running

### Example currently seen on console

On at least one jumpbox AREDN VM, the Proxmox Console has shown:

```text
BusyBox v1.37.0 (2026-05-13 22:42:09 UTC) built-in shell
20260528-efcb8c4b, r32933-4ccb782af7
```

How to read that:

| Piece | Meaning |
|-------|---------|
| `BusyBox v1.37.0 …` | Embedded shell/toolkit build inside the image |
| `20260528-efcb8c4b` | **Snapshot-style** AREDN build id: date `2026-05-28` + git hash `efcb8c4b` |
| `r32933-…` | OpenWrt revision string baked into that build |

That is **not** the same naming as a stable release such as `4.26.7.0`. Snapshot/nightly nodes are normal, but your mesh group should agree whether you stay on nightlies or move to a stable **release**.

### Confirm before every upgrade

1. Proxmox → select the AREDN VM → **Console** (restart the VM if you need a clean boot banner).  
2. Note any version / build lines.  
3. Prefer also opening **Node Admin** in a browser and reading the firmware / version display (clearest source).  
4. Proxmox → VM → **Options** (or Hardware): note **BIOS** = **OVMF (UEFI)** or **SeaBIOS**.

You need BIOS type so you download the matching x86 image family.

---

## Before you update (checklist)

```
[ ] Mesh group OK with this upgrade (and release vs nightly choice)
[ ] You can reach this node’s Admin UI again after reboot (know the IP / name)
[ ] Note current version / build string
[ ] Note BIOS: OVMF (UEFI) vs SeaBIOS
[ ] Proxmox backup or snapshot of this VM (strongly recommended)
[ ] Update ONE VM first; prove it; then the others
```

### Optional Proxmox snapshot

1. Select the AREDN VM (can be running).  
2. **Snapshot** → create named snapshot (e.g. `before-fw-2026-08-01`).  
3. If the upgrade bricks the guest, restore that snapshot.

---

## Part A — Download the correct upgrade file

1. Go to [https://downloads.arednmesh.org/](https://downloads.arednmesh.org/).  
2. Open **x86 / 64** for the version you want:
   - **Stable:** `releases/…/targets/x86/64/`  
   - **Nightly/snapshot:** `snapshots/targets/x86/64/`  
3. Download the file that matches this VM’s BIOS:

| BIOS in Proxmox | Download |
|-----------------|----------|
| **OVMF (UEFI)** | `…-x86-64-generic-ext4-combined-efi.img.gz` (or the sysupgrade/package your Admin page expects — see note below) |
| **SeaBIOS** | `…-x86-64-generic-ext4-combined.img.gz` |

4. Keep the `.gz` or extract only if the upload form requires a raw file — follow what the node’s Firmware page accepts (many accept the compressed image or a specific sysupgrade artifact listed for that release).

**Important:** Do **not** use Mikrotik `sysupgrade.bin` / `rb.elf` files on an x86 VM.

### About the built-in “download for me” updater

On some **UEFI** x86 VMs, AREDN’s automatic updater has been reported to fetch the **wrong** (non-EFI) image and break boot.  

**Recommended habit for these jumpboxes:** download the image yourself on a PC, then **upload** it on the Firmware page (Part B), instead of trusting one-click remote fetch.

---

## Part B — Apply the update from Node Admin

1. Connect to the node Admin UI (browser to the guest IP / mesh name, or via your Windows jump VM — see `01-Connect-to-Jumpbox.md`).  
2. Open **Administration** / **Setup** → **Firmware** (label varies slightly by version).  
3. Use **Upload** / browse to the file you downloaded.  
4. Confirm the UI shows the file and that you are updating **this** node.  
5. Start the update (**Update** / **Upload & Reboot** — use the button the page provides).  
6. **Do not** power off the VM mid-flash.  
7. Wait for reboot. Console may disconnect; that is normal.  
8. When it is back:
   - Confirm version/build changed  
   - Confirm node name / services still look right  
   - Confirm mesh / WAN / LAN as applicable  

### If the web UI is awkward

AREDN documents a **sideload** path (copy firmware to a fixed path on the node, then press Update). See official [Firmware tips](https://docs.arednmesh.org/en/latest/arednHow-toGuides/firmware_tips.html).

If using the node shell, do **not** use legacy OpenWrt `sysupgrade` alone. AREDN requires:

```text
/usr/local/bin/aredn_sysupgrade
```

Only use that if you know the local image path and your group’s procedure — prefer the web Firmware upload when possible.

---

## Part C — After a successful update

1. Remove or keep the Proxmox snapshot per your comfort (keep until the node is proven for a day or two).  
2. Record the new version string next to the VM name.  
3. Only then upgrade the **second** and **third** AREDN VMs the same way (same BIOS → same image family).

---

## Part D — If it will not boot after upgrade

1. Proxmox → select VM → **Snapshots** → restore the pre-upgrade snapshot.  
2. Or restore from backup.  
3. Retry with the **other** image family only if you discover BIOS and file were mismatched (EFI vs non-EFI).  
4. Avoid random “try every file” on a live mesh node without a snapshot.

---

## Quick reference

| Do | Don’t |
|----|-------|
| Match **x86/64** image to **UEFI vs SeaBIOS** | Flash Mikrotik firmware onto the VM |
| Snapshot before upgrade | Rely blindly on auto-fetch on UEFI VMs |
| Update one VM, then the others | Update Proxmox and assume AREDN changed |
| Use AREDN Firmware upload / `aredn_sysupgrade` | Use plain OpenWrt `sysupgrade` |

---

## Related

- Create a new VM from scratch: `04-Create-AREDN-x86-VM.md`  
- Connect to UI / Console: `01-Connect-to-Jumpbox.md`  
- Clean halt before host shutdown: `03-Proper-Shutdown.md` (`HALT`, then Stop)
