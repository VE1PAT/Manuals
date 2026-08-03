# Connect a Project Nomad Host to the Mesh (AREDN LAN)

**Applies to:** A separate physical PC running **Project Nomad** (Docker modules) beside a Proxmox jumpbox that hosts AREDN nodes  
**Goal:** Put Nomad on an AREDN node’s **LAN** so mesh members can reach its services, with minimal change on the Nomad box

This guide uses **AREDN terminology**. Your mesh may be private (not linked to the worldwide AREDN network). The same LAN + Advertised Services pattern applies.

---

## 1. Mental model

| Machine | Role |
|---------|------|
| **Proxmox jumpbox** | Hosts AREDN **nodes** (and operator VMs). One physical NIC should face the AREDN **LAN**. |
| **AREDN node** | Mesh **router**. Gives Nomad a LAN address, routes mesh traffic, **advertises** Nomad services. |
| **Project Nomad PC** | Application host (Docker). Treated like any other LAN device (laptop, Pi, file server). |

```
[Private mesh]
      ↕
[AREDN node on Proxmox]
      ↕ LAN (Ethernet)
[Project Nomad desktop — Docker]
```

You do **not** install AREDN or Raven on the Nomad PC. You **attach** Nomad to a node’s LAN.

---

## 2. What changes where

| Place | Work level | Typical changes |
|-------|------------|-----------------|
| **Nomad PC** | Small | Ethernet to AREDN LAN; DHCP or static in LAN subnet; gateway/DNS toward the node; firewall allows mesh clients; Docker listens on the LAN interface |
| **Proxmox + AREDN node** | Main work | Bridge a physical NIC (or VLAN) to the node’s **LAN**; DHCP reservation; **Advertised Services** |

---

## 3. Recommended wiring (two desks side by side)

Assume the jumpbox has **two NICs** (adapt names to your host):

| Proxmox NIC | Typical role |
|-------------|--------------|
| **NIC A** | Home / internet / Proxmox management (`https://JUMPBOX-IP:8006`) |
| **NIC B** | Dedicated **AREDN LAN** toward Nomad (and other LAN devices) |

### Steps (physical)

1. Choose which AREDN VM is Nomad’s parent node (call it the **primary LAN node**).  
2. In Proxmox, ensure that node has a network interface on a bridge bound to **NIC B** (or the VLAN that is untagged LAN).  
3. Connect:
   - **Option A:** NIC B → small Ethernet switch → Nomad Ethernet  
   - **Option B:** Direct cable NIC B ↔ Nomad Ethernet  
4. Keep NIC A for management/home so you do not strand Proxmox Admin on the mesh-only segment.

### If you use a VLAN-aware switch

Classic AREDN Ethernet roles (when trunked):

| Traffic | Typical 802.1Q |
|---------|----------------|
| **LAN** | Untagged (Nomad lives here) |
| **WAN** | VLAN 1 (often) |
| **DtD** | VLAN 2 (often) |

Nomad must land on **LAN** (untagged), not WAN or DtD.

---

## 4. Configure the AREDN node (LAN parent)

1. Log into the primary LAN node Admin.  
2. Confirm **LAN** settings (subnet / DHCP range) under basic/network setup.  
3. Power Nomad on with Ethernet connected; confirm it appears in the node’s DHCP leases.  
4. **Port Forwarding, DHCP, and Services** (label varies):
   - Create a **DHCP reservation** for Nomad (by MAC) so its IP stays stable.  
   - Under **Advertised Services**, **Add** each Nomad web app you want on Mesh Status, for example:
     - Name: `Nomad` or `SITE-Nomad`  
     - Link: checked  
     - Protocol: `http` (or `https` if you terminate TLS on Nomad)  
     - Host: Nomad’s reserved LAN address (dropdown after reservation)  
     - Port / path: as published by that Docker module  
5. Commit / save. Reboot the node only if the UI requires it.

Mesh members then open the service from **Mesh Status** instead of memorizing IPs.

---

## 5. Configure the Nomad PC (minimal)

1. Use the Ethernet interface that faces the AREDN LAN.  
2. Addressing (pick one):
   - **DHCP** from the AREDN node (simplest), or  
   - **Static** IP inside the node’s LAN subnet, with:
     - Gateway = **node LAN IP**  
     - DNS = node LAN IP (or your mesh DNS practice) so `.local.mesh` names work when used  
3. Confirm from Nomad:
   - Ping the node LAN IP  
   - Open the node Admin UI in a browser  
4. Docker:
   - Publish services on `0.0.0.0` (or the LAN IP), not only `127.0.0.1`  
   - Host firewall allows access from the mesh/LAN ranges you use  
5. Optional: set a stable hostname that matches what you advertise.

### Dual-homed Nomad (optional later)

If Nomad keeps a second NIC on home internet **and** one on AREDN LAN:

- Default route → home (for Docker image pulls, etc.)  
- **Static routes** for mesh prefixes via the AREDN node LAN IP  

More complex; start **single-homed on AREDN LAN** when possible.

---

## 6. Verify end-to-end

| Test | From | Expect |
|------|------|--------|
| Node Admin | Nomad browser | Loads |
| Nomad HTTP app | Linux Mint / Windows on the jumpbox (mesh/LAN path) | Loads via IP or Mesh Status link |
| Advertisement | Another node’s **Mesh Status** | Nomad service link visible |
| After Nomad reboot | Reservation | Same LAN IP |

---

## 7. What not to do

| Avoid | Why |
|-------|-----|
| Nomad only on home Wi‑Fi with no routes to mesh | Mesh hosts cannot reach Docker apps reliably |
| Putting Nomad on WAN or DtD by mistake | Wrong AREDN zone; breaks the LAN-device pattern |
| Installing AREDN firmware on Nomad | Wrong role — Nomad is a **LAN service host** |
| Expecting Proxmox host updates to change Nomad | Unrelated systems |

---

## 8. Example site map (ve1patvm01)

Captured from Proxmox **System → Network** and AREDN VM **Hardware** screens (PVE 9.2.x). Use as a worked example; re-check with the commands in §9 if hardware moves.

### Proxmox host bridges

| Proxmox name | Type | Bound physical NIC | Notes |
|--------------|------|--------------------|-------|
| **nic0** | Network Device | Onboard-style (`enp0s25`; may also show a USB-style alt name) | Slave of **vmbr0** |
| **nic1** | Network Device | Add-on USB Ethernet (`enx…`) | Slave of **vmbr1** — usual place for a desk cable to Project Nomad |
| **vmbr0** | Linux Bridge | **nic0** | Home / management path (also used by VE1PAT-01) |
| **vmbr1** | Linux Bridge | **nic1** | Physical “mesh desk” segment (VE1PAT-00, VE1PAT-02) |
| **vmbr10** | Linux Bridge | *(none — virtual only)* | Inter-node link fabric inside Proxmox |
| **vmbr20** | Linux Bridge | *(none — virtual only)* | Extra virtual segment (VE1PAT-01) |

### AREDN VMs → bridges

| VMID | Name | Guest NICs |
|------|------|------------|
| **1000** | **VE1PAT-00** | `net0` → **vmbr1** |
| **1001** | **VE1PAT-01** | `net0` → **vmbr20**; `net1` → **vmbr0**; `net2` → **vmbr10** |
| **1002** | **VE1PAT-02** | `net0` → **vmbr1**; `net1` → **vmbr10** |

```
                    ┌─ vmbr20 ── VE1PAT-01 net0
nic0 ── vmbr0 ──────┼─ (home / Proxmox mgmt / VE1PAT-01 net1)
                    │
nic1 ── vmbr1 ──────┼─ VE1PAT-00 net0
                    └─ VE1PAT-02 net0
                         ▲
                         │ Ethernet (add-on NIC)
                    Project Nomad PC

vmbr10 (no physical port): VE1PAT-01 net2 ↔ VE1PAT-02 net1  (and any other DtD-style peers)
```

**Nomad implication:** If Nomad is cabled to the **add-on** NIC, it sits on **vmbr1** with **VE1PAT-00** and **VE1PAT-02**. Pick one of those nodes as the **LAN parent** only after confirming (in that node’s AREDN Admin) that the interface on `vmbr1` is actually presenting **LAN** (DHCP for devices), not only DtD/WAN. Virtual bridges `vmbr10` / `vmbr20` never carry a copper cable to Nomad.

Still fill in after first successful attach:

| Item | Your value |
|------|------------|
| Primary AREDN LAN node for Nomad | *(VE1PAT-00 or VE1PAT-02 once LAN role is confirmed)* |
| Nomad MAC / reserved LAN IP | |
| Advertised service names / ports | |

Host DNS on this example node used search domain `home` and ordinary recursive resolvers for the Proxmox host itself — that is **Proxmox management DNS**, not the mesh DNS Nomad should use once it is on AREDN LAN (then use the node LAN IP / mesh practice).

---

## 9. Commands: map names → physical NICs

Run these in the **Proxmox host shell** (`ve1patvm01` → **Shell**), not inside an AREDN VM.

### Bridge and NIC inventory

```bash
# What Proxmox thinks the bridges are
cat /etc/network/interfaces

# Live links: which interfaces are UP, MAC, and master bridge
ip -br link
bridge link
```

Expect something like: `enp0s25` / `nic0` as a slave of `vmbr0`, and the add-on `enx…` / `nic1` as a slave of `vmbr1`.

### Which cable is which (best proof)

1. Note which desk cable goes to Nomad.  
2. Unplug / replug that cable while watching:

```bash
# Repeat a few times while you unplug/replug
ip -br link
dmesg -T | tail -n 30
```

The interface whose state flips `DOWN` ↔ `UP` (or shows link messages in `dmesg`) is the physical NIC on that cable. Match its name to the `bridge-ports` line in `/etc/network/interfaces`.

Optional blink (if `ethtool` is installed):

```bash
ethtool -p enp0s25    # or the enx… name — LED blinks on that port
```

Stop with `Ctrl+C`.

### Confirm which VMs use that bridge

```bash
grep -E 'net[0-9]:|bridge=' /etc/pve/qemu-server/*.conf
```

Or in the UI: each VM → **Hardware** → **Network Device** → `bridge=vmbr…` (same data as §8).

### On Project Nomad (after cable + DHCP)

Linux:

```bash
ip -br addr
ip route
ping -c 3 <AREDN-node-LAN-IP>
```

Windows (PowerShell):

```powershell
Get-NetAdapter | Format-Table Name, InterfaceDescription, Status, MacAddress
Get-NetIPConfiguration
ping <AREDN-node-LAN-IP>
```

---

## Quick checklist

```
[ ] Identify add-on NIC ↔ vmbr (link flap / ethtool)
[ ] Pick primary AREDN LAN node on that bridge
[ ] Confirm node Admin shows LAN/DHCP on that segment
[ ] Cable Nomad → that LAN segment
[ ] Nomad gets LAN IP (DHCP or static + node as gateway)
[ ] DHCP reservation on the node
[ ] Advertised Services for Nomad apps
[ ] Test from Nomad → node Admin
[ ] Test from mesh workstation → Nomad apps
```

---

## Related NS-ARDM docs

- Connect to Proxmox / open node Admin: `01-Connect-to-Jumpbox.md`  
- Raven on a **node** (not on Nomad): `06-Install-Raven.md`  
- Create/update AREDN x86 VMs: `04-Create-AREDN-x86-VM.md`, `05-Update-AREDN-VM.md`
