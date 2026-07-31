# Halifax & Dartmouth Amateur Radio Clubs  
# DM-32UV Operating Manual

**Baofeng DM-32UV — how to get on the air**  
From zero to working on local analog repeaters and **VE1DRR** DMR

| | |
|---|---|
| **Document** | HARC / DARC DM-32UV Operating Manual |
| **Audience** | Licensed amateurs learning the Baofeng DM-32UV |
| **Assumes** | You have a valid Canadian amateur licence and callsign |
| **Radio** | Baofeng DM-32UV (analog + DMR Tier II, GPS, digital APRS) |
| **Version** | 0.5 |

**Scope:** Club **education** — how to operate and program the DM-32UV for local analog and VE1DRR DMR.

### Publication and privacy

- This handbook has **no personal author byline**. Do not add individual names, callsigns, emails, or home paths to distributed copies.
- When exporting to PDF, DOCX, or print tooling, leave **Author / Manager / Company / Keywords** metadata **blank**. Do not embed club or personal identity in file properties.
- Do not distribute personal `.data` codeplugs in shared folders or this repo.

Sources used while compiling this handbook are listed in **Annex F**.

---

## How to use this book

Read **Chapters 1–7** before you transmit on DMR.  
That gets you from first power-on to a working ID on **VE1DRR**.

| If you want to… | Go to |
|---|---|
| Use analog / weather listen | Chapters 6 and 6A |
| Change or **leave** a talkgroup (incl. **4000**) | Chapter 8 (**important** for this codeplug) |
| Call one person by DMR ID | Chapter 9 |
| Send your position (APRS) | Chapter 10 |
| Fix common problems | Chapter 11 |
| See what is actually programmed | Appendix B |

**Important:** Menu labels can vary slightly by firmware. Paths below match the official DM-32UV manual and CPS practice. If a label differs, look for the same idea (Talk Group, Manual Dial, Contacts, APRS, GPS).

---

## Chapter 1 — What you’re working with

For this course of study you need:

1. A Baofeng **DM-32UV** handheld  
2. Battery and antenna  
3. USB-C charger and/or drop-in charger  
4. Kenwood-style **2-pin programming cable** (USB)  
5. A Windows PC with Baofeng **CPS 1.45**  
6. A **codeplug** with metro analog, marine weather (RX), and DMR starters including **VE1DRR** (Appendix B describes a working regional example)

### What a good regional codeplug already includes

- Local **analog** repeaters (see Appendix B).  
- **VE1DRR** digital channel (443.750 / 448.750, color code **1**, time slot **2**) with TX contact **ATL Canada** (talkgroup **30205**).  
- Additional DMR memories for other Atlantic-area machines and an optional hotspot simplex channel (if present).  
- Marine continuous-broadcast / weather-related channels programmed **receive-oriented** (transmit inhibited in the working codeplug).

### What you must do to operate on DMR

1. Get your own DMR ID (Chapter 3).  
2. Optionally create a BrandMeister account (Chapter 5 — needed for APRS SelfCare).  
3. Write **your** DMR ID into the radio (Chapter 4).

### Codeplug reality check (read this)

The working baseline uses **one primary talkgroup contact** — **ATL Canada (30205)** — on the VE1DRR (and related) digital channels.  
That means:

- Selecting channel **VE1DRR** and pressing PTT calls **30205** (Atlantic Canada). Perfect for club DMR nets.  
- Other talkgroups (**3021**, **302**, **91**, parrot **9990**, etc.) are reached with **Manual Dial** (Chapter 8) or dedicated channels once added.  
- To **leave** a linked TG before switching: **group call 4000** (Chapter 8).

### Legal reminder

You may only transmit if you hold a valid licence. Identify with your callsign. Follow ISED rules and club repeater etiquette.  
**Do not transmit** on marine distress or marine broadcast channels. Those memories are for monitoring.

---

## Chapter 2 — Radio orientation (5 minutes)

### Controls you will use constantly

| Control | Typical use |
|---|---|
| Power / volume | On/off and audio level |
| Channel knob | Memory channels within the current zone |
| PTT | Transmit |
| Menu / OK | Enter menus; confirm |
| Back / Exit | Leave menus |
| ▲ / ▼ or rocker | Move through lists |
| `#` | On digital: switch Manual Dial private ↔ group |
| Zone / key shortcuts | Change memory bank (zone) |

### Zones and scan lists

Channels live in **zones**. If you “can’t find” a channel, change zone.

Scan lists present in the working codeplug include (names may vary slightly):

| Scan list | Typical contents |
|---|---|
| **VHF** | Local 2 m analog repeaters / simplex |
| **UHF** | Local 70 cm analog |
| **DMR** | Digital memories (e.g. VE1DRR) |
| **WX-CH** | Marine weather / CMB listen channels |

**Rule:** Scanning weather while also scanning voice nets can be noisy — use the WX list when you specifically want weather.

### Analog vs digital

| Mode | What you hear | What you need |
|---|---|---|
| Analog (FM) | Normal FM voice | Frequency + tone (in codeplug) |
| Digital (DMR) | Digital voice; silence when idle | Your DMR ID + color code, timeslot, talkgroup/contact |

---

## Chapter 3 — Get your DMR ID (RadioID.net)

There is **no separate “BrandMeister ID.”**  
BrandMeister uses the worldwide **DMR ID** issued by [radioid.net](https://radioid.net).

### Steps

1. Open [https://radioid.net](https://radioid.net) and create an account.  
2. Apply for a **DMR ID** for your amateur callsign.  
3. Upload whatever proof the site currently requires (often a licence PDF).  
4. Wait for approval.  
5. Record your numeric ID (many Canadian IDs look like `302xxxxx`).

### While you wait

- Use **analog** and **weather listen** immediately (Chapters 6 / 6A).  
- Do **not** transmit on DMR using someone else’s leftover ID.

| Service | Purpose |
|---|---|
| **radioid.net** | Issues your permanent DMR ID number |
| **brandmeister.network** | Network SelfCare (APRS icon, SMS brand, dashboards) |

---

## Chapter 4 — Put your DMR ID into the radio (CPS)

You need a Windows PC and the programming cable.  
**Do not use CHIRP.** Use Baofeng **CPS** for the DM-32UV (official download area). Club standard: **CPS 1.45**.

### Golden rules

1. **Always Read** from the radio first. Never start with **File → New** (can switch menus to Chinese on some CPS versions).  
2. Change **only** the DMR ID / radio name fields unless an Elmer is helping.  
3. Save a backup before writing.  
4. After writing, confirm your callsign appears as expected.

### Procedure (minimum change)

1. Install CPS if needed; plug in the cable.  
2. Power on the radio; connect the cable.  
3. CPS: **Setting → COM Setting** → choose the COM port that appeared when the cable was plugged in.  
4. **Program → Read data**.  
5. **File → Save As** — e.g. `DM32_backup_before_edit.data`.  
6. **Digital → DMR ID** → set **ID** = your RadioID number, **Name** = your callsign.  
7. Clear leftover ID rows that are not yours.  
8. **File → Save As** → `DM32_YOURCALL_YYYYMMDD.data`.  
9. **Program → Write data**.  
10. Disconnect, reboot, verify.

For the full Digital menu tree in CPS 1.45, see [`CPS-1.45-Digital-Section-Walkthrough.md`](CPS-1.45-Digital-Section-Walkthrough.md).

---

## Chapter 5 — BrandMeister SelfCare (recommended)

1. Register at [https://brandmeister.network](https://brandmeister.network).  
2. Link the same DMR ID you put in the radio.  
3. Open **SelfCare**.  
4. Club default for DM-32UV APRS / SMS:  
   - **Brand:** Motorola (matches CPS **M-SMS**)  
   - **APRS Callsign:** your callsign with SSID `-7` (handheld)  
   - **APRS Icon:** person / handheld  
   - Optional APRS text  

Skip SelfCare for basic 30205 QSOs if you must; complete it before relying on APRS.

---

## Chapter 6 — Analog first (local repeaters)

Analog memories are already programmed. Goal: a successful FM contact without CPS.

### Channels in the working baseline (amateur)

| Channel name | Type | RX (MHz) | TX (MHz) | Decode tone (as programmed) |
|---|---|---|---|---|
| VE1DAR-V | Analog | 147.150 | 147.750 | None |
| VE1PKT-V | Analog | 146.685 | 146.085 | 82.5 |
| VE1SHU-V | Analog | 146.865 | 146.265 | None |
| VE1PSR-V | Analog | 147.270 | 147.870 | 82.5 |
| VE1HNS-V | Analog | 146.940 | 146.340 | 82.5 |
| VE1CDN-V | Analog | 146.970 | 146.370 | None |
| Natl Simplex-V | Analog | 146.520 | 146.520 | None |
| SAR-V | Analog | 149.080 | 149.080 | None — **club/authorized use only** |
| VE1DAR-U | Analog | 444.600 | 449.600 | None |
| VE1PSR-U | Analog | 444.350 | 449.350 | None |
| VE1CDN-U | Analog | 442.975 | 447.975 | 82.5 |
| Natl Simplex-U | Analog | 446.000 | 446.000 | None |

If encode (TX tone) is blank in the codeplug but the repeater needs a tone, you may hear the repeater and still fail to bring it up — ask an Elmer to correct encode settings in the baseline.

### Known issue to fix in the baseline

| Channel | Problem | Correct target (verify before writing) |
|---|---|---|
| **VE1MTT-V** | Export showed an invalid RX of **400.000** MHz | Common listing: **147.045** RX / **147.645** TX (Beaver Bank) — confirm current tone/offset before use |

### Operating steps

1. Open a VHF or UHF zone that contains the memories above.  
2. Pick a known local repeater (start with **VE1DAR-V** or **VE1PSR-V**).  
3. Listen first.  
4. Identify with your callsign.  
5. Use the lowest power that works.

### Club nets (analog)

Schedules change. Dartmouth often runs a Thursday evening net on VE1DAR (147.150 / 444.600). Confirm on the club website before relying on a time.

---

## Chapter 6A — Marine weather / CMB (listen only)

Environment Canada **Weatheradio** / Hello Weather service for Nova Scotia has been discontinued. Continuous marine / MSI-style broadcasts from the Canadian Coast Guard remain a practical VHF way to hear marine weather and safety information in this region.

### Channels in the working baseline

| Channel name | RX (MHz) | Role | TX |
|---|---|---|---|
| Marine WX 21B | 161.650 | CCG continuous marine broadcast (CMB) | **Inhibited** in codeplug |
| Marine WX 23B | 161.750 | CCG CMB | **Inhibited** |
| Marine WX 25B | 161.850 | Marine / MSI-related broadcast use | **Inhibited** |
| Marine WX 26 | 161.900 | Marine / MSI-related broadcast use | **Inhibited** |
| Marine WX 83B | 161.775 | CCG CMB | **Inhibited** |
| Marine DISTRESS | 156.800 | VHF Ch 16 (distress/safety calling) | **Inhibited** |

### Rules

1. **Listen only.** Do not enable transmit on these channels.  
2. Prefer the **WX-CH** scan list when hunting for an active broadcast.  
3. Channel 16 is for distress and safety — not casual ragchew. Leave TX inhibited.  
4. For land weather and alerts, use official apps / websites (e.g. WeatherCAN) in addition to radio.

FRS/GMRS-style consumer frequencies are **out of scope** for this handbook and should not be used under an amateur licence as a substitute for licensed amateur channels.

---

## Chapter 7 — VE1DRR DMR basics

### Repeater facts

| Item | Value |
|---|---|
| Callsign | **VE1DRR** |
| BrandMeister device ID | **302441** |
| RX (listen) | **443.750 MHz** |
| TX (talk) | **448.750 MHz** (+5.000 MHz) |
| Color code | **1** |
| Time slot in baseline channel | **Slot 2** |
| Default TX contact in baseline | **ATL Canada** → TG **30205** |
| Network | BrandMeister |

Dashboard: [BrandMeister device 302441](https://brandmeister.network/?page=device&id=302441)

### Other digital memories often present

| Channel name | RX / TX (MHz) | CC / Slot | Default contact |
|---|---|---|---|
| VE1DRR | 443.750 / 448.750 | 1 / Slot 2 | ATL Canada |
| VE1CRA-PEI-DMR | 441.650 / 446.650 | 1 / Slot 2 | ATL Canada |
| VE1JSR-DMR | 441.800 / 446.800 | 1 / Slot 1 | ATL Canada |
| ATL CDA DMR | 446.960 / 446.960 | 1 / Slot 2 | ATL Canada (typical **hotspot** simplex) |

### Talkgroups you will use most

| TG | Name | How on this radio |
|---|---|---|
| **30205** | Atlantic Canada | Default PTT on **VE1DRR** channel |
| **3021** | Nova Scotia | Manual Dial group, or **VE1DRR-3021** if programmed |
| **302** | Canada Wide | Manual Dial group, or **VE1DRR-302** if programmed |
| **91** | Worldwide | Manual Dial group — use sparingly; **4000** when leaving |
| **4000** | Disconnect | **Group** call — un-join dynamic TGs (Chapter 8) |
| **9990** | Parrot (private) | Manual Dial **private** 9990, or **VE1DRR-Parrot** |

### Club DMR nets (TG 30205)

| When | Where |
|---|---|
| Saturday **20:00** Atlantic | TG **30205** via VE1DRR |
| Sunday **14:00** Atlantic | TG **30205** via VE1DRR |

Confirm on the Dartmouth club website if schedules change.

### First DMR contact

1. Put **your** DMR ID in the radio (Chapter 4).  
2. Select channel **VE1DRR**.  
3. Listen.  
4. Optional radio check: Manual Dial **private** `9990`, PTT, listen for parrot echo.  
5. Return to normal: on VE1DRR, PTT calls **30205** — identify and join the net or call CQ.

### BrandMeister courtesy

- When leaving a busy or wide-area TG (especially **91**), send a **group call to 4000** first (Chapter 8).  
- Do not idle forever on Worldwide (91) if it ties up a busy slot.

---

## Chapter 8 — Talkgroups on the fly (join, leave, switch)

Because the baseline parks **ATL Canada (30205)** as the channel contact, you need two skills:

1. **Join / call** another TG (Manual Dial or a dedicated channel).  
2. **Leave** a TG cleanly with BrandMeister’s drop code **4000**.

### Why “un-join” matters

On BrandMeister, when you PTT a talkgroup that is not static on the repeater, the network **links** that TG to your repeater/timeslot for a while (often on the order of **10–15 minutes** of idle time, depending on server settings).  

If you then jump to another TG **without** dropping the first one:

- You may still hear (or fight) traffic from the old TG.  
- A busy TG like **91** can make it hard to get a word in on the new one.

**Fix:** before switching, send BrandMeister’s disconnect: a short **group call to talkgroup 4000**.

| Call type | ID | What it does |
|---|---|---|
| **Group call** to **4000** | Drop dynamic / auto-static talkgroups on that path | **Use this** to un-join a TG |
| Private call to **4000** | Reflector unlink on some systems | **Not** the main TG drop for BrandMeister talkgroups |

**4000 does not remove static talkgroups** configured by the repeater trustee. It only clears **your** dynamic / auto-static links.

---

### A. Stay on 30205 (club nets — simplest)

1. Select channel **VE1DRR**.  
2. PTT → you are on **ATL Canada (30205)**.  
No dialling needed.

---

### B. Leave / un-join a talkgroup (4000) — Manual Dial

Do this when you are done with a TG, or **before** joining a different one (especially after **91**, **302**, or any busy group).

1. Stay on **VE1DRR** (same frequency, color code, and timeslot you were using).  
2. Menu → **Talk Group** → **Manual Dial**.  
3. Press **`#`** until you are in **group call** mode (not private).  
4. Enter **`4000`**.  
5. Wait for a **gap** in traffic (important on busy TGs).  
6. Hold **PTT for about 2–5 seconds**, then release.  
7. You have requested a disconnect. You should no longer be linked to the previous dynamic TG.

**If you have a dedicated “Drop / 4000” channel** (recommended — see Appendix B): select that channel and PTT briefly in a gap instead of Manual Dial.

---

### C. Join another talkgroup — Manual Dial

1. Prefer **4000 first** if you were just on a different dynamic TG (section B).  
2. Still on **VE1DRR**.  
3. Menu → **Talk Group** → **Manual Dial**.  
4. **`#`** → **group call** mode.  
5. Enter the TG number (`3021`, `302`, `91`, …).  
6. Hold **PTT** briefly to **link**, then operate normally.

Treat Manual Dial as temporary; changing memory channels may revert the TX contact to the channel default (**ATL Canada**).

---

### D. Recommended “switch TG” habit (memorize this)

```
1. Gap in traffic
2. Group call 4000  (drop)
3. Gap
4. Group call new TG  (join)
5. Identify with your callsign
```

Example: leave Worldwide, go to Atlantic:

```
Manual Dial group 4000 → PTT 2–5 s
Manual Dial group 30205 → PTT
“VE1ABC on VE1DRR, Atlantic”
```

---

### E. Contact list / dedicated channels

- **Contact List** only shows contacts already in the codeplug (baseline: mainly **ATL Canada** until expanded).  
- Best experience: add dedicated VE1DRR memories for **30205**, **3021**, **302**, **91**, **parrot 9990**, and **Drop 4000** (Appendix B + `reference/recommended-ve1drr-channels.md`). Then switching is: **Drop channel → new TG channel**.

---

### F. Parrot (not a talkgroup leave)

Radio check: Manual Dial **`#` → private** → **`9990`** → PTT → listen for echo.  
Parrot is a **private** call. Do not confuse it with **4000** (group).

---

## Chapter 9 — Private (person-to-person) DMR calls

A **private call** goes to one DMR ID, not a talkgroup.

### Method 1 — Manual Dial (usual method)

1. Select a suitable digital channel (often **VE1DRR**).  
2. Menu → **Talk Group** → **Manual Dial**.  
3. Press **`#`** for **private call** entry.  
4. Enter the other station’s DMR ID.  
5. PTT and call by callsign.

### Method 2 — Pre-programmed / CSV contacts

If contacts were loaded: **Talk Group → Contact List / CSV Contacts** → select → PTT.

### Method 3 — Call log

**Call Log** → Missed / Answered / Sent → select → PTT.

### Etiquette

Agree on repeater/slot when possible. Keep private calls short on networked repeaters.

---

## Chapter 10 — GPS and APRS (digital)

| Feature | This radio |
|---|---|
| Built-in GPS / GNSS | Yes |
| APRS via DMR SMS → BrandMeister → APRS-IS | Yes, when the RF path supports SMS |
| Classic FM AFSK APRS (e.g. 144.390) | **No** |

### Canada BrandMeister APRS target

Private upload ID: **302999**

### Setup summary

**SelfCare:** Brand = Motorola; APRS callsign `CALL-7`; icon; optional text.  

**CPS:** Enable GPS; SMS format **M-SMS**; APRS profile private to **302999**; enable APRS only on suitable digital channels (often VE1DRR); write codeplug.

### Check

Outdoors for GPS fix → VE1DRR (APRS-enabled) → wait for beacon or use an **APRS Send** key if programmed → confirm on [aprs.fi](https://aprs.fi).

---

## Chapter 11 — Troubleshooting

| Symptom | Likely cause | What to try |
|---|---|---|
| No DMR TX / wrong ID on network | Missing or leftover DMR ID | Chapter 4 |
| On VE1DRR but still hear old TG | Didn’t drop dynamic link | **Group** call **4000**, then new TG (Ch. 8) |
| On VE1DRR but “wrong” TG | Channel default is 30205 | Chapter 8 Manual Dial or TG-specific channel |
| 4000 seems to do nothing | Used private instead of group; or no gap / too short PTT | Manual Dial **group** 4000; PTT 2–5 s in a gap |
| Hear digital, can’t reply | Slot / TG / CC | Confirm Slot 2 on VE1DRR; try parrot 9990 |
| Nothing on VE1DRR | Range / antenna / CC | Move; confirm CC 1 |
| Parrot silent | Not private 9990 | Manual Dial private `9990` |
| Chinese menus | File → New used | Restore a known-good English `.data` (Read from a good radio, or a saved training codeplug) |
| CPS fail | Cable / COM | Other USB port; known-good cable |
| APRS missing | SMS / GPS / SelfCare | Chapter 10 |
| Weather channel keys up TX | TX not inhibited | Stop; do not transmit; ask an Elmer to fix the codeplug |
| VE1MTT useless | Bad RX frequency in memory | Use other VHF; ask an Elmer to fix the baseline |

### Hotspot note

Channel **ATL CDA DMR** (446.960 simplex) is a typical hotspot memory. Hotspot configuration itself is out of scope — ask an Elmer.

---

## Chapter 12 — Etiquette and good habits

1. Listen before transmit.  
2. Lowest power that works.  
3. Prefer **30205** for local/regional chat.  
4. Keep **91** brief.  
5. ID with your callsign.  
6. No encryption / disable / remote-monitor experiments on the air.  
7. Marine channels = **listen only**.  
8. Transmit DMR only with **your** RadioID programmed (Chapter 4).

---

## Appendix A — Quick reference

### VE1DRR

- **443.750** / **448.750** · **CC 1** · **Slot 2** · BM **302441**  
- Default PTT contact: **ATL Canada (30205)**  
- Nets: Sat 20:00 & Sun 14:00 Atlantic on **30205**

### Essential IDs

| ID | Type | Purpose |
|---|---|---|
| Your RadioID | Radio ID | Required before DMR TX |
| 30205 | Group | Atlantic Canada (default on VE1DRR) |
| 3021 | Group | Nova Scotia |
| 302 | Group | Canada Wide |
| 91 | Group | Worldwide |
| **4000** | **Group** | **Disconnect / drop dynamic TGs** |
| 9990 | Private | Parrot |
| 302999 | Private | Canada APRS gateway |

### Manual Dial

**Talk Group → Manual Dial → `#` private/group → number → PTT**

**Leave a TG:** group **4000** (2–5 s PTT in a gap) → then group **new TG**

### Switch habit

`4000 (drop) → new TG (join) → identify`

### CPS

**Read → Save backup → edit DMR ID only → Save As → Write** · Never **File → New**

---

## Appendix B — Working baseline channel map

Sanitized from the March 2026 working export used to build this handbook. Personal DMR IDs removed. FRS/GMRS omitted.

### Digital

| Name | RX | TX | CC | Slot | TX contact | Notes |
|---|---|---|---|---|---|---|
| ATL CDA DMR | 446.960 | 446.960 | 1 | 2 | ATL Canada | Hotspot-style simplex |
| VE1DRR | 443.750 | 448.750 | 1 | 2 | ATL Canada | Primary DMR repeater |
| VE1CRA-PEI-DMR | 441.650 | 446.650 | 1 | 2 | ATL Canada | PEI-area DMR |
| VE1JSR-DMR | 441.800 | 446.800 | 1 | 1 | ATL Canada | Slot 1 in this export |

### Analog amateur (see Chapter 6 table)

Include VE1DAR / VE1PSR / VE1HNS / VE1CDN / VE1PKT / VE1SHU / national simplex. **Repair VE1MTT** before relying on it.

### Marine / safety listen (Chapter 6A)

21B, 23B, 25B, 26, 83B, and Ch 16 — TX inhibited.

### Recommended additions to the shared baseline

Full CPS field list: [`reference/recommended-ve1drr-channels.md`](reference/recommended-ve1drr-channels.md)  
Digital menu meanings (CPS 1.45): [`CPS-1.45-Digital-Section-Walkthrough.md`](CPS-1.45-Digital-Section-Walkthrough.md)

| Add | Why |
|---|---|
| **VE1DRR-Drop** — group contact **4000** | One-knob un-join before switching TGs |
| VE1DRR channels for **30205 / 3021 / 302 / 91** | Each memory = one TG (less Manual Dial) |
| **VE1DRR-Parrot** — private **9990** | Easy radio check |
| Corrected **VE1MTT** (verify ~147.045+) | Broken RX in prior export |
| VE1MHR (~147.030), VE1ESR (~145.450) | Eastern Shore coverage |
| RX **and** TX CTCSS where required | Some memories only had decode tone set |

Always verify additions against current trustee / directory listings before writing radios.

---

## Appendix C — Suggested Halifax-region extras (not all may be in radio yet)

| Name | Approx. RX | Notes |
|---|---|---|
| VE1MTT | 147.045+ | Fix/replace bad memory |
| VE1MHR | 147.030 | Musquodoboit Harbour area |
| VE1ESR | 145.450 | Sheet Harbour area |
| VE1PSR 6 m | 53.550− (tone often 151.4) | Only if the club codeplug includes 6 m |

---

## Appendix D — Resources (operational links)

| Resource | URL |
|---|---|
| Dartmouth ARC | https://ve1yo.ca |
| Halifax ARC | https://www.halifax-arc.org |
| RadioID | https://radioid.net |
| BrandMeister | https://brandmeister.network |
| BrandMeister Canada wiki | https://wiki.brandmeister.network/index.php/Canada |
| VE1DRR dashboard | https://brandmeister.network/?page=device&id=302441 |
| aprs.fi | https://aprs.fi |
| Baofeng downloads (CPS / factory manual) | https://www.baofengradio.com/pages/download |
| WeatherCAN / ECCC notice on Weatheradio | https://www.canada.ca/en/environment-climate-change/services/weatheradio/find-your-network/nova-scotia.html |
| Canadian Coast Guard Radio Aids (marine) | https://www.canada.ca/en/canadian-coast-guard/corporate/publications/radio-aids-marine-navigation.html |

---

## Appendix E — Document control

| Version | Date | Notes |
|---|---|---|
| 0.1 | 2026-07-30 | Initial chapter draft |
| 0.2 | 2026-07-30 | Working channel map; Manual Dial emphasis; marine WX; sources annex; privacy/metadata note |
| 0.3 | 2026-07-30 | BrandMeister **group 4000** leave/join workflow; recommended VE1DRR channel set |
| 0.4 | 2026-07-31 | Renamed to Operating Manual; equipment logistics removed from docs |
| 0.5 | 2026-07-31 | Reframed as club education / training materials |

Update Appendix B whenever the shared baseline codeplug changes.

---

## Annex F — Sources and acknowledgements

This handbook is **original club training material**. It combines public technical facts, manufacturer documentation, network documentation, and a sanitized reading of a local working codeplug. It is **not** a copy of any commercial book (including Nifty Guides or third-party Amazon “complete guides”).

### Primary sources consulted

| Source | What was used |
|---|---|
| Baofeng **DM-32UV User Manual** (manufacturer PDF) | Menu concepts; Manual Dial / Contacts / private vs group call behaviour; APRS menu terminology; feature list (GPS, digital APRS via DMR SMS, no claim of FM AFSK APRS) |
| Jay Farlow, W9LW — “Programming the Baofeng DM-32UV” series (baofengradio.com blog, Parts 1–7) | CPS workflow warnings (especially avoid **File → New** / Chinese menus); BrandMeister APRS/SMS setup pattern (M-SMS + SelfCare brand); general codeplug teaching order. **Not copied verbatim**; procedures were rewritten for club training use |
| BrandMeister Canada wiki | Talkgroup numbers (302, 3021, 30205, etc.); ARS/GPS ID **302999**; VE1DRR listing (302441, 443.750, CC 1, +5 MHz) |
| BrandMeister / community DMR operating notes on TG **4000** | Disconnect is a **group call** to 4000 for dynamic talkgroups (not the same as private-call reflector unlink); static TGs are unaffected; use a gap and a firm PTT so the network registers the drop |
| BrandMeister network device page for 302441 | Cross-check of VE1DRR network presence |
| Dartmouth Amateur Radio Club website (ve1yo.ca) | VE1DRR identification; published DMR net times on TG 30205; VE1DAR analog identifiers |
| Halifax Amateur Radio Club repeater pages | VE1PSR / VE1HNS identifiers used in local analog lists |
| radioid.net | Authority for amateur DMR ID registration (process described in our own words) |
| Canadian Coast Guard *Radio Aids to Marine Navigation* / related CMB channel documentation | Marine VHF broadcast channel roles (21B, 23B, 83B, etc.) |
| Environment and Climate Change Canada Weatheradio NS page | Confirmation that Weatheradio / Hello Weather service is no longer in service |
| Public repeater directories (e.g. RepeaterBook / RadioReference community listings) | Cross-checks for metro analog frequencies and suggested additions (VE1MTT, VE1MHR, VE1ESR). **Always re-verify** before programming |
| Local working CPS channel export (March 2026) | Frequency/slot/contact layout for Appendix B. **Personal callsigns and DMR IDs stripped.** FRS/GMRS rows ignored for this handbook |

### Fair-use / originality statement

- Quoting of third-party text has been avoided in favour of paraphrased operational instructions.  
- Where a unique procedural insight originates with Farlow’s series (notably the **File → New → Chinese menus** CPS hazard and BrandMeister APRS field choices), that debt is acknowledged above; the operating narrative and regional chapters are new composition.  
- Manufacturer menu names are used as technical terms of art.  
- Club websites are cited for schedule and repeater identity facts, not reproduced as pages.

### Not used as source material

- Commercial Amazon “DM-32UV complete guide” books of unknown quality  
- Nifty Mini-Manuals (no DM-32UV edition was available; not copied)  
- Encrypted / non-amateur “tactical” programming videos

---

*Independent educational material for Halifax & Dartmouth Amateur Radio Clubs. Not affiliated with or endorsed by Baofeng, BrandMeister, or RadioID.net.*
