# Install and Use Raven on an AREDN Node

**Applies to:** AREDN **x86_64** (and other AREDN-supported) nodes, including virtual nodes on Proxmox  
**Goal:** Install **Raven** mesh messaging on a node so mesh members can use it from a web browser

This guide uses **AREDN terminology**. Your mesh may be a **private** mesh (not linked to the worldwide AREDN network). Raven and service advertisement still work the same way.

Upstream:

- AREDN chat overview: [Chat Programs — Raven](https://docs.arednmesh.org/en/latest/arednServicesGuide/chat_programs.html)  
- Raven project / packages: [github.com/kn6plv/Raven](https://github.com/kn6plv/Raven)  
- Raven wiki: [github.com/kn6plv/Raven/wiki](https://github.com/kn6plv/Raven/wiki)

---

## 1. Where Raven lives (important)

| Role | What it is | Raven? |
|------|------------|--------|
| **Node** | AREDN firmware device/VM (router on the mesh) | **Install Raven here** (node package) |
| **LAN device** | Computer on a node’s LAN (Linux Mint, Windows, Pi, “services” VM) | **Browser client only** — do not install the Raven node package here |
| **Operator PC** | Any machine that can reach the node Admin / Raven URL | Open Raven in a browser after login |

Raven is a **node package**. Mesh members typically do **not** install a separate Raven app on every PC. They browse to the node that runs Raven (or to its advertised service link).

---

## 2. Map this to a Proxmox jumpbox (example pattern)

Use this as a pattern; rename to match your site.

| Example name | AREDN role | Notes |
|--------------|------------|--------|
| **Node-0 / Node-1 / Node-2** | Mesh **nodes** (x86 VMs) | Pick **one** as the primary Raven host |
| **Linux Mint VM** | LAN (or mesh-reachable) workstation | Used to open node Admin and Raven |
| **Windows 11 VM** | Same | Same — browser client |
| Host with **2 NICs** | Physical Proxmox server | Only matters for how you bridge WAN/LAN/DtD; Raven install steps stay the same |

**Recommendation:** Install Raven on your **primary node** — usually the node that:

- Has the most RAM free  
- Is the one operators already open for Admin  
- Is best connected toward the rest of your private mesh  

You can install Raven on more than one node later (distributed messaging), but start with **one**.

---

## 3. Before you install

1. Node firmware is current enough for modern packages (prefer a recent snapshot or release — see `05-Update-AREDN-VM.md`).  
2. You can log into that node’s **web Admin** from a LAN device (Mint/Windows on the jumpbox is fine).  
3. Note free memory on the node (**Node Status** / Admin). AREDN docs: give Raven a node with **plenty of available memory**. x86 VMs can be given more RAM in Proxmox if needed (e.g. 512 MB–1 GB).  
4. Know the node’s name / IP / how you reach it (LAN IP, `.local.mesh` name, etc.).

Optional but smart: Proxmox **snapshot** of that AREDN VM before installing packages.

---

## 4. Download the Raven package

1. On Mint or Windows, open:  
   [https://github.com/kn6plv/Raven](https://github.com/kn6plv/Raven)  
2. Download the current install package from the repo root (or Releases if the project moves packages there).  
   Typical names look like:
   - `raven-alpha.apk`  
   - `raven-0.0.1-….apk`  
3. Prefer the **newest** `.apk` unless release notes say otherwise.  
4. Older AREDN builds sometimes used `.ipk`; if your node’s Package Upload rejects `.apk`, check the Raven repo/wiki for an `.ipk` build that matches your firmware era.

Save the file where the browser can upload it (Downloads folder is fine).

**GitHub tip:** open the file page → use the download (↓) control to save the binary, not the “View raw text” page.

---

## 5. Install Raven on the node (Package Upload)

UI labels vary slightly by AREDN version; look for **Packages** / **Package Management** / **Upload**.

1. From Mint or Windows, browse to the **primary node** Admin UI and **log in**.  
2. Open the **Packages** (or Administration → Packages) page.  
3. Use **Upload package** / **Browse…** and select the Raven `.apk` (or `.ipk`) file.  
4. Upload / install. Wait for success (no error banner).  
5. If the UI asks for a **reboot**, reboot the node cleanly:
   - Prefer node **Reboot** from Admin, or  
   - Console: follow your normal halt/reboot practice (`03-Proper-Shutdown.md` for full jumpbox shutdown; for package install a node **Reboot** is enough).  
6. After reboot, log into Admin again.

The package postinstall enables and starts the Raven service (`/etc/init.d/raven`).

---

## 6. Open Raven

1. Log into the node Admin UI.  
2. In the **left navigation**, open **Raven** (it becomes available after install / login).  
3. Confirm the Raven UI loads (channels such as **AREDN**, and possibly Meshtastic / Meshcore placeholders).  

First-time use:

- Identify with your **callsign** / mesh identity as your group requires.  
- Use the default **AREDN** channel for general mesh chat.  
- Create extra **channels** later for nets, EmComm, training, etc. (Raven configuration UI).

Raven is **not** compatible with MeshChat message databases — treat it as a separate system.

---

## 7. Let the rest of the mesh find it (Advertised Services)

Other operators should not need to memorize a raw IP. On the **same node** that runs Raven:

1. Admin → **Setup** → **Port Forwarding, DHCP, and Services** (name varies; look for **Advertised Services** / **Local Services**).  
2. If Raven did not auto-appear as a local service, **Add** an advertised service, for example:
   - **Name:** something clear (`Raven` or `SITE-Raven`)  
   - **Link:** checked (so it shows on Mesh Status)  
   - **Protocol:** `http` (or `https` if you terminate TLS that way — usually `http` on mesh)  
   - **Host:** this node (select from reservation/dropdown when required)  
   - **Port / path:** as required by your Raven/AREDN version (often the node’s web UI path that opens Raven — if unsure, use the working URL from your browser’s address bar after opening Raven)  
3. **Commit** / save. Reboot only if the UI requires it.  
4. On **Mesh Status** (this node or another), confirm the Raven link appears.

Private-mesh note: advertisement still propagates to nodes that can route to you. You do **not** need a worldwide AREDN connection for that.

---

## 8. How mesh members use Raven day to day

On any LAN device or mesh-connected PC (Mint, Windows, laptop at another site):

1. Open a browser.  
2. Either:
   - Click **Raven** on Mesh Status, or  
   - Open the node Admin URL → log in → **Raven** in the left pane.  
3. Join the appropriate channel and chat.

No Raven install on Mint/Windows is required for normal use.

---

## 9. Optional: more than one Raven node

Raven is described as **distributed**. After the primary node is proven:

- You may install Raven on additional nodes so messaging is more resilient if one node is down.  
- Coordinate **channel** names/keys with your group so everyone lands in the same conversations.  
- Still keep heavy services (Nextcloud, mail, etc.) on a **LAN server**, not on every node.

---

## 10. Memory / flash notes (x86 VMs)

From the Raven wiki (summary):

- Default: messages in flash, images in RAM (images ephemeral).  
- On real radio flash this raises wear questions; authors estimate wear is not a practical issue for normal use.  
- On **Proxmox x86** nodes your “disk” is a virtual disk — far less of a concern than NOR flash on a tiny radio.  
- You can still give the Raven node **extra RAM** in Proxmox for comfort.

---

## 11. Troubleshooting

| Problem | What to try |
|---------|-------------|
| Upload fails / wrong package type | Use current `.apk` for modern AREDN; confirm firmware age; try the other package format if the repo still publishes it. |
| No Raven in left nav | Log in (guest view may hide it); reboot node; confirm package listed under Packages. |
| Raven opens then errors | Free memory; raise VM RAM; check node System log. |
| Others cannot find Raven | Advertised Services + Link checked; their node can route to yours; try direct node URL. |
| GitHub download confusing | Open the `.apk` file → download arrow; don’t copy the HTML page. |
| Expected MeshChat history | Raven does not import MeshChat; start fresh channels. |
| Auto-update surprises | While Raven is in active development it may auto-update; note version after changes ([AREDN announcement](https://www.arednmesh.org/content/introducing-aredn-chat-client)). |

---

## Quick checklist

```
[ ] Choose primary node (enough free RAM)
[ ] Snapshot AREDN VM (Proxmox) — optional
[ ] Download Raven .apk from kn6plv/Raven
[ ] Node Admin → Packages → Upload → install
[ ] Reboot if required
[ ] Log in → left nav → Raven
[ ] Advertise service for Mesh Status
[ ] Test from Mint and/or Windows browsers
[ ] Tell mesh members the Mesh Status link / channel names
```

---

## Related NS-ARDM docs

- Connect to Proxmox / open node Admin: `01-Connect-to-Jumpbox.md`  
- Update node firmware before packages: `05-Update-AREDN-VM.md`  
- Clean node halt: `03-Proper-Shutdown.md`
