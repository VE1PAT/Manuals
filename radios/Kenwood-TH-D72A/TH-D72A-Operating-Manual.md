# Halifax & Dartmouth Amateur Radio Clubs  
# Kenwood TH-D72A Operating Manual

**Kenwood TH-D72A — training handbook**  
FM voice briefly; **settings, APRS, GPS, packet/Winlink, PC link, and special features in depth**

| | |
|---|---|
| **Document** | HARC / DARC Kenwood TH-D72A Operating Manual |
| **Audience** | Licensed amateurs learning the TH-D72A |
| **Assumes** | Valid Canadian amateur licence and callsign |
| **Equipment** | Kenwood TH-D72A (144/440 MHz FM HT + GPS + AX.25 TNC) |
| **Also known as** | Often listed simply as “TH-72A” |
| **Version** | 0.4 |
| **Companion** | [`topics/pc-radio-connectivity/`](../../topics/pc-radio-connectivity/) — USB/serial ideas shared by many radios |

**Scope:** Club **education** that **enhances** (does not replace) the Kenwood manuals. Analog FM is brief. Weight is on settings clarity, APRS/GPS, and **using the built-in TNC with a computer** (packet / Winlink).

### How this manual is weighted

| Topic | Depth |
|---|---|
| Analog FM voice, memories, tones | Brief — enough to get on local repeaters |
| Memory / VFO / Call / Weather channel fields | Brief — what each field *means* |
| Menu — Radio | Moderate — everyday comfort settings |
| **Menu — GPS / APRS / related tables** | **Deep** |
| **PC USB link, Packet mode, Winlink** | **Deep** (practical paths; not an OEM command dump) |
| Digipeater, EchoLink, Sky Command, MCP-4A | Deep enough for classroom use |
| Official menu encyclopaedia / full TNC command table | Kenwood CD-ROM English manual |

### Publication and privacy

- No personal author byline. Leave PDF/DOCX Author/Company metadata blank.
- Do not publish personal codeplugs, callsigns, EchoLink node numbers, or member PII in this repo.
- Settings **names** in this book follow the MCP-4A HTML export structure. Values here are teaching defaults / NA practice — not a copy of any one operator’s file.

Sources are listed in the **Annex**.

---

## How to use this book

| If you want to… | Go to |
|---|---|
| Understand how MCP-4A organizes the radio | Chapter 3 |
| Get on a local FM repeater quickly | Chapter 4 |
| Learn memory / Call / Weather / VFO fields | Chapters 5–9 |
| Everyday radio menus (display, power, lock…) | Chapter 10 |
| GPS + logging + target / mark waypoints | Chapters 11–12 |
| **APRS settings end-to-end** | **Chapters 13–15** |
| Messages, Voice Alert, IGate picture, SmartBeaconing | Chapters 14–15 |
| EchoLink / DTMF / Band Mask / Sky Command | Chapters 16–18 |
| **USB to Windows / Linux / Raspberry Pi** | **Chapter 19** |
| **Packet TNC + Winlink** | **Chapters 20–21** |
| Reset / firmware hygiene | Chapter 22 |
| Fix “I’m not beaconing” / Winlink fails | Chapter 23 |

**Critical distinction:** APRS on the TH-D72A is classic **AX.25 packet over FM** (typically **144.390 MHz** in North America). It is **not** DMR SMS APRS.

---

## Chapter 1 — What the TH-D72A is

The TH-D72A is a dual-band FM handheld with:

- Normal **VHF/UHF FM voice**
- Built-in **GPS**
- Built-in **TNC** for **APRS** and packet
- Front-panel APRS without a computer
- USB link to a PC (**MCP-4A**, GPS log export, external apps)
- Optional temporary **digipeater**
- **EchoLink** DTMF memories
- **Sky Command II** (advanced / optional)

Kenwood’s **MCP-4A** is the PC view of nearly everything this book calls a “setting.”

---

## Chapter 2 — What you need

1. TH-D72A with charged battery  
2. Dual-band HT antenna  
3. Clear sky view for GPS (outdoors)  
4. USB cable (Mini-B style) if using MCP-4A  
5. PC with **MCP-4A** (free from Kenwood)  
6. Official TH-D72A instruction manual for exact menu numbers / display icons  

---

## Chapter 3 — MCP-4A and the settings map

MCP-4A can **read** the radio and export an HTML “TH-D72 Information” report. That report’s **section headings** are the outline of this book’s settings chapters:

| MCP-4A / export heading | This manual |
|---|---|
| Memory Channel | Chapter 5 |
| Program Scan Memory | Chapter 6 |
| Call Channel | Chapter 7 |
| Weather Channel | Chapter 8 |
| VFO | Chapter 9 |
| Menu — Radio | Chapter 10 |
| Menu — Sky Command II | Chapter 18 |
| Menu — GPS | Chapter 11 |
| Target Point | Chapter 12 |
| Menu — APRS | Chapters 13–14 |
| My Position / Status Text / User Phrases / NAVITRA Message | Chapter 15 |
| DTMF Memory / EchoLink Memory | Chapter 16 |
| Band Mask | Chapter 17 |

### Safe MCP-4A habit

1. **Read** from radio  
2. **Save** a dated backup file  
3. Edit  
4. **Write** to radio only when deliberate  

Never treat an Elmer’s personal export as a shared club file — strip callsigns and private DTMF/EchoLink codes first.

### Front-panel vs MCP-4A

Most items exist in both places. MCP-4A is better for bulk memories and reviewing APRS tables; the panel is better for field changes (TNC, BCON, POS, one-off status).

---

## Chapter 4 — Analog FM (brief)

You already know most of this from other HTs:

1. Power on; set volume and squelch.  
2. Select **VFO** or a **memory**.  
3. For a repeater: receive frequency, **Shift/Offset**, and **CTCSS** (or DCS) as required.  
4. Use an appropriate power level.  
5. Identify with your callsign.

### Local practice targets (verify tones before TX)

| System | Approx. | Club |
|---|---|---|
| VE1DAR | 147.150+ / 444.600+ | Dartmouth ARC |
| VE1PSR | 147.270+ / 444.350+ | Halifax ARC |
| VE1HNS | 146.940− | Halifax ARC |
| Simplex | 146.520 / 446.000 | As appropriate |
| APRS data | **144.390** | North America FM APRS |

**Quirk:** when APRS is active, one band is the **data band**. Keep voice on the other band. Do not voice-TX on 144.390.

### TNC states (must know)

Press **[TNC]** to cycle:

| State | Meaning |
|---|---|
| **TNC Off** | Normal FM only |
| **APRS** | What you want for APRS |
| **PACKET** | Generic packet / host mode — **not** everyday APRS beaconing |

### BCON

**[BCON]** arms beacon transmit per the APRS TX Method setting. If the BCON indicator is not active, you are **not** beaconing.

---

## Chapter 5 — Memory Channel

Memories are the radio’s stored voice (and data) channels. MCP-4A shows one row per channel, often in **Groups 0–9**.

### Fields (what they mean)

| Field | Purpose |
|---|---|
| **No.** | Memory number |
| **Memory Name** | Short label shown when “Display Memory Name” is On |
| **Rx / Tx Frequency** | Receive; TX only needed when **Split** is On (odd splits) |
| **Rx / Tx Step** | Tuning step used when you leave that memory into VFO-style edits |
| **Offset** | Standard repeater offset amount (e.g. 0.60 MHz VHF, 5.00 MHz UHF in NA habit) |
| **Tone/CTCSS/DCS** | Which encode/decode family is active: Off / Tone / CTCSS / DCS / Cross |
| **Tx Cross / Rx Cross** | Cross-tone pairing when using mixed encode/decode |
| **Tone / CTCSS / DCS** | The actual tone or code values (even if currently Off — stored for later) |
| **Shift** | Simplex / Plus / Minus (classic repeater shift) |
| **Split** | Independent TX frequency (true split), not just ± offset |
| **Lockout** | Skip this channel during memory scan |
| **Mode** | Usually **FM** for amateur voice; AM appears on air-band VFO ranges |

### How to use memories in class

- Store local repeaters + national simplex + **APRS 144.390** with clear names.  
- Put APRS on a memorable early channel so students can find it quickly.  
- Use **groups** if you travel (home / EmComm / trip) — see Menu — Radio → Memory.

Analog detail (how to write a memory from the keypad): Kenwood instruction manual. No special “CPS” beyond MCP-4A.

---

## Chapter 6 — Program Scan Memory

Program-scan memories define **frequency limits** (or dedicated scan endpoints) used by program scan, not everyday repeater memories.

Same general field meanings as Memory Channel (name, RX/TX, tones, shift, mode).  

**Classroom tip:** leave this alone until someone specifically wants band-segment scanning. Wrong program-scan edges confuse “why won’t it scan my repeaters?” troubleshooting.

---

## Chapter 7 — Call Channel

One quick-access **Call** channel per band (typically 144 MHz and 440 MHz). The **Call** key jumps here.

| Use | Example |
|---|---|
| National simplex parking spot | 146.520 / 446.000 |
| Club “meet me” frequency | Whatever the class agrees |

Fields match memory channels (freq, offset, tones, shift, mode). Keep Call channels **simple** and well known — they are for speed, not a second memory bank.

Menu — Radio → Repeater → **Call Key** can change what the Call key does (Call vs other behaviours) — see Chapter 10.

---

## Chapter 8 — Weather Channel

North American **NOAA / Weatheradio**-style channels (WX 1–10 class frequencies around 162 MHz). Receive-only for weather audio.

Related settings:

- Menu — Radio → **Weather Alert** A/B-Band — enables weather-alert sampling behaviour on that band  
- Panel PF key can be assigned to **WX** for one-button access  

**Canada note:** Continuously transmitting Weatheradio services have been discontinued in many areas; treat WX as “if you can still hear a transmitter” monitoring, not a guaranteed service. Do not TX on WX frequencies.

---

## Chapter 9 — VFO

VFO is “live tuning,” not a stored memory. MCP-4A records the last VFO state per band segment.

| Field | Purpose |
|---|---|
| **VFO Band** | Which A/B segment (e.g. A:144, B:118, B:440) |
| **Rx Frequency / Step / Offset / tones / Shift / Mode** | Same ideas as memories |
| **Programmable VFO** | Allowed tune range for that segment (keeps the dial inside a band) |

**A-band vs B-band habit for APRS class:** put **144.390** on the **data band** (often A), voice repeater on the other. Confirm **Data Band** / **Packet Band** menus match that plan (Chapters 10 and 13).

---

## Chapter 10 — Menu — Radio

Everyday radio behaviour. MCP-4A groups these under **Radio (AUX)**, **Transmit/Receive**, **Memory**, **DTMF**, **Repeater**, **PF Key**, and **Lock**.

### Radio (AUX) — comfort and power management

| Setting | What it does / how to use it |
|---|---|
| **Power-on Custom Start-up Screen** / **Bitmap File** | Optional splash graphic at power-on. Fun, not required for class. |
| **Message** | Power-on text line (keep generic on shared radios — not a personal callsign billboard unless intentional). |
| **Password** | Locks radio use behind a code. Off for training radios unless theft risk warrants it. |
| **Contrast** | LCD contrast. Raise outdoors in glare; don’t max it until unreadable. |
| **Lamp Timer** | How long the backlight stays on after a keypress. Shorter = battery. |
| **Cursor Shift** | Auto-moves editing cursor after a timeout while programming. Off = you move the cursor yourself. |
| **Time Zone** | Offset from UTC for clock/GPS-related time display. Set for Atlantic (or your operating area); wrong zone makes logged times look “wrong.” |
| **GPS Logger Custom Start-up Screen** / **Bitmap** | Splash used when starting GPS logger mode — cosmetic. |
| **Beep** | Key/GPS beep policy (e.g. Radio & GPS). Turn down socially when sitting in a net. |
| **Automatic Power-off** | Shuts radio off after idle minutes. Great for battery; disastrous mid-APRS demo if students forget. Teach “APO is why it died.” |
| **Save** | Battery-saver duty cycle (receiver sleep ratio). More save = longer battery, slightly slower open-squelch reaction. |
| **Type** | Battery chemistry selection for correct gauge/charging behaviour (**match the pack** — Lithium vs Ni-MH, etc.). |
| **Scan Resume** | **Time Operate** vs **Carrier Operate** — when scanning resumes after a busy channel. |
| **Time Operate Time** | Seconds to stay on a busy channel before resume (Time Operate). |
| **Carrier Operate Time** | Delay after carrier drops before resume (Carrier Operate). |

### Radio (Transmit/Receive)

| Setting | What it does / how to use it |
|---|---|
| **Packet Band** | Which band the **packet/TNC path** uses (A or B). Must agree with where you put 144.390. |
| **VHF / UHF Band AIP** | Advanced Intercept Point / front-end toughness tradeoff. Off is common; turn On if strong nearby signals overload you (may reduce weak-signal feel). |
| **Beat Shift** | Moves internal spurious “birdies.” Change Type if a birdie sits on a favourite frequency. |
| **VOX** | Voice-operated TX. Usually **Off** on HTs in class (false triggers). |
| **VOX on Busy** | Whether VOX may key while the channel is busy. Keep Off. |
| **Gain** / **Delay Time** | VOX sensitivity and hang time — only if VOX is On. |
| **Inhibit** | TX inhibit (blocks transmit). Know this exists when “radio won’t TX.” |
| **RF Power A-Band / B-Band** | Independent power per band. Low near the repeater; High only when needed. |
| **Time-out Timer** | Max continuous TX. Protects the radio and the repeater; leave enabled. |
| **Weather Alert A/B-Band** | Weather alert check behaviour tied to that band. |
| **Scan Time** | Optional limit on how long a scan session runs. |

### Radio (Memory)

| Setting | What it does / how to use it |
|---|---|
| **Memory Recall Method** | How memories are browsed (e.g. all bands vs restricted). |
| **Group Link** | Links memory groups for scanning across groups. |
| **Display Memory Name** | Show names instead of bare frequencies — **On** for training. |
| **Group 0 … Group 9** | Labels for the ten memory groups (rename for Home / Travel / EmComm, etc.). |

### Radio (DTMF)

| Setting | What it does / how to use it |
|---|---|
| **DTMF Hold** | Keeps DTMF encoder behaviour latched while sending strings. |
| **Pause Code Time** | Duration of pause codes embedded in DTMF memories. |
| **DTMF Speed** | Milliseconds per digit — slower can help picky autopatch / EchoLink DTMF decoders. |

### Radio (Repeater)

| Setting | What it does / how to use it |
|---|---|
| **1750 Hz Transmit Hold** | European tone-burst style access — usually irrelevant in NA. |
| **Automatic Repeater Offset** | Auto-applies standard shift when you tune repeater segments. Convenient; still verify odd splits. |
| **Call Key** | What the Call key does (Call channel vs other assignments). |

### Radio (PF Key)

Programmable function keys on mic and panel (PF1–PF3 / Panel PF1). Assign shortcuts students actually need (examples: **A/B**, **VFO**, **MR**, **WX**, APRS-related jumps if offered).

**Teaching tip:** standardize PF keys on club radios so muscle memory transfers.

### Radio (Lock)

| Setting | What it does / how to use it |
|---|---|
| **Key** | Panel key lock On/Off. |
| **Type** | Which lock profile applies when Key lock is used. |
| **Mic PF Key** | Lock mic PF keys separately. |
| **DTMF Key** | Lock DTMF pad to prevent pocket beeps / accidental codes. |

---

## Chapter 11 — Menu — GPS

GPS feeds APRS positions, the **POS** display, logging, and optional NMEA output to a PC.

| Setting | What it does / how to use it |
|---|---|
| **Operating Mode** | GPS operating profile (e.g. Normal). Use Normal unless following a special Kenwood procedure. |
| **Battery Saver** | Lets the GPS sleep on a schedule to save power. **Auto** is fine for portable use; if fixes are flaky while walking slowly, try less aggressive saving. |
| **PC Output** | Streams GPS/NMEA toward the USB/serial side for mapping apps. Off unless a PC app needs it. |
| **SBAS** | Satellite-based augmentation (WAAS-class). Can improve accuracy when satellites/SBAS are visible; Off is common default. |
| **Datum** | Keep **WGS-84** unless you have a specialist mapping reason. |
| **$GPGGA / $GPGLL / $GPRMC / $GPVTG / $GPZDA / $GPGSA / $GPGSV** | Which NMEA sentence types are emitted when PC output is active. For most APRS-only use, leave defaults; enable the set your PC application documents. |
| **Record Method** | How the track logger decides to store a point: **Time**, distance, or related modes. |
| **Interval** | Seconds between log points when recording by time. |
| **Distance** | Minimum movement before logging another point (when using distance method). |
| **Wrap When Full** | If On, oldest points are overwritten when the log fills; if Off, logging stops when full. |
| **Select Target Point** / **Target Point** | Which stored target is active for bearing/distance displays — see Chapter 12. |

### Displays newcomers should know

| Idea | Why it matters |
|---|---|
| **Satellite information** | Shows how many satellites the internal GPS is using. No bars / poor geometry → poor or no fix. |
| **North Up vs Heading Up** | Map-style orientation: north fixed at top, or your travel direction at top. Pick whichever is less confusing while walking. |
| **GPS Only mode** | Radio focuses on GPS/logging with reduced “full radio” behaviour — useful for track logging to save confusion/battery; not your everyday APRS voice+data setup. |
| **Battery with GPS on** | Internal GPS draws power. Expect shorter runtime with GPS + APRS + backlight than with plain FM. GPS battery-saver helps; it can also delay fixes. |

### Field habit

- Outdoors for a fix before blaming APRS.  
- Logging ≠ beaconing: you can log a hike with BCON off.  
- Export logs with MCP-4A (KML / GPX) after exercises.

---

## Chapter 12 — Target Point and Mark Waypoint

### Target Point

Up to several named lat/lon targets (plus grid). The radio can show direction/distance toward the selected target.

| Column | Meaning |
|---|---|
| **Use** | Which target slot is active |
| **Name** | Label (trailhead, EOC, parking, etc.) |
| **Latitude / Longitude** | Target coordinates |
| **GS** | Grid square derived/associated display |

**Classroom use:** set one target to the meeting site so students see GPS navigation features without APRS TX.

### Mark Waypoint (“drop a pin”)

A **Mark Waypoint** stores *where you are right now* (or a marked position) into a waypoint list — different from a pre-planned Target Point.

| Task | Idea |
|---|---|
| Mark this spot | Use the mark-waypoint key/hold sequence in the Kenwood GPS chapter (often a long-press style **MARK** action — confirm on your firmware) |
| Navigate back | Copy a mark into a **Target Point**, then use bearing/distance |
| Export | MCP-4A can read mark waypoints with logs |

Think: **Mark** = breadcrumb you just created; **Target** = place you intentionally navigate toward.

---

## Chapter 13 — Menu — APRS (concepts + Basic / Packet / TX-RX / GPS)

This is the heart of the radio. MCP-4A’s **Menu — APRS** groups match the subsections below.

### North America frequency

Put **144.390 MHz FM** on the **Data Band**.

### APRS (Basic)

| Setting | What it does / how to use it |
|---|---|
| **Operating Mode** | **APRS** vs packet-oriented modes. Everyday position beaconing wants **APRS** (and the front-panel TNC in APRS, not Packet). |
| **My Callsign** | **Required.** Without it, the radio will not TX APRS. Include an **SSID** (see below). |
| **APRS Lock** | Limits accidental changes to APRS-critical settings while operating. Useful once configured. |
| **Speed / Altitude** | Include speed and altitude in position packets when On. |
| **Position Ambiguity** | Coarsens reported position for privacy. Off = full precision available from GPS. |
| **Method** (TX Beacon Method) | **Manual** / **PTT** / **Auto** / **SmartBeaconing**. Start Manual or Auto in class; SmartBeaconing after manners are understood. |
| **Initial Interval** | Base beacon interval for Auto (and related timing). Prefer **5–10+ minutes** for desk/slow portable — not sub-minute hammering. |
| **Decay Algorithm** | When nearly stopped, doubles intervals over time so you don’t flood the channel. Keep **On** for stationary/portable. |
| **Proportional Pathing** | Rotates path aggressiveness over time (fewer hops often, fuller path less often) to cut network load. Works with Decay; **does not apply while SmartBeaconing is selected**. |
| **Stopped / Moving [knots]** | Speed thresholds that choose Decay vs Proportional Pathing behaviour when both are enabled. |
| **Station Icon** | APRS symbol table/icon (people recognize “Kenwood” / person / bike icons). Pick something true to how you operate. |
| **Rx Beep / Tx Beep** | Audible cues for received/transmitted APRS traffic. Rx All is educational; Tx Off is less annoying in a room. |
| **Special Call** | Callsign that gets elevated alerting when it messages/appears — optional Elmer/family watch list. |

### SSID (Secondary Station Identifier)

APRS callsigns look like `VE1ABC-7`. The number after the dash is the **SSID** — it distinguishes *this radio* from your other stations (home digi, car, Winlink, etc.).

| Common habit | Typical meaning (convention, not law) |
|---|---|
| `-7` | Handheld / portable |
| `-9` | Mobile |
| `-10` | Often Winlink / gateway style (depends on service) |
| no SSID / `-0` | Often a primary home station |

Pick one SSID per radio role and **keep it stable** so aprs.fi history stays readable. Your Winlink account / packet `MYCALL` may use a different SSID than APRS — that is normal.

### First beacon checklist

1. **My Callsign** set (with SSID).  
2. Data band = **144.390**.  
3. **[TNC]** → **APRS**.  
4. GPS fix (or My Position — Chapter 15).  
5. Method + Initial Interval chosen.  
6. **[BCON]** On (indicator visible).  
7. Optional **Quick Beacon:** **[F] + [BCON]** forces a beacon when Auto/SmartBeaconing is selected (confirm on your firmware).  
8. Verify locally and/or on [aprs.fi](https://aprs.fi).

### APRS (Packet) — filters and path

These control **what you accept** and **how your packets are addressed** through digipeaters.

#### Receive filters (Position Limit + type filters)

| Setting | What it does / how to use it |
|---|---|
| **Position Limit** | Ignore stations farther than a set distance (keeps the list local). Off = no distance filter. |
| **Weather / Digipeater / Mobile / Object / NAVITRA / Others / 1-Way** | Include/exclude those packet types in what you store/display. Turning Digipeater Off hides digi stations — fine for a quiet list, bad if you are studying the network. |
| **ALTNET** | Alternate network TOCALL filtering — leave empty unless you are doing a special altnet exercise. |
| **Network** | Normally **APRS**. |

#### Path / New-N paradigm

| Setting | What it does / how to use it |
|---|---|
| **Type** | Path helper mode; **New-N Paradigm** is the modern WIDEn-N style helper. |
| **WIDE1-1** | Enables the common first-hop fill-in style path element when using the helper. |
| **RELAY / ABBR** | Legacy path aliases — usually unused in modern NA APRS. |
| **Total Hops** | How many digi hops your helper builds (often 1–2). **2** is a common portable starting point; use fewer in dense RF. |
| **Path** | Manual path override when not relying solely on the helper. |

**Manner reminder:** short paths in dense areas; never invent huge hop counts “so I’ll be heard everywhere.”

### APRS (Transmit/Receive)

| Setting | What it does / how to use it |
|---|---|
| **Data Band** | A or B — must be the band sitting on 144.390. |
| **Data Speed** | **1200** bps for normal NA FM APRS. **9600** is a different use case; also breaks Voice Alert tone demodulation. |
| **DCD Sense** | When the TNC is allowed to TX: wait for data-band clear (**D or RxD Band**), wait for both bands, or **Ignore DCD** (can collide — avoid unless you know why). |
| **Tx Delay** | Milliseconds of preamble before packet data — helps slow squelch/digi rise times. 200 ms is a common starting point; increase if digis chop your first bytes. |
| **Voice Alert** | See “Voice Alert in plain language” below. |
| **CTCSS Frequency** | Tone used for Voice Alert (Kenwood materials commonly use **100.0 Hz**). |
| **Message Group Code** | Group names your radio will accept as group-addressed messages (defaults often include ALL, QST, CQ, KWD). |
| **Bulletin Group** | Bulletin group filter/name — optional. |

### APRS (GPS) — ports and waypoints

| Setting | What it does / how to use it |
|---|---|
| **GPS Port Baud Rate** | Serial rate for external GPS I/O. |
| **GPS Port Input / Output** | External GPS in, or NMEA/waypoints out, via the GPS port path. Off for pure internal-GPS HT use. |
| **PC Output** | APRS-side PC output enable (complementary to Menu — GPS PC Output — enable only when an app needs it). |
| **Waypoint Format / Length / Output** | How received stations are emitted as GPS waypoints to an external GPS/moving-map (NMEA, character length, which stations). |
| **WX Station Tx / WX Tx Interval** | If the radio is used with weather-station style TX — advanced; Off for normal HT class. |
| **My Position Channel in Use** | Which manual My Position slot is active when not using live GPS. |
| **Target Point** (APRS GPS page) | Cross-link to target/My Position references for navigation displays. |

---

## Chapter 14 — Menu — APRS (Message, Digipeat, Display, SmartBeaconing, NAVITRA)

### Voice Alert in plain language

**Voice Alert** is an APRS-era trick: stations leave a CTCSS tone on the APRS *data* frequency so that if another Voice Alert station is **nearby** (simplex range), your radio can tip you that a human is close enough for a voice chat — without staring at the APRS list while driving.

| Fact | Detail |
|---|---|
| Needs | Voice Alert enabled; matching CTCSS (often 100.0 Hz); **1200 bps** data speed |
| Broken by | **9600 bps** packet speed (tone demodulation suffers) |
| Tone key | When APRS + Voice Alert are configured, Voice Alert appears in the **[TONE]** cycle with Tone/CTCSS/DCS |
| Club default | **Off** unless your local group actually uses it |

### Seeing other stations (list literacy)

With TNC in **APRS** on 144.390:

1. Stations appear as packets are decoded.  
2. Open a station for detail pages (position, course, path/digis, status, QSY frequency if present).  
3. **Filters** (Weather / Digipeater / Mobile / Object / …) shrink what you keep — useful when the list is noisy.  
4. **Position Limit** keeps only nearby stations.  
5. **Sort** (where offered) helps find a callsign faster.  
6. GPS quality cues on a station (Kenwood uses ideas like tracked vs last-known) tell you whether their position is fresh.

You do **not** need to understand every icon on day one — learn “open station → read distance/bearing → read status/QSY.”

### APRS messages (send / receive)

APRS messages are short RF texts to a callsign-SSID (or group names you accept).

| Step | What to do |
|---|---|
| Receive | Radio can interrupt/display a new message; store it in the message list (capacity is limited — on the order of 100). |
| Read / reply | Open the message list → Reply / Edit / New. |
| Send new | Address `CALL-SSID`, type text (or pick a **User Phrase**), transmit when the channel is clear. |
| Groups | **Message Group Code** list (e.g. ALL, QST, CQ, KWD) — messages to those names can be accepted. |
| Bulletins | Optional bulletin group feature — specialty traffic; not day-one. |
| Auto Reply | Keep **Off** unless you have a reason — unattended replies create RF noise. |

Etiquette: messaging shares 144.390 with everyone’s beacons. Keep it short.

### How you get onto aprs.fi (IGate picture)

```
Your HT (RF on 144.390)
    → heard by a digipeater and/or an IGate
        → IGate injects into APRS-IS (internet)
            → sites like aprs.fi show you
```

| You observe | Likely meaning |
|---|---|
| Hear others on RF, never see yourself online | No **IGate** heard you (or path too odd / power too low) |
| See yourself online quickly | A local IGate copied you — success |
| See yourself only after a long path | Worked, but be kind: shorten path next time |

**IGate** = a station that bridges RF APRS ↔ internet. You do not need to run one to *use* APRS.

### APRS email (optional)

Some networks support sending short email-like traffic via APRS (Kenwood in-depth docs describe email send procedures). Treat as **advanced / occasional**: easy to get addressing wrong, and it still burns RF capacity. Prefer Winlink (Chapters 20–21) for real radio email practice.

### APRS (Message) settings

| Setting | What it does / how to use it |
|---|---|
| **Position Comment** | Standard short comment field (Off Duty, En Route, In Service, etc.) baked into position packets. Pick something honest. |
| **QSY in Status** | Embeds your voice frequency into status so others can QSY to you. |
| **Tone/Narrow** / **Shift/Offset** | Whether QSY info also carries tone and shift details. |
| **Status Text Channel in Use** | Which of the Status Text slots is active. |
| **Status Text** | Points at the Status Text table (Chapter 15). **QSY needs a real status configuration** — empty/disabled status is a common “why won’t QSY work?” failure. |
| **User Phrases** | Quick canned text for messaging (Chapter 15). |
| **Reply** / **Delay Time** / **Text** / **Reply To** | Automatic reply to incoming messages. Keep **Off** unless deliberate. |

### APRS (Digipeat) — advanced

| Setting | What it does / how to use it |
|---|---|
| **Digipeat** | Master enable for the HT acting as a digipeater. **Off** unless an exercise asks for it. |
| **UIcheck Time** | Duplicate suppression window (seconds) so you don’t re-digi the same frame endlessly. |
| **UIdigi** / **Aliases** | Classic UI digipeat alias matching. |
| **UIflood** / **UIflood Alias** / **Substitution** | Flood-style digi behaviour and alias substitution (e.g. ID). Easy to misconfigure — Elmer territory. |
| **UItrace** / **UItrace Alias** | Trace-style digipeat (often temporary aliases like TEMP). |

**Training rule:** digipeater **Off** unless coordinated. An HT digi in the wrong place adds load without adding useful coverage.

### APRS (Display)

| Setting | What it does / how to use it |
|---|---|
| **Display Area** | How much of the screen APRS pop-ups may use. |
| **Interrupt Display Time** | How long a new-station interrupt stays visible. |
| **Cursor Control** | Whether the list cursor follows new activity. |
| **Speed, Distance** | Units (e.g. mi/h & mile vs metric). |
| **Altitude, Rain** | feet/inch vs metric weather units. |
| **Temperature** | °F vs °C. |
| **Grid Format** | Maidenhead vs other grid display options. |
| **Position** | Coordinate format (e.g. `dd mm.mm`). |

Set units once for the class (Canada clubs often prefer metric — match what students already use on aprs.fi).

### APRS (SmartBeaconing)

Used only when **Method = SmartBeaconing**. When SmartBeaconing is selected, **Initial Interval / Decay / Proportional Pathing no longer govern** TX timing the same way — SmartBeaconing takes over.

| Setting | What it does / how to use it |
|---|---|
| **Low Speed** | Below this, beacons at **Slow Rate**. Set high enough that GPS jitter while standing still does not look like “motion.” |
| **High Speed** | Above this, beacons at **Fast Rate**. |
| **Slow Rate** | Interval when crawling/stopped (minutes). |
| **Fast Rate** | Interval when moving fast (seconds). Don’t set absurdly short in a crowded RF area. |
| **Turn Angle** | Minimum course change to trigger a corner-peg beacon. |
| **Turn Slope** | Makes corner pegging more sensitive at lower speeds (Kenwood units: 10°/speed style scaling). |
| **Turn Time** | Minimum time between corner-peg beacons. |

**Practice:** demo SmartBeaconing on a drive; return Method to Auto/Manual afterward if the radio will sit on a desk.

### What is NAVITRA?

**NAVITRA** is a **Japanese** position/messaging system that also uses packet-like beacons. Kenwood included NAVITRA menus so the same radio hardware can serve that market.

| For HARC / DARC | Guidance |
|---|---|
| Do we use it in Nova Scotia? | **No** — local practice is **APRS** on **144.390** |
| Why are the menus there? | Shared firmware with TH-D72E / global product line |
| What should students do? | Leave NAVITRA settings alone; ignore NAVITRA Message slots |
| If the radio says NAVITRA | You pressed **[TNC]** into the wrong personality — get back to **APRS** (or Packet when doing Winlink) |

NAVITRA is **not** “APRS with another name,” and it is **not** required for Canadian operation.

---

## Chapter 15 — My Position, Status Text, User Phrases, NAVITRA Message

These MCP-4A tables back the APRS Message/GPS menus.

### My Position

Manual lat/lon (and grid) slots used when GPS is unavailable or you intentionally beacon a fixed position (classroom, tent, EOC).

| Column | Meaning |
|---|---|
| **Use** | Active slot |
| **Name** | Label |
| **Latitude / Longitude / GS** | Fixed position |

**Quirk:** Indoors with no GPS fix, set My Position or you will not get useful posits.

### Status Text

| Column | Meaning |
|---|---|
| **Use** | Active status slot |
| **Message** | Status string (length-limited — on the order of 40+ characters) |
| **Tx Rate** | How often status is attached/sent (Off = don’t send that status) |

Use short, useful text (“HARC demo”, “QSY 146.520”, event names). Enable a Tx Rate if you want the world to see it.

### User Phrases

Canned phrases for composing APRS messages quickly (short strings). Pre-load class-useful phrases (“QRZ?”, “QSY voice”, “At site”) without typing on the keypad in the cold.

### NAVITRA Message

Message slots for NAVITRA — skip for NA club work.

---

## Chapter 16 — DTMF Memory and EchoLink Memory

### DTMF Memory

Ten general DTMF memories (name + code) for autopatch, controller commands, or other DTMF sequences. Speed/pause come from Menu — Radio → DTMF.

### EchoLink Memory

Ten EchoLink-oriented DTMF memories (name/callsign + code). Typical contents are node numbers and control codes (connect/disconnect patterns).

| Reality check | |
|---|---|
| The HT stores **DTMF** | It does **not** create an internet EchoLink gateway by itself |
| You still need | An on-air EchoLink-ready repeater/link and permission/manner |

MCP-4A is the sane way to edit these. Do not publish personal node lists with private access codes in shared manuals.

---

## Chapter 17 — Band Mask

Enables or masks which band segments appear on A (upper) and B (lower):

- A: 144 / 440  
- B: 118 / 144 / 300 / 440  

**Use:** Hide segments you never use to simplify band switching in class.  
**Caution:** Masking 144 on the data band’s side is a great way to “lose” APRS — don’t.

---

## Chapter 18 — Sky Command II and wireless remote (brief)

### Sky Command II

| Setting | What it does / how to use it |
|---|---|
| **Commander Callsign** | Handheld commander identity |
| **Transporter Callsign** | HF transporter / base identity |
| **Tone Frequency** | CTCSS on the Sky Command link |

Remotes a compatible Kenwood HF setup. **Skip until HF mentoring is available.**

### Wireless operation (TH-D72A)

The Americas model can act as a **wireless remote** for certain Kenwood mobiles (OEM “Wireless Operation” chapter). Specialty topic — not required for APRS or Winlink class. Leave off unless an Elmer is teaching that specific pair of radios.

---

## Chapter 19 — Connecting the TH-D72A to a computer

Cross-radio overview: [`topics/pc-radio-connectivity/`](../../topics/pc-radio-connectivity/). This chapter is the **TH-D72A** path.

### What the USB cable is for

| Use | TNC / mode | Typical software |
|---|---|---|
| Program memories / APRS menus | Radio on; MCP-4A talking “radio control” | **MCP-4A** (Windows) |
| Export GPS logs / waypoints | MCP-4A | MCP-4A → KML/GPX |
| **Packet / Winlink / keyboard TNC** | **[TNC] → PACKET** | Winlink Express, Pat, terminal, AX.25 stack |
| Live NMEA to a map app | GPS/APRS PC output menus On | Mapping app that reads NMEA |

Same mini-USB cable; **different software jobs**. Do not expect MCP-4A and a packet program to own the COM port at the same time.

### Driver (Virtual COM Port)

Kenwood documents a **virtual COM port** driver so Windows sees the radio as `COMx`. On many systems this is a Silicon Labs **CP210x**-class USB-serial device (Kenwood’s package name may say “Virtual COM Port”).

| Platform | What you do |
|---|---|
| **Windows** | Install Kenwood’s VCP / CP210x package if Device Manager shows an unknown USB device. Note the **COM port number**. |
| **Linux** | Often appears as `/dev/ttyUSB0` (or similar) via the `cp210x` kernel driver — no Kenwood GUI required. Check `dmesg` after plug-in. Add your user to the `dialout` group (or equivalent) so you can open the port. |
| **Raspberry Pi** | Same as Linux. Prefer a known-good powered USB path; flaky hubs cause mystery disconnects. |

**Baud note:** In **PACKET** mode the PC↔radio USB link is commonly **9600 bps** (serial line rate). That is *not* the same number as on-air **1200 / 9600** HBAUD — see Chapter 20.

### MCP-4A newcomer path (Windows)

1. Install VCP driver if needed.  
2. Install **MCP-4A**.  
3. Power radio → plug USB → select COM port in MCP-4A.  
4. **Read** from radio → **Save** a dated backup → edit → **Write** only when intentional.  
5. GPS log: read log → export **KML** / **GPX** for Google Earth / GIS viewers.

MCP-4A is the comfortable tool for memories and APRS tables. Packet/Winlink use other programs (Chapters 20–21).

### Linux / Pi without MCP-4A

You can still:

- Use the serial device for **packet / Pat / kissattach** (Chapter 21)  
- Use community tools that speak Kenwood protocols (advanced)  
- Keep a Windows VM or club laptop for MCP-4A backups if you do not want to fight wine/VMs on day one  

---

## Chapter 20 — Packet mode and the built-in TNC

### APRS mode vs Packet mode (do not confuse them)

| Front-panel TNC state | Job |
|---|---|
| **APRS** | On-radio APRS beacons, list, messages |
| **PACKET** | Built-in TNC for a **computer** (or keyboard terminal) — BBSs, nodes, **Winlink**, experiments |
| **Off** | Plain FM |

For Winlink / classic packet: **[TNC]** until the display shows **PACKET** (often with **12** or **96** to hint 1200 vs 9600 on-air).

### What “TNC command list” means

Kenwood’s CD-ROM manual includes a long **TNC COMMANDS LIST** (`MYCALL`, `KISS`, `HBAUD`, `CONNECT`, …). That is a **reference dump** for the `cmd:` style TNC — useful when you open a serial terminal to the radio.

This club book does **not** reprint that encyclopedia. You need:

| Command / idea | Why |
|---|---|
| **MYCALL** | Your callsign-SSID for packet connects (also tied to Menu My Callsign behaviour) |
| **HBAUD 1200** or **9600** | On-air modem speed — must match the gateway |
| **KISS ON** + **RESTART** | Enter **KISS** framing so Linux AX.25 / many apps can drive the TNC |
| **CONNECT** / `c CALL-SSID` | Manual connect from a terminal (learning / debugging) |
| Software flow control | Often required for reliable KISS (tools such as `tmd710_tncsetup -s` on Linux) |

Everything else on the OEM list is “look up when an Elmer says so.”

**Quirk:** Many Packet-mode TNC settings **reset when you power-cycle** (Kenwood notes limited backup). Expect to re-apply KISS / setup scripts after power-off. My Callsign / clock are the usual survivors.

### On-air 1200 vs 9600

| On-air speed | When |
|---|---|
| **1200 baud** (`packet12`) | Most VHF packet / many Winlink gateways; default APRS world |
| **9600 baud** (`packet96`) | Only if the *gateway* and your path support it; needs strong signal |

Match the published RMS / node speed. Wrong speed = you TX into silence.

### Data band / frequency

1. Set **Packet Band** / **Data Band** to the band you will use.  
2. Tune that band to the **packet or Winlink gateway frequency** (not 144.390 unless that gateway really is there).  
3. Store a memory (e.g. label `WinlinkV` / `PacketU`) once you know the local channel.  

Ask club Elmers for current Nova Scotia / Maritime gateway frequencies — they change; this manual does not hard-code a living list.

### Manual terminal smoke test (any OS)

1. USB connected; VCP/tty visible.  
2. Radio → **PACKET**, correct frequency, 1200 unless told otherwise.  
3. Open a serial terminal at **9600** 8N1 on that port (PuTTY, `picocom`, `minicom`, …).  
4. Wake to `cmd:` prompt (may need Enter).  
5. Check/set `MYCALL`, try a `CONNECT` to a known node if one is reachable.  

If this fails, fix cables/drivers/mode before blaming Winlink software.

---

## Chapter 21 — Winlink with the TH-D72A

**Winlink** is radio email (and forms) via RMS gateways. The TH-D72A’s built-in TNC can do **packet Winlink** when a gateway is in range.

### What you need

1. Winlink account / callsign authorization (winlink.org process).  
2. TH-D72A + charged battery + decent antenna.  
3. USB cable + working COM/`tty` (Chapter 19).  
4. Known **RMS gateway** frequency, SSID (often `-10`), and baud.  
5. Software below.

### Windows — Winlink Express (typical club path)

1. Install VCP driver; note COM port.  
2. Install **Winlink Express**.  
3. Radio: **PACKET**, data band on gateway frequency, **1200 or 9600** to match the RMS.  
4. In Express, configure a **Packet Winlink** session using the Kenwood / KISS-style TNC options appropriate to the D72 (select the COM port; follow current Express UI labels — they evolve).  
5. Start session → connect to `GATEWAY-10` (example form) → send a test message to yourself.

Club tip: practice once at a meeting where an Elmer can hear whether you are keying and whether the gateway answers.

### Linux / Raspberry Pi — Pat + AX.25 (typical)

Community-proven pattern for the D72:

1. Radio USB → `/dev/ttyUSBx`.  
2. Radio in **PACKET** / **packet12** (for 1200-baud gateways).  
3. Use a Kenwood KISS setup helper (commonly **`tmd710_tncsetup`**, shared with TM-D710-class TNCs): set band, **HBAUD 1200**, enable **software flow control**.  
4. `kissattach` / AX.25 ports (`/etc/ax25/axports`) — note the usual gotcha: **serial line speed 9600** vs **on-air HBAUD 1200** are different settings.  
5. Run **Pat** with an `ax25://…/CALL-10` connect alias to your RMS.

Pi note: same stack as Linux; keep power solid. For class demos, a laptop running Express may be less fragile than a first-time Pat install.

### Winlink vs APRS on this radio

| | APRS | Winlink packet |
|---|---|---|
| TNC key | **APRS** | **PACKET** |
| Typical frequency | 144.390 (NA) | Published RMS channel |
| Goal | Positions / short messages | Email / forms via RMS |
| PC required? | No for basic use | Yes for Express / Pat |

You generally **cannot** usefully run full APRS beaconing personality and a Winlink KISS session as one brain at the same time — pick a job, set the TNC mode, finish, then switch back.

### Etiquette

- Leave the channel once your traffic finishes.  
- Don’t camp a gateway for practice during an emergency net.  
- Identify; use your own callsign-SSID.

---

## Chapter 22 — Reset and firmware (hygiene)

### Reset

Kenwood offers reset styles (key combo vs menu). Know before you use them:

| Risk | What you can lose |
|---|---|
| Partial / menu resets | Selected settings |
| Full transceiver reset | Memories, APRS config, almost everything |

**Training habit:** MCP-4A backup **before** any reset. After reset, reload the club or student file.

### Firmware

1. Read the version on the radio and/or in MCP-4A (**Transceiver Information**).  
2. Download firmware only from **Kenwood’s official** update path.  
3. Follow their steps exactly (battery charged, cable solid, do not interrupt).  

Club radios: note the version on a label or inventory sheet after updates.

---

## Chapter 23 — Troubleshooting

| Symptom | Likely cause | What to try |
|---|---|---|
| No APRS TX | My Callsign empty | Set My Callsign + SSID |
| No APRS TX | TNC Off or Packet | **[TNC]** → **APRS** |
| No APRS TX | BCON not armed | **[BCON]** until indicator shows |
| No APRS TX / odd posits | No GPS fix | Go outside; or set My Position |
| Hear nothing on APRS | Wrong frequency / data band | **144.390** on Data Band |
| Hear others, not on aprs.fi | No IGate heard you | Move; check path; ask locals |
| Voice Alert “broken” | Data speed 9600 | Use **1200** for Voice Alert |
| QSY info missing | Status empty / Tx Rate Off | Configure Status Text + QSY in Status |
| PC does not see radio | Driver / cable / port busy | VCP install; close MCP-4A; try other USB port |
| Packet terminal dead | Not in PACKET mode / wrong baud | PACKET + 9600 8N1 on USB |
| Winlink no connect | Wrong freq/baud/SSID / not KISS | Match RMS; KISS setup; strong signal |
| Winlink flaky | Flow control / power / antenna | Enable software flow control; better antenna |
| KISS settings vanished | Power cycle cleared TNC RAM | Re-run setup script / re-enter KISS |
| Digi mystery traffic | Digipeat left On | Turn Digipeat Off |
| Radio dies in class | APO | Lengthen/disable APO while training |

---

## Chapter 24 — Suggested training path

1. **Analog:** one repeater memory + simplex (Chapters 4–5).  
2. **Tour MCP-4A headings** (Chapter 3) + USB driver on one PC (Chapter 19).  
3. **APRS receive only** → station list literacy (Chapter 14).  
4. **First beacon** → aprs.fi / IGate picture (Chapters 13–14).  
5. **Manners:** interval, Decay, path.  
6. **Status / messages / QSY** (optional Voice Alert if locals use it).  
7. **Packet terminal smoke test** (Chapter 20).  
8. **Winlink** to a local RMS with Express or Pat (Chapter 21).  
9. **Optional:** SmartBeaconing drive, GPS log export, digipeater drill.  

---

## Appendix A — Quick reference card

### APRS bring-up (NA)

```
My Callsign-SSID  →  144.390 on Data Band
TNC → APRS  →  GPS fix (or My Position)
Method + Initial Interval  →  BCON ON
Optional: F + BCON quick beacon
Verify aprs.fi / local decode
```

### Packet / Winlink bring-up

```
USB → COM/tty working
TNC → PACKET (packet12 or packet96 to match RMS)
Data band on gateway frequency
Windows: Winlink Express  |  Linux/Pi: KISS setup + Pat
```

### Keys

| Key | Role |
|---|---|
| **TNC** | Off / APRS / Packet |
| **BCON** | Arm beaconing / with F: quick beacon |
| **POS** | Position display |
| **PTT** | Voice — keep off the data band |

### Settings map (MCP-4A order)

Memory → Program Scan → Call → Weather → VFO → Menu Radio → Sky Command → Menu GPS → Target Point → Menu APRS → My Position → Status Text → User Phrases → NAVITRA → DTMF → EchoLink → Band Mask

---

## Appendix B — Document control

| Version | Date | Notes |
|---|---|---|
| 0.1 | 2026-07-31 | Scaffold |
| 0.2 | 2026-07-31 | Light analog, deep APRS narrative |
| 0.3 | 2026-07-31 | MCP-4A settings headings |
| 0.4 | 2026-07-31 | Voice Alert/list/messages/IGate; GPS marks; PC USB; Packet/Winlink; NAVITRA explained; reset/firmware |

Menu numbers in the field may be confirmed against the Kenwood instruction manual for your firmware; this book prefers **setting names** (as in MCP-4A) so wording stays stable across docs.

---

## Annex — Sources and acknowledgements

Original HARC/DARC training narrative. Enhances, does not replace, Kenwood OEM manuals.

| Source | Use |
|---|---|
| Kenwood TH-D72A Instruction Manual (CD-ROM English) | Menus, PACKET mode, TNC command reference |
| Kenwood TH-D72A/E APRS In-Depth Manual | Decay, Proportional Pathing, SmartBeaconing, QSY, Voice Alert, IGate, MCP-4A, firmware |
| Kenwood MCP-4A + VCP driver materials | PC programming / GPS export |
| Community Pat + TH-D72A AX.25 write-ups | Linux/Pi KISS / `tmd710_tncsetup` patterns (paraphrased) |
| SSIARS practical TH-D72A notes | BCON/TNC field quirks (paraphrased) |
| aprs.fi / Winlink org practice | Verification concepts |

*Independent educational material for Halifax & Dartmouth Amateur Radio Clubs. Not affiliated with or endorsed by JVCKENWOOD / Kenwood / Winlink.*
