# Halifax & Dartmouth Amateur Radio Clubs  
# Kenwood TH-D72A Operating Manual

**Kenwood TH-D72A — training handbook**  
FM voice briefly; **settings, APRS, GPS, TNC, and special features in depth**

| | |
|---|---|
| **Document** | HARC / DARC Kenwood TH-D72A Operating Manual |
| **Audience** | Licensed amateurs learning the TH-D72A |
| **Assumes** | Valid Canadian amateur licence and callsign |
| **Equipment** | Kenwood TH-D72A (144/440 MHz FM HT + GPS + AX.25 TNC) |
| **Also known as** | Often listed simply as “TH-72A” |
| **Version** | 0.3 |

**Scope:** Club **education**. Analog FM is covered for completeness but kept light. The educational weight is on **radio settings** (as exposed in MCP-4A) and **APRS / GPS / special features**.

### How this manual is weighted

| Topic | Depth |
|---|---|
| Analog FM voice, memories, tones | Brief — enough to get on local repeaters |
| Memory / VFO / Call / Weather channel fields | Brief — what each field *means* |
| Menu — Radio | Moderate — everyday comfort settings |
| **Menu — GPS / APRS / related tables** | **Deep** |
| Digipeater, EchoLink, Sky Command, MCP-4A | Deep enough for classroom use |
| Official menu encyclopaedia | Kenwood instruction manual remains authoritative for exact menu numbers |

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
| GPS + logging + target points | Chapters 11–12 |
| **APRS settings end-to-end** | **Chapters 13–15** |
| Messages, status, digipeat, SmartBeaconing | Chapters 14–15 |
| EchoLink / DTMF / Band Mask / Sky Command | Chapters 16–18 |
| Fix “I’m not beaconing” | Chapter 19 |

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

### Field habit

- Outdoors for a fix before blaming APRS.  
- Logging ≠ beaconing: you can log a hike with BCON off.  
- Export logs with MCP-4A (e.g. KML) after exercises.

---

## Chapter 12 — Target Point

Up to several named lat/lon targets (plus grid). The radio can show direction/distance toward the selected target.

| Column | Meaning |
|---|---|
| **Use** | Which target slot is active |
| **Name** | Label (trailhead, EOC, parking, etc.) |
| **Latitude / Longitude** | Target coordinates |
| **GS** | Grid square derived/associated display |

**Classroom use:** set one target to the meeting site so students see GPS navigation features without APRS TX.

---

## Chapter 13 — Menu — APRS (concepts + Basic / Packet / TX-RX / GPS)

This is the heart of the radio. MCP-4A’s **Menu — APRS** groups match the subsections below.

### North America frequency

Put **144.390 MHz FM** on the **Data Band**.

### APRS (Basic)

| Setting | What it does / how to use it |
|---|---|
| **Operating Mode** | **APRS** vs packet-oriented modes. Everyday position beaconing wants **APRS** (and the front-panel TNC in APRS, not Packet). |
| **My Callsign** | **Required.** Without it, the radio will not TX APRS. Include SSID (handhelds often use `-7`). |
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

### First beacon checklist

1. **My Callsign** set (with SSID).  
2. Data band = **144.390**.  
3. **[TNC]** → **APRS**.  
4. GPS fix (or My Position — Chapter 15).  
5. Method + Initial Interval chosen.  
6. **[BCON]** On (indicator visible).  
7. Verify locally and/or on [aprs.fi](https://aprs.fi).

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
| **Voice Alert** | Uses CTCSS on the APRS channel as a “someone nearby is on Voice Alert” proximity idea, with voice QSO potential. Off unless the local group uses it. |
| **CTCSS Frequency** | Tone used for Voice Alert (commonly discussed as 100.0 Hz in Kenwood APRS materials). |
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

### APRS (Message)

| Setting | What it does / how to use it |
|---|---|
| **Position Comment** | Standard short comment field (Off Duty, En Route, In Service, etc.) baked into position packets. Pick something honest. |
| **QSY in Status** | Embeds your voice frequency into status so others can QSY to you. |
| **Tone/Narrow** / **Shift/Offset** | Whether QSY info also carries tone and shift details. |
| **Status Text Channel in Use** | Which of the Status Text slots is active. |
| **Status Text** | Points at the Status Text table (Chapter 15). **QSY needs a real status configuration** — empty/disabled status is a common “why won’t QSY work?” failure. |
| **User Phrases** | Quick canned text for messaging (Chapter 15). |
| **Reply** / **Delay Time** / **Text** / **Reply To** | Automatic reply to incoming messages (delay, text, which sender pattern). Keep **Off** unless you have a deliberate unattended reason — easy to create RF noise loops. |

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

### APRS (NAVITRA)

Japanese NAVITRA group messaging features (**Group Mode**, **Group Code**, message channel). Not used in normal North American club APRS. Leave disabled / unused unless teaching a specialty topic.

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

## Chapter 18 — Menu — Sky Command II

| Setting | What it does / how to use it |
|---|---|
| **Commander Callsign** | Callsign identity for the handheld commander role |
| **Transporter Callsign** | Callsign of the HF transporter / base side |
| **Tone Frequency** | CTCSS used on the Sky Command link |

Sky Command II remotes a compatible Kenwood HF station via the handheld. **Skip until HF mentoring is available.** Leave callsigns at safe placeholders on shared radios so nobody accidentally keys a link.

---

## Chapter 19 — Troubleshooting

| Symptom | Likely cause | What to try |
|---|---|---|
| No APRS TX | My Callsign empty | Set My Callsign + SSID |
| No APRS TX | TNC Off or Packet | **[TNC]** → **APRS** |
| No APRS TX | BCON not armed | **[BCON]** until indicator shows |
| No APRS TX / odd posits | No GPS fix | Go outside; or set My Position |
| Hear nothing on APRS | Wrong frequency / data band | **144.390** on Data Band; match Packet Band |
| Collisions / chopped packets | DCD / Tx Delay | Prefer DCD sense on data band; increase Tx Delay |
| Hear others, not on aprs.fi | No IGate heard you | Move; shorten/fix path; ask locals |
| Beaconing too often | Interval / SmartBeaconing | Lengthen rates; enable Decay; check Low Speed jitter |
| QSY info missing | Status empty / Tx Rate Off | Configure Status Text + QSY in Status |
| Voice on 144.390 | TX on data band | Move voice to the other band |
| Radio “won’t TX” | Inhibit / lock / TOT / password | Check Menu — Radio TX Inhibit, Lock, TOT, Password |
| Radio dies in class | APO / Save / lamp | Check Automatic Power-off |
| Digi mystery traffic | Digipeat left On | Turn Digipeat Off after exercises |
| Units look “American” | Display units | Menu — APRS Display unit settings |

---

## Chapter 20 — Suggested training path

1. **Analog:** one repeater memory + simplex (Chapters 4–5).  
2. **Tour MCP-4A headings** so students know where settings live (Chapter 3).  
3. **APRS receive only:** 144.390, TNC APRS, watch the list.  
4. **First beacon:** Chapter 13 checklist → aprs.fi.  
5. **Manners:** interval, Decay, path, Proportional Pathing.  
6. **Status / messages / QSY** (Chapters 14–15).  
7. **Optional:** SmartBeaconing drive, GPS log export, digipeater drill, EchoLink DTMF demo.  

---

## Appendix A — Quick reference card

### APRS bring-up (NA)

```
My Callsign  →  144.390 on Data Band
TNC → APRS  →  GPS fix (or My Position)
Method + Initial Interval  →  BCON ON
Verify aprs.fi / local decode
```

### Keys

| Key | Role |
|---|---|
| **TNC** | Off / APRS / Packet |
| **BCON** | Arm beaconing |
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
| 0.3 | 2026-07-31 | Restructured around MCP-4A export headings; settings explained without personal values |

Menu numbers in the field may be confirmed against the Kenwood instruction manual for your firmware; this book prefers **setting names** (as in MCP-4A) so wording stays stable across docs.

---

## Annex — Sources and acknowledgements

Original HARC/DARC training narrative. Not a copy of Nifty or third-party commercial guides.

| Source | Use |
|---|---|
| Kenwood TH-D72A Instruction Manual | Authoritative menus and specifications |
| Kenwood TH-D72A/E APRS / In-Depth materials | Decay, Proportional Pathing, SmartBeaconing, QSY, Voice Alert concepts |
| Kenwood MCP-4A (export section headings) | Outline of settings chapters in this book |
| SSIARS practical TH-D72A notes | BCON/TNC field quirks (paraphrased) |
| aprs.fi / APRS network practice | Beacon verification |

*Independent educational material for Halifax & Dartmouth Amateur Radio Clubs. Not affiliated with or endorsed by JVCKENWOOD / Kenwood.*
