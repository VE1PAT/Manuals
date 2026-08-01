# Connect to Your Proxmox Jumpbox and VMs

**Applies to:** Proxmox VE 9.2.x jumpboxes on a home/site LAN  
**Goal:** Open the Proxmox admin UI, start VMs, and use those VMs (console, RDP, SSH, or AREDN web UI).

## Terms

| Term | Meaning |
|------|---------|
| **Jumpbox** | The **physical** computer running Proxmox |
| **Guest / VM** | A virtual machine on that jumpbox (Windows, Linux, AREDN, …) |
| **Jumpbox IP** | LAN address of the **physical** Proxmox host (not a guest) |
| **Guest IP** | LAN address of a **VM** (each VM usually has its own) |

---

## Step 1 — Find the jumpbox IP

The Proxmox admin page is on the **physical** machine.

1. Log into your **home/site router** admin page.  
2. Open the **DHCP client / lease** list (names vary by router).  
3. Find the jumpbox computer (hostname may look like `pve`, `proxmox`, or the PC name you set at install).  
4. Note its IPv4 address, for example `192.168.1.50`.  
   That is **JUMPBOX-IP**.

**Other ways (if you already know them):** sticker/sheet next to the PC, previous bookmark, or ask whoever installed it.

You must be on a network that can reach that IP (usually the same LAN / VPN).

---

## Step 2 — Open the Proxmox admin console

1. On your laptop/PC, open a browser.  
2. Go to:

```text
https://JUMPBOX-IP:8006
```

Example: `https://192.168.1.50:8006`

3. If the browser warns about the certificate, choose **Advanced** → proceed / accept (Proxmox uses a self-signed certificate by default).  
4. Log in:
   - **User:** `root` (unless you were given another admin)  
   - **Password:** the Proxmox root password  
   - **Realm:** `Linux PAM` (typical)

You should see the Proxmox tree: **Datacenter** → **node (jumpbox)** → VMs.

---

## Step 3 — Start the VMs you need

1. In the left tree, select a VM that shows **stopped**.  
2. Click **Start**.  
3. Wait until it shows **running** (green indicator).  
4. Repeat for each VM you need (Windows, Linux, AREDN, …).

Some VMs may be set to start automatically when the jumpbox boots. Still verify they are running.

---

## Step 4 — Connect into a guest VM

Pick the method that matches how you use that guest.

### Method A — Proxmox Console (works even if you do not know the guest IP)

Best first step for everyone.

1. Select the VM.  
2. Click **Console**.  
3. Use the on-screen keyboard/mouse to log into Windows, Linux, or the AREDN UI.  
4. If the console is blank, click inside it, or try **Send Ctrl+Alt+Del** from the console menu (Windows).

This does **not** require knowing the guest’s IP address.

### Method B — Windows guest via Remote Desktop (RDP)

1. Start the Windows VM; open **Console** once and confirm you can log in.  
2. Find the **guest IP** (Step 5).  
3. On your laptop, open **Remote Desktop Connection** (`mstsc`).  
4. Connect to the **guest IP** (not the jumpbox IP, unless they happen to be the same — they usually are not).  
5. Log in with the Windows username/password for that VM.

Windows must allow Remote Desktop (enabled in Windows settings) and the network profile must allow it.

### Method C — Linux guest via SSH

1. Start the Linux VM.  
2. Find the **guest IP** (Step 5).  
3. From your laptop:

```bash
ssh USER@GUEST-IP
```

### Method D — AREDN node web UI

1. Start the AREDN VM.  
2. Find the **AREDN guest IP** (Step 5) — or use Console.  
3. In a browser (from a PC that can reach that IP), open `http://GUEST-IP/` (or the address your AREDN build uses).  
4. For halt/shutdown later, see `03-Proper-Shutdown.md`.

---

## Step 5 — Find guest VM IP addresses (correct ways)

**Important:** The **Default Route / Gateway** in a VM’s network details is usually your **router**, **not** the list of VM addresses. Do **not** paste the default route into a browser expecting to reach other VMs.

Use one of these instead:

### Way 1 — Proxmox Summary (easiest when it works)

1. Select the VM.  
2. Open **Summary**.  
3. Look for **IPs** / network information.  
4. This appears when **QEMU Guest Agent** is installed and running inside that VM. If blank, use Way 2 or 3.

### Way 2 — Inside the guest (always works via Console)

**Windows VM**

1. Console into the VM and log in.  
2. Right-click the network icon (system tray) → **Open Network & Internet settings**  
   - or run `cmd` and type `ipconfig`  
3. Find the Ethernet/vEthernet adapter’s **IPv4 Address** (for example `192.168.1.80`).  
4. That is this VM’s guest IP.

**Linux VM**

```bash
ip -4 addr
```

or

```bash
hostname -I
```

**AREDN**

Use the node’s status/LAN display in its UI, or check the address shown after login in Console.

### Way 3 — Router DHCP leases

1. Open the router DHCP list again.  
2. Find hostnames for each VM (if they announce names).  
3. Note each lease IP.

---

## Step 6 — Typical “work from a Windows jump VM” pattern (optional)

Some setups include a **Windows desktop VM** used as a daily workstation. Flow:

1. Connect to Proxmox (Steps 1–2).  
2. Start the Windows workstation VM and any other VMs you need (Step 3).  
3. Open that Windows VM with **Console** or **RDP** (Step 4).  
4. From **inside** that Windows VM, use a browser or RDP/SSH to other guests **using each guest’s own IP** from Step 5 — not the default gateway.

Example: AREDN at `192.168.1.90` → in the Windows VM browser open `http://192.168.1.90/`.

---

## Quick map

```
Your laptop
    → https://JUMPBOX-IP:8006   (Proxmox UI on the physical PC)
        → Start VMs
        → Console / RDP / SSH / http to each GUEST-IP
```

| You want… | Use |
|-----------|-----|
| Admin Proxmox, start/stop VMs | `https://JUMPBOX-IP:8006` |
| See a VM desktop without knowing IP | VM → **Console** |
| Remote Desktop to Windows VM | RDP to **guest IP** |
| Shell on Linux VM | SSH to **guest IP** |
| AREDN web pages | Browser to **AREDN guest IP** (or Console) |

---

## Troubleshooting

| Problem | What to try |
|---------|-------------|
| Browser cannot open `:8006` | Wrong IP; not on same network/VPN; jumpbox powered off; try ping JUMPBOX-IP. |
| Certificate warning | Expected — proceed once you trust you typed the right IP. |
| Login fails | Caps Lock; wrong realm; reset is an advanced host procedure. |
| Console black | Click the console pane; send Ctrl+Alt+Del; confirm VM is **running**. |
| RDP fails | Guest firewall/RDP off; wrong IP (used jumpbox IP by mistake); VM not started. |
| “Default route” IP does nothing useful in browser | That is usually the **router**. Use the guest’s own IPv4 instead. |
| Summary shows no IP | Install/enable QEMU Guest Agent later, or use `ipconfig` / `ip addr` in Console. |
