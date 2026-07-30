# CPS 1.45 — Digital section walkthrough (DM-32UV)

**Software:** Baofeng CPS DMR **V1.45** (club standard — do not use 1.60 for the shared baseline yet)  
**Goal:** Build / maintain the club digital baseline for VE1DRR loaners  
**Audience:** Codeplug custodian (not the casual borrower)

This guide matches the **Digital** tree in CPS 1.45:

```
Digital
├── DMR ID
├── Talk Groups
├── CSV Contacts
├── RX Group List
├── Digital Emergency Systems
├── Digital Encrypt Systems
└── Quick Text Messages
```

Many “how to DMR” articles use other radios’ CPS names (Contact Manager, Digital Contacts, Rx Group, etc.). **Trust this tree**, not those labels.

---

## Before you touch Digital

1. Cable connected, radio on, correct **COM** port (**Setting → COM Setting**).  
2. **Program → Read data** from a known-English radio.  
3. **File → Save As** a dated backup.  
4. **Never File → New** (can push Chinese menus).

Work order that avoids frustration:

```
DMR ID  →  Talk Groups  →  RX Group List  →  (Public) Channels  →  Zones  →  Save  →  Write
```

Leave **CSV Contacts**, **Emergency**, **Encrypt**, and **Quick Text** until the radio already keys VE1DRR correctly — or skip them for loaners.

---

## Map: what each Digital item actually is

| CPS 1.45 item | Plain English | Needed for club loaners? |
|---|---|---|
| **DMR ID** | *Your* radio identity on the network (number + name) | **Yes — every borrower** |
| **Talk Groups** | Address book of **call targets** used as **TX Contact** on channels (group *and* private) | **Yes** |
| **CSV Contacts** | Huge name lookup list (who is calling you) | Optional |
| **RX Group List** | Which **group** calls this channel will **hear** | **Yes** (or you only hear your TX TG) |
| **Digital Emergency Systems** | Alarm / emergency call profiles | **No — leave alone** |
| **Digital Encrypt Systems** | Encryption keys | **No — do not use on amateur air** |
| **Quick Text Messages** | Canned DMR SMS phrases | Optional |

### Talk Groups vs CSV Contacts (the usual confusion)

| | **Talk Groups** | **CSV Contacts** |
|---|---|---|
| Purpose | Things you **call** (TX Contact / Manual Dial list building blocks) | Things you **recognize** when they call you |
| Contains | TG 30205, Drop 4000, Parrot 9990, … | Thousands of callsigns / DMR IDs |
| Used by channel field | **TX Contact** | Display / `#` CSV lookup |
| Size | Small list you maintain by hand | Large import file |

If a guide says “add a contact for talkgroup 91”, in CPS 1.45 that means **Digital → Talk Groups**, not CSV Contacts.

---

## 1. DMR ID

**Path:** Digital → **DMR ID**

### What it does

Every DMR transmission tags your radio with this number. BrandMeister and other users see it. Wrong leftover ID = transmitting as the previous borrower.

### Club baseline (idle loaner)

| Field | Value |
|---|---|
| ID | Club placeholder policy (empty/disabled policy — or a non-personal placeholder the custodian defines) |
| Name | e.g. `CLUB LOANER` |

### At checkout (borrower)

| Field | Value |
|---|---|
| ID | Borrower’s number from radioid.net |
| Name | Borrower’s callsign (e.g. `VE1ABC`) |

### Steps

1. Open **Digital → DMR ID**.  
2. Double-click row 1.  
3. Set **ID** and **Name**.  
4. Delete or clear extra rows that belong to old users.  
5. OK → Save As.

**Loaner rule:** one active personal ID only while checked out; restore baseline on return.

You can have multiple DMR ID rows for advanced use; loaners should not need that.

---

## 2. Talk Groups

**Path:** Digital → **Talk Groups**

### What it does

Creates the selectable **TX Contact** entries for digital channels. Despite the name, this list holds:

- **Group Call** entries (real talkgroups: 30205, 4000, …)  
- **Private Call** entries (parrot 9990, a friend’s DMR ID, APRS gateway 302999, …)

### Create these for the club baseline

Double-click an empty row (or Add), fill, OK. Repeat.

| Name | TG / DMR ID | Type |
|---|---|---|
| ATL Canada | 30205 | Group Call |
| NS 3021 | 3021 | Group Call |
| Canada 302 | 302 | Group Call |
| WW 91 | 91 | Group Call |
| Drop 4000 | 4000 | **Group Call** |
| Parrot 9990 | 9990 | **Private Call** |
| APRS 302999 | 302999 | **Private Call** (only if you will configure APRS) |

### Tips

- Put the **number in the name** (`NS 3021`) so you can tell networks apart later.  
- **Drop 4000 must be Group Call** — Private 4000 is not the BrandMeister TG disconnect.  
- Do not import the entire BrandMeister universe here; keep this list short.

When channels are built (later), each digital channel’s **TX Contact** points at one of these rows.

---

## 3. CSV Contacts

**Path:** Digital → **CSV Contacts**

### What it does

Optional “phone book.” When someone private-calls or appears on the air, the radio can show **callsign / city** instead of only a number — *if* that ID is in this list.

### Loaner recommendation

| Approach | When |
|---|---|
| **Leave empty / untouched** | Simplest loaners; less CPS pain |
| Import a trimmed regional CSV later | Nice-to-have after VE1DRR works |

### If you import

1. Use a CSV format the CPS expects (RadioID-style exports; columns must match what 1.45 offers under import).  
2. Prefer a **small** Atlantic / Canada extract over a full world dump on loaners (write time + confusion).  
3. CSV Contacts do **not** replace Talk Groups. You still need Talk Groups for TX Contact.

Borrowers can still Manual Dial a raw DMR ID without CSV Contacts.

---

## 4. RX Group List

**Path:** Digital → **RX Group List**

### What it does

On a digital channel you always transmit to **TX Contact**.  
**RX Group List** answers: “Which **group calls** may I **hear** on this channel?”

If RX Group List is empty / None / too narrow, you may:

- Transmit fine on 30205, but  
- Miss other group traffic you expected to hear on that RF channel, or  
- Only hear the single TG you transmit to (depending on settings)

### Club starting point

1. Open **RX Group List**.  
2. Edit **RX Group 1** (or create `VE1DRR Listen`).  
3. Add **Group Call** members from Talk Groups, for example:

| Member |
|---|
| ATL Canada |
| NS 3021 |
| Canada 302 |
| WW 91 |

Do **not** put Private Call entries (Parrot, APRS) in an RX group list — those are not group receive memberships.

4. Later, on each VE1DRR-* channel (**Public → Channel**), set **RX Group List** = this list.

### Practical loaner policy

| Policy | Effect |
|---|---|
| One shared RX list on all VE1DRR TG channels | Simple; hear any of those TGs while parked on a VE1DRR memory (still only TX to that channel’s TX Contact) |
| Separate RX lists per channel | Stricter; usually unnecessary for beginners |

**Drop 4000** and **Parrot** channels: RX list can stay the shared list or None; you are not “listening for 4000 traffic.”

---

## 5. Digital Emergency Systems

**Path:** Digital → **Digital Emergency Systems**

### What it is

Commercial-style emergency alarm / emergency call configurations (panic, emergency indicator, related channel behaviour).

### Club loaner action

**Do not configure. Do not assign to channels.**  

Leave factory defaults / empty. Skip any guide that starts with “set up Emergency System” unless your clubs adopt a formal EmComm SOP later (separate topic manual).

---

## 6. Digital Encrypt Systems

**Path:** Digital → **Digital Encrypt Systems**

### What it is

AES / ARC4 / custom key storage for encrypted digital voice.

### Club loaner action

**Leave empty. Do not enable Encryption on any amateur channel.**

Encrypted amateur transmissions are not appropriate for normal HARC/DARC loaner use and conflict with typical amateur rules/expectations. Ignore tactical/YouTube encryption tutorials for this fleet.

---

## 7. Quick Text Messages

**Path:** Digital → **Quick Text Messages**

### What it is

Pre-written DMR SMS strings (canned messages) you can send quickly from the radio menu.

### Club loaner action

**Optional.** Examples if you want them later:

- `QRZ?`  
- `QSY Atlantic 30205`  
- `Testing loaner radio`

Not required for voice nets on VE1DRR. APRS position beacons are **not** configured here (that is APRS / Option Feature / BrandMeister SelfCare — see loaner manual Chapter 10).

---

## After Digital: wire it to Channels and Zones

Digital entries do nothing on the air until **Public → Channel** (and **Zone**) use them.

### For each new VE1DRR memory

**Public → Channel** → add/edit:

| Field | Value |
|---|---|
| Channel Name | e.g. `VE1DRR-30205` |
| RX / TX | 443.750 / 448.750 |
| Channel Type | Digital |
| Color Code | 1 |
| Time Slot | Slot 2 |
| **TX Contact** | Pick from **Talk Groups** (e.g. ATL Canada) |
| **RX Group List** | Your shared list from step 4 |
| TX Admit | Color Code Idle (preferred) or Always |
| Forbid Talkaround | Checked |
| Encryption | Off |
| Emergency | None |
| DMR ID | Usually the radio’s active ID (row from Digital → DMR ID) |

Full recommended set: [`recommended-ve1drr-channels.md`](recommended-ve1drr-channels.md)

### Zone

**Public → Zone** → put all `VE1DRR-*` channels in one zone (Drop last).

### Save / Write

1. **File → Save As** dated club baseline.  
2. **Program → Write data**.  
3. Test: 30205, group **4000** drop, parrot **9990**, analog still OK.

---

## Custodian “Digital only” checklist

| Done | Step |
|:---:|---|
| ☐ | Read radio; Save As backup |
| ☐ | **DMR ID** set (placeholder or borrower) |
| ☐ | **Talk Groups** created (30205, 3021, 302, 91, 4000 group, 9990 private) |
| ☐ | **RX Group List** includes those group TGs |
| ☐ | **CSV Contacts** skipped or imported on purpose |
| ☐ | **Emergency** untouched |
| ☐ | **Encrypt** empty / unused |
| ☐ | **Quick Text** skipped or minimal |
| ☐ | Channels point at TX Contact + RX Group List |
| ☐ | Channels added to a Zone |
| ☐ | Write + on-air test |

---

## Why other docs feel wrong

| What you read elsewhere | In CPS 1.45 that usually means |
|---|---|
| “Digital Contacts” / “Contacts” | **Talk Groups** (for TX) and/or **CSV Contacts** (for names) |
| “Rx Group” / “Receive Group” | **RX Group List** |
| “Radio ID” | **DMR ID** |
| “Privacy” / “Basic Privacy” | **Digital Encrypt Systems** (skip on ham) |
| “Emergency” | **Digital Emergency Systems** (skip for loaners) |
| AnyTone / CPS menus | Different product — ignore label mapping |

Stick to the left-hand **Digital** tree in **V1.45** and this order: **ID → Talk Groups → RX Group List → Channels → Zones**.

---

## Related files

| File | Role |
|---|---|
| [`../DM-32UV-Loaner-Manual.md`](../DM-32UV-Loaner-Manual.md) | Borrower-facing handbook |
| [`recommended-ve1drr-channels.md`](recommended-ve1drr-channels.md) | Exact VE1DRR channel / contact table |
| [`baseline-channels-sanitized.csv`](baseline-channels-sanitized.csv) | Current sanitized channel map |
