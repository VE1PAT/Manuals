# Recommended VE1DRR channel set (CPS)

Add these to a **training / regional codeplug** so students can join/leave talkgroups with the channel knob instead of only Manual Dial.

All rows use the same RF plant as channel **VE1DRR** in the working export.

## 1. Talk Group / Contact list (create these first)

In CPS: **Digital → Talk Groups** (names can vary; keep Type exact).

| Name (suggestion) | TG / DMR ID | Type |
|---|---|---|
| ATL Canada | 30205 | Group Call |
| NS 3021 | 3021 | Group Call |
| Canada 302 | 302 | Group Call |
| WW 91 | 91 | Group Call |
| Drop 4000 | **4000** | **Group Call** |
| Parrot 9990 | 9990 | **Private Call** |

`ATL Canada` may already exist in the baseline.

## 2. Channel rows (Public → Channel)

Use these fields unless the trustee publishes different slot preferences.  
**Color Code = 1**, **Channel Type = Digital**, **Band Width = 12.5 kHz**.

| Channel Name | RX MHz | TX MHz | TX Contact | Time Slot | Power | TX Admit | Notes |
|---|---|---|---|---|---|---|---|
| VE1DRR-30205 | 443.750 | 448.750 | ATL Canada | Slot 2 | High (or Low for local) | Color Code Idle (preferred) or Always | Club nets / default |
| VE1DRR-3021 | 443.750 | 448.750 | NS 3021 | Slot 2 | same | same | Nova Scotia |
| VE1DRR-302 | 443.750 | 448.750 | Canada 302 | Slot 2 | same | same | Canada Wide |
| VE1DRR-91 | 443.750 | 448.750 | WW 91 | Slot 2 | same | same | Worldwide — use sparingly |
| VE1DRR-Parrot | 443.750 | 448.750 | Parrot 9990 | Slot 2 | Low | same | Private echo test |
| **VE1DRR-Drop** | 443.750 | 448.750 | **Drop 4000** | Slot 2 | Low | same | **Un-join** dynamic TGs |

Optional: keep the existing memory named `VE1DRR` as an alias of `VE1DRR-30205`, or rename it for clarity.

### Other useful CPS checkboxes (per channel)

| Field | Suggestion |
|---|---|
| Forbid Talkaround | Checked |
| APRS Report | Off on most; On only on the channel you want for APRS beacons |
| RX Group List | Start with existing **RX Group 1** if it already includes ATL Canada; expand later so you can hear the TGs you use |

## 3. Zone membership

Put all `VE1DRR-*` channels in one zone (e.g. **VE1DRR** or **DMR Metro**), in this order:

1. VE1DRR-30205  
2. VE1DRR-3021  
3. VE1DRR-302  
4. VE1DRR-91  
5. VE1DRR-Parrot  
6. **VE1DRR-Drop**

## 4. How operators use the new set

| Goal | Action |
|---|---|
| Club Atlantic net | Select **VE1DRR-30205** → PTT |
| Leave current TG | Select **VE1DRR-Drop** → wait for a gap → PTT 2–5 seconds |
| Move to NS | **Drop** first → then **VE1DRR-3021** → PTT |
| Radio check | **VE1DRR-Parrot** → PTT → listen for echo |

Without these memories, use Manual Dial as in Chapter 8 of the operating manual (group **4000**, then group **new TG**).

## 5. After editing

1. Save the codeplug as a new dated `.data` file.  
2. Write to a test radio; confirm Drop and 30205.  
3. Use that file as the class / regional example going forward.

Do not commit personal `.data` files to the manuals repo.
