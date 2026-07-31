# Halifax & Dartmouth Amateur Radio Clubs  
# Kenwood TH-D72A Operating Manual

**Kenwood TH-D72A — training handbook**  
FM voice briefly; **APRS, GPS, TNC, and special features in depth**

| | |
|---|---|
| **Document** | HARC / DARC Kenwood TH-D72A Operating Manual |
| **Audience** | Licensed amateurs learning the TH-D72A |
| **Assumes** | Valid Canadian amateur licence and callsign |
| **Equipment** | Kenwood TH-D72A (144/440 MHz FM HT + GPS + AX.25 TNC) |
| **Also known as** | Often listed simply as “TH-72A” |
| **Version** | 0.2 |

**Scope:** Club **education**. Analog FM is covered for completeness but kept light. The educational weight is on **APRS and related special features** — where most new TH-D72A operators get stuck.

### How this manual is weighted

| Topic | Depth |
|---|---|
| Analog FM voice, memories, tones | Brief — enough to get on local repeaters |
| Dual-band A/B receive | Moderate — needed for APRS + voice |
| **APRS / GPS / TNC / beacons / messaging** | **Deep** |
| Digipeater, EchoLink memories, MCP-4A, Sky Command | Deep enough for classroom use |
| Full menu encyclopaedia | Use the official Kenwood instruction manual |

### Publication and privacy

- No personal author byline. Leave PDF/DOCX Author/Company metadata blank.
- Do not publish personal codeplugs or member PII in this repo.

Sources are listed in the **Annex**.

---

## How to use this book

| If you want to… | Go to |
|---|---|
| Get on a local FM repeater quickly | Chapter 3 |
| Understand A/B bands + data band | Chapter 4 |
| **First working APRS beacon** | **Chapters 5–7** |
| Messages, QSY, SmartBeaconing | Chapters 8–9 |
| Digipeater / Packet / EchoLink / MCP-4A | Chapters 10–12 |
| Fix “I’m not beaconing” | Chapter 13 |

**Critical distinction:** APRS on the TH-D72A is classic **AX.25 packet over FM** (typically **144.390 MHz** in North America). It is **not** DMR SMS APRS (as on some Baofeng DMR HTs).

---

## Chapter 1 — What the TH-D72A is

The TH-D72A is a dual-band FM handheld with:

- Normal **VHF/UHF FM voice** (like many dual-band HTs)
- Built-in **GPS**
- Built-in **TNC** (Terminal Node Controller) for **APRS** and packet
- Front-panel **APRS** operation without a computer
- Optional **USB** link to a PC (MCP-4A, GPS log export, external APRS apps)
- Can act as a temporary **digipeater**
- **EchoLink** DTMF memories
- **Sky Command II** (advanced / optional module)

Kenwood’s MCP-4A software manages memories and many APRS settings from a PC.

---

## Chapter 2 — What you need

1. TH-D72A with charged battery (and spare if possible)  
2. Stock or dual-band HT antenna  
3. Clear view of the sky for GPS (outdoors)  
4. USB cable (supplied Mini-B style) if using MCP-4A  
5. PC with **MCP-4A** (free from Kenwood) for backup / bulk edit  
6. Official TH-D72A instruction manual as the menu encyclopaedia  

---

## Chapter 3 — Analog FM (brief)

You already know most of this from other HTs. On the TH-D72A:

1. Power on; set volume and squelch.  
2. Select **VFO** or a **memory** channel.  
3. For a repeater: set receive frequency, **offset**, and **CTCSS encode** (tone) as required.  
4. Use an appropriate power level (Low when close).  
5. Identify with your callsign.

### Local practice targets (verify tones before TX)

| System | Approx. | Club |
|---|---|---|
| VE1DAR | 147.150+ / 444.600+ | Dartmouth ARC |
| VE1PSR | 147.270+ / 444.350+ | Halifax ARC |
| VE1HNS | 146.940− | Halifax ARC |
| Simplex | 146.520 / 446.000 | As appropriate |

**Quirk to remember later:** when APRS is active, one band is often reserved as the **data band**. Voice may live on the other band (Chapter 4). Do not accidentally voice-TX on 144.390.

Menu entry of memories, scan, and CTCSS details: see the Kenwood manual. No special “UV-5R style” CPS — use the panel or **MCP-4A**.

---

## Chapter 4 — Dual band, TNC modes, and the data band

### A and B bands

The TH-D72A can receive on two frequencies (including same-band dual receive). Mentally assign:

| Role | Typical classroom setup (NA) |
|---|---|
| **Data / APRS band** | **144.390 MHz** FM |
| **Voice band** | Local repeater or simplex on the other band (often UHF or another VHF channel) |

### TNC key — three states that confuse everyone

Press **[TNC]** to cycle modes. You must know which state you are in:

| State (conceptually) | What it means |
|---|---|
| **TNC Off** | Normal FM radio only — no APRS decode/TX |
| **APRS** | TNC running APRS protocol — **this is what you want for APRS** |
| **PACKET** | Generic packet mode — **not** the same as APRS beaconing |

**Quirk:** If the TNC is Off or in Packet mode, you will not get normal APRS behaviour. Look for the APRS/TNC indicators on the display (often a **D** / APRS indication after the frequency — confirm on your firmware’s display legend in the official manual).

### BCON key

**[BCON]** arms beacon transmit according to Menu **3D0** method (Manual / PTT / Auto / SmartBeaconing).  

**Quirk (very common):** If **BCON** is not shown as active on the display, you are **not** beaconing — even if GPS has a fix and you are on 144.390. Toggle BCON and verify the indicator.

---

## Chapter 5 — APRS essentials (concepts)

### What APRS does here

- Sends your **position** (and often speed/course/altitude) as AX.25 UI frames  
- Receives others’ positions and **messages**  
- Can show digipeater path info  
- Can advertise voice **QSY** frequency info in status (optional)  
- Relays via digipeaters / IGates to APRS-IS (then visible on sites such as aprs.fi)

### North America frequency

| Region | Common APRS FM frequency |
|---|---|
| **North America** | **144.390 MHz** |
| Europe (FYI) | 144.800 MHz |

Canada classroom default: put **144.390** on the data band.

### My Callsign (required)

Without **My Callsign**, the radio **will not transmit** APRS packets.

- Menu **300** — program your callsign (with optional **SSID**)  
- Handheld convention often uses SSID **`-7`** (example: `VE1ABC-7`)  
- Use a consistent SSID so aprs.fi history stays readable  

### Position source

| Menu / control | Purpose |
|---|---|
| Internal GPS | Usual portable choice — go outdoors for a fix |
| Menu **331** (Input Type / related GPS menus) | Choose GPS vs other inputs |
| Menu **360** My Position | Manual fixed position if GPS Off / indoor demo |
| **[POS]** | View position |

**Quirk:** Indoors, GPS may never fix. For classroom demos without sky view, set a manual My Position — or step outside.

---

## Chapter 6 — First successful beacon (checklist)

Do these in order:

1. **Menu 300** — My Callsign set (with SSID).  
2. Data band frequency = **144.390** (NA).  
3. **[TNC]** until you are in **APRS** mode (not Off, not Packet).  
4. GPS On; wait for a fix outdoors (or set My Position).  
5. Menu **3D0** — TX Beacon Method:  
   - Start with **Manual** or **Auto** for learning  
   - Use **SmartBeaconing** after you understand rates  
6. Menu **3D1** — Initial Interval: for a desk/slow walk, prefer **5–10 minutes** (or longer), not 0.2–1 minute, unless temporarily testing.  
7. Press **[BCON]** so beaconing is **On** (indicator visible).  
8. Force a beacon if needed (method-dependent: Manual press, or **[F]+[BCON]** quick beacon when Auto/Smart is selected — see manual).  
9. Confirm:  
   - Local decode of your own packet (sometimes via digi bounce shows “My Position”), and/or  
   - Your call-SSID on [aprs.fi](https://aprs.fi) after an IGate hears you  

### Path (digipeater path)

Menu group for packet path (often discussed as **3H0** / path menus in Kenwood docs):

| Habit | Recommendation |
|---|---|
| Dense urban / good IGate | Short path — often **`WIDE1-1`** only, or local guidance |
| Sparse area | Sometimes **`WIDE1-1,WIDE2-1`** |
| Never | Huge hop counts that flood the network |

Follow current local APRS etiquette; paths are a social convention as much as a technical setting.

---

## Chapter 7 — Beacon methods and network manners

### Menu 3D0 methods

| Method | Behaviour (summary) |
|---|---|
| **Manual** | You press BCON (or equivalent) each time you want a posit |
| **PTT** | Beacon tied to PTT-related behaviour (see manual) |
| **Auto** | Beacons on Initial Interval while BCON is on |
| **SmartBeaconing** | Rate rises with speed; corner pegging on turns |

### Decay algorithm (Menu 3E0 area)

When you are **stationary**, decay can stretch the interval (1 → 2 → 4 → … minutes) so you do not hammer 144.390. Keep it enabled for portable/stationary use unless you have a reason not to.

### SmartBeaconing tips (from field practice)

- Do not set the “slow speed” threshold so low that GPS jitter while standing still looks like motion (unnecessary beacons).  
- Highway use: SmartBeaconing shines; still avoid absurdly short minimum intervals in crowded RF areas.  
- After testing, return to neighbour-friendly rates.

---

## Chapter 8 — Receiving stations, lists, and messages

### Seeing others

With TNC in APRS mode on 144.390, stations appear as they are received. Browse the station list / detail pages (Kenwood provides multiple information pages per station, including digipeater path).

### APRS messages

- The TH-D72A can send/receive short APRS messages (stored message capacity is limited — on the order of **100** messages, length limits apply).  
- Status texts and user phrases are separate editable strings (status length on the order of **42** characters; user phrases shorter).  
- Special-call / notification features can alert you when a designated station messages you.

Use messaging sparingly on RF; it shares the APRS channel.

### QSY (frequency) in status

Optional feature: advertise the voice frequency you are using so others can QSY to you.

**Quirk:** QSY info is tied to **status text** configuration. If status TX is disabled / empty, QSY-in-status will not do what you expect. Enable status text, enter text, set status TX rate, then enable QSY-related menus (**3A0** area: QSY in status, tone/narrow, shift/offset as desired).

---

## Chapter 9 — GPS logging

The TH-D72A can log track points (capacity on the order of **thousands** of points — Kenwood cites up to about **5,000**). Log interval can follow time, distance, or beacon events.

Export via **MCP-4A** to formats such as **KML** for mapping on a PC.

Classroom tip: logging is separate from APRS TX. You can log without beaconing aggressively.

---

## Chapter 10 — Digipeater mode (advanced)

The TH-D72A can digipeat (relay) packets — useful in exercises or temporary coverage gaps.

| Topic | Guidance |
|---|---|
| Enable | Digipeat menus (e.g. **3K0** / UI digipeat / aliases — see official manual) |
| When to use | Coordinated events, EmComm drills, sparse areas — **not** as an always-on urban digi without a plan |
| Risk | Extra hops increase channel load |
| Alias | Configure aliases carefully so you do not unintentionally relay everything |

**Training rule:** Leave digipeater **Off** unless an Elmer asks you to enable it for a specific exercise.

---

## Chapter 11 — Packet mode, PC TNC, IGate (overview)

| Mode | Use |
|---|---|
| APRS (on-radio) | Everyday position/messaging |
| PACKET | Host-mode / PC programs talking to the internal TNC over USB |
| IGate | Possible with suitable PC software + internet — **advanced**; not a first-day topic |

USB port / PC output menus (e.g. around **350**) control what leaves the radio toward the computer. Enable only when needed; lock panels if you bump keys in the field.

---

## Chapter 12 — EchoLink memories, Sky Command, MCP-4A

### EchoLink DTMF memories

- About **10** dedicated EchoLink DTMF memories  
- Store node numbers / commands; MCP-4A can manage them  
- Still need an EchoLink-ready repeater/node on the air — the radio alone is not an internet gateway  

### Sky Command II

Allows linking a compatible Kenwood HF setup with the handheld as a commander (advanced HF remote topic). Skip until HF mentoring is available.

### MCP-4A (do use this)

| Task | Why |
|---|---|
| Backup memories + APRS settings | Recover from menu experiments |
| Edit many memories | Faster than keypad |
| Manage EchoLink memories | Less typing |
| Export GPS logs | After field exercises |
| TravelPlus import (where used) | Trip memory builds |

Always **read from radio → save file → edit → write** carefully. Keep dated backups.

---

## Chapter 13 — Troubleshooting

| Symptom | Likely cause | What to try |
|---|---|---|
| No APRS TX | My Callsign empty | Menu **300** |
| No APRS TX | TNC Off or Packet mode | **[TNC]** → **APRS** |
| No APRS TX | BCON not armed | **[BCON]** until indicator shows |
| No APRS TX / weird posits | No GPS fix | Go outside; or set My Position |
| Hear nothing on APRS | Wrong frequency | **144.390** (NA) on data band |
| Hear others, not on aprs.fi | No local IGate heard you | Move; check path; ask locals |
| Beaconing too often | Interval / SmartBeaconing too aggressive | Lengthen interval; enable decay |
| Voice on 144.390 by mistake | Talking on data band | Move voice to the other band |
| Dual things “broken” | Locked keys / wrong band focus | Check lock; which band is TX |

---

## Chapter 14 — Suggested training path

1. **Day A — Analog only:** one repeater memory, one simplex contact (Chapter 3).  
2. **Day B — APRS receive:** 144.390, TNC APRS, watch stations (no TX).  
3. **Day C — First beacon:** Chapters 5–6; confirm on aprs.fi.  
4. **Day D — Manners:** intervals, decay, path (Chapter 7).  
5. **Day E — Messages / QSY** (Chapter 8).  
6. **Optional:** digipeater drill, MCP-4A backup, GPS log export.  

---

## Appendix A — Quick reference card

### APRS bring-up (NA)

```
My Callsign (Menu 300)  →  144.390 on data band
TNC → APRS  →  GPS fix (or My Position)
Beacon method (3D0) + interval (3D1)
BCON ON (indicator visible)  →  verify aprs.fi
```

### Keys to memorize

| Key | Role |
|---|---|
| **TNC** | Off / APRS / Packet |
| **BCON** | Beacon arm / method actions |
| **POS** | Position display |
| **PTT** | Voice (keep off 144.390 when APRS data band is selected for TX) |

### Local voice memories (fill in your training codeplug)

| Label | Freq / tone | Notes |
|---|---|---|
| VE1DAR-V | 147.150+ | |
| VE1PSR-V | 147.270+ | |
| VE1HNS-V | 146.940− | |
| APRS | 144.390 | Data band |

---

## Appendix B — Document control

| Version | Date | Notes |
|---|---|---|
| 0.1 | 2026-07-31 | Scaffold |
| 0.2 | 2026-07-31 | Full education draft: light analog, deep APRS/special features |

Menu numbers follow common TH-D72A/E documentation; if your firmware labels differ slightly, match by function name (My Callsign, TX Beacon Method, etc.).

---

## Annex — Sources and acknowledgements

Original HARC/DARC training narrative. Not a copy of Nifty or third-party commercial guides.

| Source | Use |
|---|---|
| Kenwood TH-D72A Instruction Manual | Authoritative menus and specifications |
| Kenwood TH-D72A/E APRS / product primers (Kenwood PDF materials) | APRS feature overview, regional frequency table, MCP-4A roles |
| Kenwood MCP-4A documentation | PC programming / GPS export |
| SSIARS “Tips on using a TH-D72A” (ssiarc.ca) | Practical BCON/TNC quirks and SmartBeaconing field advice (paraphrased) |
| Community APRS best-practice notes for TH-D72A | QSY/status interdependency; path manners |
| aprs.fi / APRS network practice | Verification of beacons via IGate |

*Independent educational material for Halifax & Dartmouth Amateur Radio Clubs. Not affiliated with or endorsed by JVCKENWOOD / Kenwood.*
