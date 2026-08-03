# NS-ARDM

Procedures for **NS-ARDM** Proxmox jumpboxes (desktop PCs running Proxmox VE with Windows, Linux, and AREDN VMs).

**Platform assumed:** Proxmox Virtual Environment **9.2.x** (Debian Trixie-based).

## Documents

| File | Purpose |
|------|---------|
| [`01-Connect-to-Jumpbox.md`](01-Connect-to-Jumpbox.md) | Reach the Proxmox UI and open guest VMs |
| [`02-Update-Proxmox-No-Subscription.md`](02-Update-Proxmox-No-Subscription.md) | Enable free update repos and apply updates |
| [`03-Proper-Shutdown.md`](03-Proper-Shutdown.md) | Shut down guest VMs, then the jumpbox |
| [`04-Create-AREDN-x86-VM.md`](04-Create-AREDN-x86-VM.md) | Create a new AREDN node VM from x86_64 image |
| [`05-Update-AREDN-VM.md`](05-Update-AREDN-VM.md) | Upgrade firmware on an existing AREDN VM |
| [`06-Install-Raven.md`](06-Install-Raven.md) | Install Raven chat on a primary AREDN node |

## Terms used in these docs

| Term | Meaning |
|------|---------|
| **Jumpbox** | The physical computer running Proxmox VE |
| **Guest / VM** | A virtual machine on that jumpbox (Windows, Linux, AREDN, etc.) |
| **Node** | An AREDN mesh router (hardware or x86 VM) |
| **Proxmox UI** | Web admin at `https://JUMPBOX-IP:8006` |
