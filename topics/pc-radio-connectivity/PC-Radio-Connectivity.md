# Halifax & Dartmouth Amateur Radio Clubs  
# PC ↔ Radio Connectivity (training overview)

**Audience:** New operators connecting *any* club radio to a computer  
**Version:** 0.1  
**Scope:** Concepts shared across radios. Each radio manual adds model-specific cables, drivers, and software.

This is **not** a substitute for a radio’s own chapter — it is the map so USB/serial stops feeling like magic.

---

## Why this matters

Almost every “digital” activity eventually needs a PC (or Pi):

| Goal | Typical need |
|---|---|
| Program memories / codeplug | Vendor CPS / MCP / CHIRP-class tool |
| DMR contacts / talkgroups | CPS + often a codeplug file |
| APRS / packet / Winlink | Serial or audio path into an app |
| Firmware update | Vendor updater + stable USB |
| GPS / log export | Serial/NMEA or vendor utility |

---

## Three different “connections” people confuse

| Path | What moves | Examples |
|---|---|---|
| **Programming / control serial** | Channel data, menus, sometimes GPS logs | Kenwood MCP-4A USB; Baofeng CPS cable; Yaesu programming cable |
| **TNC / KISS serial** | AX.25 packet frames to Winlink Express, Pat, etc. | TH-D72A built-in TNC over USB in PACKET mode |
| **Sound-card / audio** | Analog audio for FT8, JS8, some Winlink HF modes, AllStar, etc. | USB sound interface + radio speaker/mic or data jack |

A radio may support one or more of these. **Using the wrong mental model** (expecting a programming cable to do FT8 audio, or MCP-4A to do Winlink) is the most common beginner failure.

---

## OS expectations

### Windows

- Most vendor CPS tools target Windows first.  
- USB-serial devices need a **driver** → then appear as `COM3`, `COM7`, …  
- Device Manager is your friend: unknown device = driver missing; correct COM = note the number for the app.  
- Only **one** program should open a COM port at a time.

### Linux

- Many USB-serial chips work with in-kernel drivers (`cp210x`, `ch341`, `ftdi_sio`, …) → `/dev/ttyUSB0` or `/dev/ttyACM0`.  
- Permission: user usually needs `dialout` (or udev rules).  
- Vendor GUI CPS may be missing — use wine/VM, or radio-specific open tools when they exist.  
- Packet: AX.25 tools + Pat are common for VHF Winlink.

### Raspberry Pi

- Same ideas as Linux.  
- Watch **power**: hungry HTs + WiFi + HDMI on a weak supply → USB disconnect ghosts.  
- Great for dedicated Pat / digi / gateway projects once the serial path is proven on a laptop.

---

## Cable and port cheat-sheet (fill per radio)

| Radio | Physical | Driver / device | Programming app | Digital / Winlink path |
|---|---|---|---|---|
| Kenwood TH-D72A | Mini-USB | VCP / CP210x → COM or ttyUSB | MCP-4A | Built-in TNC, PACKET mode → Express / Pat |
| Baofeng DM-32UV | Vendor USB cable | CPS COM port | Baofeng CPS | DMR/APRS via radio+network; not classic AX.25 TNC |
| *(add rows as manuals mature)* | | | | |

---

## Safe habits (all radios)

1. **Backup first** (read + save) before writing.  
2. Correct **COM/`tty`** — guessing the wrong port looks like “software is broken.”  
3. Close the other app before switching MCP ↔ Winlink ↔ CPS.  
4. Charged battery / external power during firmware writes.  
5. Never publish personal codeplugs with passwords, DMR IDs, or private DTMF codes in shared repos.

---

## Where to go next

| Need | Document |
|---|---|
| TH-D72A USB, packet, Winlink | [`radios/Kenwood-TH-D72A/TH-D72A-Operating-Manual.md`](../../radios/Kenwood-TH-D72A/TH-D72A-Operating-Manual.md) Chapters 19–21 |
| DM-32UV CPS | [`radios/DM-32UV/`](../../radios/DM-32UV/) |
| General Winlink operating (non-radio-specific) | Future `topics/winlink/` (planned) |

---

## Annex

Club training overview. Radio OEM manuals remain authoritative for pinouts and official drivers.
