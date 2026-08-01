# Proper Shutdown (VMs First, Then Jumpbox)

**Applies to:** Proxmox VE 9.2.x jumpboxes with Windows, Linux, and AREDN guests  
**Goal:** Shut everything down cleanly so disks are not left half-written.

**Order always:**

1. Shut down / stop **every guest VM**  
2. Confirm none show a green “running” indicator  
3. Shut down the **Proxmox jumpbox** (the physical PC)

Never power off the wall outlet or hold the PC power button while VMs are still running, unless you have no other choice.

---

## Part A — Open the Proxmox UI

1. Browser → `https://JUMPBOX-IP:8006`  
2. Log in as `root` (or your admin account).  
3. In the left tree you will see the **node** (jumpbox) and under it each **VM** / container.

A **green** play-style indicator next to a VM usually means it is still running. After a proper stop, that goes away (VM shows stopped).

---

## Part B — Shut down each guest VM

Work through **all** running VMs one by one. Use the section that matches the guest type.

### B1 — AREDN node VM

AREDN guests are special: use **HALT** inside the node first, then force Stop in Proxmox if needed.

1. Select the AREDN VM in the left tree.  
2. Open **Console** (noVNC).  
3. Get to a command / shell window on the AREDN node (as you normally administer it).  
4. Type:

```text
HALT
```

5. Press Enter.  
6. Wait until the console goes to a **black / idle** screen (node has halted).  
7. Back in the Proxmox UI (still on that VM): open the **Shutdown** control  
   - Click the **down-arrow** on the Shutdown button (not only the main Shutdown if your UI splits actions).  
   - Choose **Stop**.  
   - Confirm **Yes**.  
8. Wait until the VM no longer shows as running (no green running indicator).

If Console was already dead but the VM still shows running, use **Stop** as in step 7.

### B2 — Windows 10 / Windows 11 VM

Prefer a normal Windows shutdown so disks stay clean.

**Option 1 — From inside Windows (best)**

1. Select the Windows VM → **Console**.  
2. Sign in if needed.  
3. Start menu → **Power** → **Shut down**.  
4. Wait until the Proxmox status shows the VM **stopped** (console will go black / disconnect).

**Option 2 — From Proxmox ACPI Shutdown**

1. Select the Windows VM.  
2. Click **Shutdown** (graceful ACPI request — like pressing the power button on a PC).  
3. Wait up to a few minutes for Windows to finish.  
4. If it **never** stops: use Shutdown **down-arrow** → **Stop** → **Yes** (hard stop — last resort).

Do **not** use **Stop** first unless Windows is frozen.

### B3 — Linux VM (Ubuntu, Debian, etc.)

**Option 1 — From inside Linux (best)**

1. Select the Linux VM → **Console** (or SSH if you already use it).  
2. Log in.  
3. Run:

```bash
sudo shutdown -h now
```

(or `sudo poweroff`)

4. Wait until Proxmox shows the VM **stopped**.

**Option 2 — From Proxmox**

1. Select the VM → **Shutdown** (ACPI).  
2. Wait for stopped status.  
3. If stuck: Shutdown down-arrow → **Stop** → **Yes**.

### B4 — Any other guest

1. Try a normal OS shutdown from **Console** first.  
2. If unknown/frozen: Proxmox **Shutdown**, wait, then **Stop** if required.

---

## Part C — Confirm all guests are stopped

1. Look at every VM under the node.  
2. None should show a green running indicator.  
3. Status should be **stopped** (wording may vary).

If **any** VM is still running, go back to Part B for that VM.

---

## Part D — Shut down the Proxmox jumpbox

Only after **all** VMs are stopped:

1. Select the **node** (the jumpbox itself) in the left tree — not a VM.  
2. Click **Shutdown**.  
3. Confirm **Yes**.  
4. Wait for the physical PC to power off (fans stop, lights off as usual for that machine).  
5. You may then switch off a power bar / UPS output if that is part of your site procedure.

### If the Web UI is unreachable

At the physical keyboard on the jumpbox (or via SSH to the host as root), after guests are stopped:

```bash
shutdown -h now
```

---

## Quick checklist

```
[ ] Proxmox UI open
[ ] AREDN: HALT → black screen → Stop (if still running)
[ ] Each Windows VM: Shut down from Start menu (or ACPI Shutdown)
[ ] Each Linux VM: shutdown -h now (or ACPI Shutdown)
[ ] No VM shows green / running
[ ] Node → Shutdown
[ ] Physical PC is off
```

---

## Troubleshooting

| Problem | What to try |
|---------|-------------|
| Shutdown sits forever | Wait 2–3 minutes; then **Stop**. Next time, shut down from inside the guest OS. |
| Clicked Stop by mistake while OS was busy | Next boot may run disk check — usually OK; avoid as habit. |
| Shut down the node while a VM was green | Avoid; if it happened, on next boot check each VM. |
| AREDN HALT does nothing | Check you are in the AREDN command UI; then use Proxmox **Stop**. |
| Wrong Shutdown button | Guest actions are on the **VM**; host power-off is on the **node**. |
