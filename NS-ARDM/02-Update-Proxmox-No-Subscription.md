# Update a Proxmox Jumpbox (No Subscription)

**Applies to:** Proxmox VE **9.2.x** (confirmed target: 9.2.3)  
**Goal:** Receive normal security and package updates **without** a paid Proxmox subscription.

Out of the box, Proxmox points at the **Enterprise** update repository. Without a subscription key, refresh fails (often with a **401** error). You must:

1. Disable the Enterprise repo  
2. Enable the free **No-Subscription** repo  
3. Refresh and install updates  

Do this **once** per jumpbox. After that, updating is a short routine.

---

## Before you start

1. Prefer a time when VMs can be interrupted (or shut guests down first — see `03-Proper-Shutdown.md`).  
2. You need the Proxmox **root** password (or another account that can use the UI / Shell).  
3. The jumpbox must be on the internet.  
4. Know which machine you are updating (the **physical** Proxmox host, not a Windows/Linux guest).

**Words used here**

| Word | Meaning |
|------|---------|
| Jumpbox | Physical PC running Proxmox |
| Proxmox UI | Browser page `https://JUMPBOX-IP:8006` |

---

## Part A — One-time: switch to No-Subscription updates

### Method 1 — Web UI (easiest)

1. On any computer on the same network, open a browser.  
2. Go to: `https://JUMPBOX-IP:8006`  
   - Replace `JUMPBOX-IP` with the jumpbox address (from your router DHCP list if needed).  
   - Accept the certificate warning if the browser shows one (self-signed cert is normal).  
3. Log in (usually user `root`, Realm `Linux PAM`).  
4. In the left tree, click the **node** (the jumpbox computer name), not a VM.  
5. Open **Updates** → **Repositories**.  
6. Find the **Enterprise** / `pve-enterprise` entry.  
   - Select it → **Disable** (or equivalent).  
7. Click **Add**.  
8. Choose the **No-Subscription** Proxmox VE repository (`pve-no-subscription`).  
9. Save / OK.  
10. If a **Ceph Enterprise** repository appears and you are **not** running a Ceph cluster (typical for these jumpboxes), **Disable** it as well so it does not cause 401 errors.  
11. Open **Updates** (package list view) → **Refresh**.  
12. Confirm Refresh finishes **without** enterprise 401 errors.

If Refresh still fails, use Method 2 (Shell) below.

### Method 2 — Shell on the jumpbox

Use this if the Repositories UI is unclear or Refresh still errors.

1. In the Proxmox UI, select the **node** → **Shell**  
   *(or sit at the physical keyboard/monitor on the jumpbox and log in as root)*.  
2. Check version:

```bash
pveversion
```

You should see something like `pve-manager/9.2.3/...`.

3. List apt source files:

```bash
ls -la /etc/apt/sources.list.d/
```

4. Disable the Enterprise Proxmox repo (PVE 9 uses `.sources` files).  
   Open the file:

```bash
nano /etc/apt/sources.list.d/pve-enterprise.sources
```

Add this line under that repository entry (official key name):

```text
Enabled: no
```

Save: `Ctrl+O`, Enter, then exit: `Ctrl+X`.

*(If the file is missing and you only have an old `.list` file, skip to step 5 and add No-Subscription; then disable any enterprise line by putting `#` at the start of that line.)*

5. Create the No-Subscription repo file:

```bash
nano /etc/apt/sources.list.d/proxmox.sources
```

Paste **exactly**:

```text
Types: deb
URIs: http://download.proxmox.com/debian/pve
Suites: trixie
Components: pve-no-subscription
Signed-By: /usr/share/keyrings/proxmox-archive-keyring.gpg
```

Save and exit.

6. If `ceph.sources` exists and points at `enterprise.proxmox.com`, and you do **not** use Ceph: either disable it (`Enabled: no`) or change it to the public Ceph no-subscription URI documented by Proxmox. For most jumpboxes, **disabling** unused Ceph enterprise is enough.

7. Refresh package lists:

```bash
apt update
```

You want a clean finish with **no 401** from `enterprise.proxmox.com`.

---

## Part B — Install updates (routine)

Do this whenever you are told updates are available, or on a regular schedule.

### From the Web UI

1. Log into `https://JUMPBOX-IP:8006`.  
2. Select the **node**.  
3. **Updates** → **Refresh**.  
4. Review the list.  
5. Click **Upgrade** (or **Upgrade** in the toolbar — wording can vary slightly).  
6. A console/task window may open; let it finish. Answer `y` if a package asks a question and you are unsure — when in doubt, keep the default / maintainer choice unless an Elmer directs otherwise.  
7. If the task says a **reboot is required**, plan a proper shutdown/start of guests (`03-Proper-Shutdown.md`), then reboot the node (**Node → Reboot**) or from Shell: `reboot`.

### From the Shell

```bash
apt update
apt full-upgrade
```

If asked about config file changes, prefer keeping the local version unless you know a package must overwrite it.

Reboot if the upgrade says so:

```bash
reboot
```

---

## Part C — After updating

1. Confirm the node comes back: open `https://JUMPBOX-IP:8006` again.  
2. Start any VMs that do not auto-start (see `01-Connect-to-Jumpbox.md`).  
3. Spot-check important guests (Windows, Linux, AREDN).

Check version anytime:

```bash
pveversion -v
```

---

## Troubleshooting

| Problem | What to try |
|---------|-------------|
| `401 Unauthorized` on apt update | Enterprise repo still enabled — disable it; confirm `proxmox.sources` has `pve-no-subscription`. |
| “Subscription” popup in UI | Normal without a paid key. It does **not** block No-Subscription updates once repos are fixed. |
| Refresh finds nothing | Internet/DNS issue on the jumpbox; ping `download.proxmox.com` from Shell. |
| Wrong machine updated | You must update the **Proxmox host**, not a guest VM’s Windows Update / `apt` inside a Linux VM. |
| Ceph 401 errors | Disable unused Ceph enterprise repo (Part A). |

---

## Notes

- No-Subscription packages are appropriate for these internet-connected jumpboxes. Enterprise is for paid support contracts.  
- Do **not** enable the `pve-test` repository for normal jumpbox use.  
- Debian base repos must stay enabled (they usually already are).
