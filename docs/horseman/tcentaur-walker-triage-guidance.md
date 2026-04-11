**Triage Guidance Document**  
**Centaur Free Flow Exerciser –**  
**Version 1.13** | April 10, 2026  

**The Simple Path to AI & Digital Success.**  
**SimplexVia LLC** – Research support

---

### Purpose
This document provides **quick, safe triage steps** for barn staff when the Centaur Free Flow Exerciser does **not** start, stop, or operate correctly using the **factory-original white/gray control panel**.  

---

### 1. Safety First – Never Bypass These
- **Physical E-stop** must be pulled out (reset) before anything works.  
- Shocker **must** be ON before the walker will start **during normal horse exercise sessions**.  
- **Horses must be attached before turning the machine on for normal daily operation and exercise sessions.**  
- Never change direction while the walker is moving.  
- Minimum 10-minute timer required for each horse exercise session.

**Important Clarification on Testing**  
The machine **can** be safely tested and run **empty (with no horses attached)** for troubleshooting, maintenance, commissioning, or verifying repairs. Empty testing is allowed and recommended.

**Recommended Safe Empty-Test Procedure**  
1. Ensure the arena/fence area is completely clear of people and objects.  
2. Reset the red E-stop button (pull firmly).  
3. Turn the shocker switch **OFF** (not needed for empty test).  
4. **Set the timer to 2–5 minutes** (this is allowed and safe for empty testing).  
5. Select Forward or Reverse.  
6. Press and hold the green START button.  
7. Observe arm movement, listen for unusual noises, and test speed control while running.

**Note on Timer Minimum**  
The 10-minute minimum in the Centaur manual (pages 28–30) applies **only** to normal horse exercise sessions. It does **not** apply to empty test runs. The mechanical timer and Commander C200 VSD allow any duration (including 2–5 minutes) when no horses are attached.

---

### 2. Quick Triage Checklist (Do This First – 60 Seconds)
1. **Power** – Is the main power switch ON and the machine plugged in?  
2. **E-stop** – Pull out the red mushroom button (it must click and stay out).  
3. **Shocker** – Turn the shocker switch to **ON** (for normal use).  
4. **Timer** – Set the timer for at least **10 minutes** (or more).  
5. **Direction** – Make sure Forward or Reverse is selected.  
6. **Start button** – Press and hold the green START button for 2–3 seconds.

If it still does **not** run → go to Step 3 and check the VSD.

---

### 3. Commander C200 VSD – How It Fits into the System
The original control panel does **not** directly power the motor. It sends simple signals to the **Commander C200 Variable Speed Drive (VSD)**, which then controls the 3-phase motor.

**System Flow**  
Control Panel (switches, speed knob, timer, E-stop, shocker)  
↓ (digital on/off + 0–10 V analog speed signal)  
**Commander C200 VSD** (green box inside control enclosure)  
↓ (precise variable voltage & frequency 0–240 V, 0–550 Hz)  
Motor & mechanical arms

**Firmware in the System**  
- Original control panel switches and timer: **100 % analog / electromechanical** – no firmware.  
- Commander C200 VSD: **Contains embedded firmware** (software version typically V01.xx). The firmware handles speed control, ramping, protection, and all trip logic.

**No WiFi Capability**  
The base C200 model has **no built-in WiFi or Bluetooth**. It uses only wired connections (Modbus RTU, optional plug-in modules). You must be physically at the machine to read diagnostics.

---

### 4. How to Get Output from the Commander C200
1. Power the machine ON (E-stop pulled out).  
2. Open the control box (power OFF first, then re-energize safely).  
3. Look at the **small display + keypad** on the front of the green C200 unit.  
4. The screen will show current status/speed or a **trip code**.  
5. Use the arrow keys to view trip history, parameters, and real-time motor data.

**Common Trip Codes** (see full table in References below)  
- **OV** – Over voltage  
- **I.Trip / OC** – Over current / motor overload  
- **dESt** – Parameter conflict  
- **UU** – Under voltage  
- **O.Ld** – Overload

For the full diagnostic info including how to read the VSD display and the trip codes, see the diagonstics section (chapter 12) starting on page 147 of the [Commander C200/C300 Control User Guide](https://moen.nidec.com/drives/-/media/Project/Nidec/ControlTechniques/Documents/Technical/Control-User-Guides/Commander-C/Commander-C200-C300-Control-User-Guide-EN.pdf)


---

### 5. Triage Flow (Updated with VSD)

**Symptom → Action**  
**Machine has no power / completely dead** → Check barn breaker + confirm C200 display lights up.  
**E-stop light is on or machine will not start** → Reset red E-stop + check VSD display for trip.  
**Starts for a second then stops** → Check shocker + **read VSD trip code**.  
**Speed does not change or is erratic** → Turn speed knob while running + check VSD display.  
**Will not change direction** → Full stop first + confirm VSD receives direction command.  
**Control panel buttons feel unresponsive** → Check wiring to VSD + read VSD display.

---

### 6. Common Problems & Fixes Table (Updated)

| Symptom                          | Most Likely Cause                     | Fix (Panel + VSD)                          | Ref. |
|----------------------------------|---------------------------------------|--------------------------------------------|------|
| Nothing happens                  | E-stop or no power to VSD             | Pull E-stop + check VSD power              | p. 28 |
| Starts then immediately stops    | Shocker OFF or VSD trip               | Turn shocker ON + read VSD display         | p. 29 |
| Speed does not increase          | Speed knob / VSD analog input         | Turn knob + check VSD trip                 | p. 30 |
| Intermittent power               | Loose wire or VSD input               | Tighten terminals + check VSD supply       | — |
| Erratic / sudden stop            | VSD trip (OV, I.Trip, etc.)           | Read and clear VSD trip code               | VSD Guide |
| Buttons do not respond           | Wiring to VSD or VSD fault            | Check wiring + VSD display                 | — |

---

### 7. When to Stop & Call for Service
Call your technician immediately if:
- VSD shows a persistent trip that will not clear after reset.  
- You smell burning or hear grinding from motor/gearbox.  
- The C200 display is blank or damaged.  
- You have tried the checklist twice with no success.

**Lock-Out / Tag-Out (LOTO)** before any internal work.

---

### 8. Quick Reference – Original Equipment Workflows
- Horses **always** attached **before** powering on **for normal exercise sessions**.  
- Speed **can** be adjusted while moving.  
- Direction change **only** when fully stopped.  
- Shocker **must** stay ON during entire session.  
- Minimum 10-minute sessions.

---

### 9. How to Read and Clear Trips on the Commander C200 (Pages 147–148)
According to the **Commander C200/C300 Control User Guide** (pages 147–148), the drive stores the **last 10 trips** in non-volatile memory and displays them on the built-in keypad.

**Step-by-step procedure to read trips**:

1. Ensure the machine is powered ON and the E-stop is pulled out (display must be lit).  
2. On the C200 keypad, press the **Trip** key (or navigate to Menu 0 → Status → Trip log).  
3. The display will show the **most recent trip** first (e.g., “OV” or “I.Trip”).  
4. Use the **Up / Down arrows** to scroll through the trip history (Trip 1 = most recent, Trip 10 = oldest).  
5. For each trip the display also shows:
   - Trip code  
   - Time stamp (when the trip occurred)  
   - The parameter number that triggered the trip (if applicable)  

**To clear a trip** (page 148):  
- Press the red **STOP / RESET** key once.  
- If the trip does not clear, power cycle the entire machine (turn main power OFF for 10 seconds, then back ON).  
- The drive will only allow a start after the trip is cleared.

**Important note from manual (p. 147)**:  
Trips are **latched** for safety. The drive will not run until the fault is acknowledged and cleared. Always record the exact trip code before clearing it.

---

### 10. References

**Manuals & Hyperlinks**  
- Centaur Free Flow Exerciser Service Manual (pages 28–30):  
  [Download PDF](https://equinecisers.com/site/wp-content/uploads/FREE-FLOW-EXERCISER-SERVICE-MANUAL-INSTALLATION-DIAGRAMS.pdf)  
- Commander C200/C300 Control User Guide (full manual, trip codes, parameters):  
  [Download PDF](https://moen.nidec.com/drives/-/media/Project/Nidec/ControlTechniques/Documents/Technical/Control-User-Guides/Commander-C/Commander-C200-C300-Control-User-Guide-EN.pdf)  
- Nidec / Control Techniques Drives Services & Downloads:  
  [moen.nidec.com/drives/services](https://moen.nidec.com/drives/services)  
- Commander C200 Parameter Reference & Trip Code List:  
  [ctmanuals.info (search “Commander C200”)](https://ctmanuals.info)  

**Connect Drive Commissioning Software** (free PC tool to read parameters, trip history, update firmware, and commission the C200 VSD)  
- Official Product Page & Documentation:  
  [https://moen.nidec.com/en-US/drives/Products/Software/Commissioning/Connect](https://moen.nidec.com/en-US/drives/Products/Software/Commissioning/Connect)  
- Direct Downloads Page (latest version V03.01.02):  
  [https://apps.controltechniques.com/Downloads/SharePoint/Download.aspx?SiteId=4&ProductId=258](https://apps.controltechniques.com/Downloads/SharePoint/Download.aspx?SiteId=4&ProductId=258)  
- Getting Started Guide (PDF):  
  [Download PDF](https://moen.nidec.com/drives/-/media/Project/Nidec/ControlTechniques/Documents/Technical/Getting-Started-Guides/Software/Connect/Commissioning-a-Control-Techniques-drive-using-Connect-Getting-Started-Guide-EN.pdf)  
- **Supported Platforms**  
  - **Windows only** (Windows 7 SP1, Windows 8, Windows 10, Windows 11 recommended).  
  - Not available for macOS or Linux.



**Commander C200 / C300 VSD Trip Codes Table**  
(Extracted from *Commander C200/C300 Control User Guide*, primarily Chapter 12 Diagnostics, pages 147–168)

| Code       | Description                                      | Possible Causes                                      | Page Reference |
|------------|--------------------------------------------------|------------------------------------------------------|----------------|
| OV         | Over voltage                                     | Supply too high, insufficient deceleration, braking issues | 159 |
| OI.AC      | Instantaneous output over current                | Short circuit, motor insulation fault, long cable    | 158–159 |
| OI.br      | Braking IGBT over current                        | Brake resistor wiring/value fault                    | 158 |
| dESt       | Two or more parameters writing to same destination | Parameter conflict (Menus 7, 8, 9, 12, 14)         | 153 |
| I.Trip / OC| Over current / motor overload                    | Motor overload, short circuit                        | 158 |
| UU         | Under voltage                                    | Low supply voltage                                   | — |
| O.Ld       | Overload                                         | Excessive load or prolonged high current             | 156 |
| Et         | External trip                                    | External safety input activated                      | 154 |
| th         | Motor thermistor over-temperature                | Motor overheating, faulty thermistor                 | 164 |
| FAn.F      | Fan fail                                         | Fan obstructed or failed                             | 154 |
| PAd        | Keypad removed while in keypad mode              | Keypad disconnected during operation                 | 160 |
| SCL        | Control word watchdog timeout                    | Control word not serviced within 1 second            | 163 |
| HFxx       | Hardware faults (HF01–HF19)                      | Control/power PCB failure                            | 154–156 |
| C.xx       | NV Media Card / cloning trips                    | Card errors, read-only, mismatch                     | 149–151 |
| SL.xx      | Option module trips (slot 1)                     | Option module fault or removed                       | 163–164 |

For the full diagnostic info including how to read the VSD display and all the trip codes, see the diagonstics section (chapter 12) starting on page 147 of the [Commander C200/C300 Control User Guide](https://moen.nidec.com/drives/-/media/Project/Nidec/ControlTechniques/Documents/Technical/Control-User-Guides/Commander-C/Commander-C200-C300-Control-User-Guide-EN.pdf)

**Sequence Diagrams**

**Normal Start Flow**

![Normal Flow Path](./images/NormalFlow.png)

**Fault/Trip Path**

![Fault Trip Path](./images/Fault-Trip-Path.png)

--

### Appendix A – VSD Replacement Guide
**Replacement Options for Commander C200 (C200-042 00133 A, 3 HP, 200–240 V, 13.3 A)**

| Rank | Manufacturer (US Focus)       | Model / Series                  | Key Specs Match                  | Single-Phase (2-Phase) Input Support | Why Reliable / Notes                                      | Supplier Link (Official / Major Distributor) | Approx. Price (USD) |
|------|-------------------------------|---------------------------------|----------------------------------|--------------------------------------|-----------------------------------------------------------|----------------------------------------------|---------------------|
| 1    | Rockwell Automation (USA)     | PowerFlex 525 (25B)            | 3 HP, 13.3 A, 200–240 V, 3-ph   | **Yes** (with ~35–50% derating)     | Highest reliability, modular, excellent diagnostics       | [Rockwell PowerFlex 525 3 HP](https://www.rockwellautomation.com/en-us/products/hardware/vfds-variable-frequency-drives/25b-powerflex-525.html) | $950 – $1,100 |
| 2    | Eaton (USA)                   | PowerXL DG1                    | 3 HP, 13–16 A, 200–240 V, 3-ph  | **Yes** (with derating)             | Built for harsh barn environments, energy-saving          | [Eaton PowerXL DG1 3 HP](https://www.eaton.com/us/en-us/catalog/drives/powerxl-dg1-variable-frequency-drives.html) | $680 – $820 |
| 3    | Eaton (USA)                   | PowerXL DC1 (compact)          | 3 HP, 13.3 A, 200–240 V, 3-ph   | **Yes** (with derating)             | Very compact, cost-effective                              | [Eaton PowerXL DC1 3 HP](https://www.eaton.com/us/en-us/catalog/drives/powerxl-dc1-variable-frequency-drives.html) | $460 – $550 |
| 4    | Rockwell Automation (USA)     | PowerFlex 523 (25A)            | 3 HP, 13.3 A, 200–240 V, 3-ph   | **Yes** (with derating)             | Slightly lower cost than 525, still very reliable         | [Rockwell PowerFlex 523 3 HP](https://www.rockwellautomation.com/en-us/products/hardware/vfds-variable-frequency-drives/25a-powerflex-523.html) | $680 – $790 |
| 5    | ABB (strong US operations)    | ACS355                         | 3 HP, 13–15 A, 200–240 V, 3-ph  | **Yes** (with derating)             | Extremely robust, easy parameter cloning                  | [ABB ACS355 3 HP](https://new.abb.com/drives/low-voltage-ac/drives-and-drive-modules/acs355) | $580 – $720 |
| 6    | Yaskawa (US manufacturing)    | GA500                          | 3 HP, 13.3 A, 200–240 V, 3-ph   | **Yes** (with derating)             | Excellent vector control, long MTBF                       | [Yaskawa GA500 3 HP](https://www.yaskawa.com/products/drives/industrial-ac-drives/ga500) | $620 – $780 |
| 7    | Schneider Electric (US ops)   | Altivar 320 (ATV320)           | 3 HP, 13–16 A, 200–240 V, 3-ph  | **Yes** (with derating)             | Compact, native Modbus                                    | [Schneider Altivar 320 3 HP](https://www.se.com/us/en/product-range/61374-altivar-320/) | $480 – $590 |
| 8    | Danfoss (US manufacturing)    | VLT Micro Drive (FC 51)        | 3 HP, 13.3 A, 200–240 V, 3-ph   | **Yes** (with derating)             | Harsh-environment rated                                   | [Danfoss VLT Micro Drive](https://www.danfoss.com/en-us/products/danfoss-drives/low-voltage-drives/vlt-micro-drive-fc-51/) | $510 – $650 |

---

**Important Note on “2-Phase” (Single-Phase) Input**  
All listed drives **support single-phase 200–240 V input** (what you called “2 phase”), but with **derating** (typically 35–50% of rated power) to prevent overheating the DC bus.  
The original C200 also supported single-phase input with derating, so this is normal for this size drive.  
If your barn supply is truly single-phase, the **Eaton PowerXL DC1** or **Schneider Altivar 320** are often the easiest to configure.

**DC Bus Clarification**  
The **DC Bus** is the bank of large capacitors located **inside the VSD device** itself.  
When running on single-phase input, the DC Bus experiences higher ripple current and heats up more, which is why manufacturers require derating (35–50 % of rated power) to keep the capacitors within safe temperature limits and extend drive life.

### Simple Explanation
Inside every modern Variable Speed Drive (VSD) there is a section called the **DC Bus**.  
It is a bank of large capacitors that store the DC voltage after the incoming AC power is converted (rectified) to DC.    The DC Bus then supplies clean DC power to the inverter stage that creates the variable-frequency AC for the motor.

**Why derating is required for single-phase (“2-phase”) input:**

- The original Commander C200 (and all the replacement drives) was **designed for 3-phase input**.
- When you feed it single-phase power instead, the rectifier only charges the DC Bus capacitors on every half-cycle instead of three times per cycle.
- This creates much higher ripple current → the capacitors heat up significantly more than normal.
- To prevent overheating and premature failure of the DC Bus capacitors, the manufacturer requires **derating** (reducing the output power to 35–50 % of the drive’s rated capacity).

In practice this means:
- A 3 HP drive run on single-phase power is safely limited to roughly **1–1.5 HP** continuous load (depending on the specific model).
- The Centaur exerciser motor is only ~3 HP, so derating is acceptable and commonly done.

All the drives in Appendix A above support single-phase input **with derating**. No external DC Bus or extra hardware is needed.