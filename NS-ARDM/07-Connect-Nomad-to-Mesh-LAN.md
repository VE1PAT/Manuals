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

## 8. Adapting to your site

Fill this in for your jumpbox (keeps the doc reusable):

| Item | Your value |
|------|------------|
| Proxmox NIC for AREDN LAN | |
| Bridge / VLAN name | |
| Primary AREDN node (VM name) | |
| Nomad MAC / reserved LAN IP | |
| Advertised service names / ports | |

---

## Quick checklist

```
[ ] Pick primary AREDN LAN node
[ ] Bridge node LAN to physical NIC B (or LAN VLAN)
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
