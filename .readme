# Brake System Plausibility Device (BSPD)

A standalone, analog **Brake System Plausibility Device (BSPD)** designed for **Formula Student / Formula SAE Electric Vehicles**. This project implements the mandatory BSPD safety system using analog comparators, logic gates, and timing circuits without relying on programmable controllers.

The BSPD continuously monitors the brake pressure sensor and tractive system current sensor. If hard braking occurs while the vehicle is delivering significant propulsion power, or if either sensor fails, the BSPD opens the Shutdown Circuit (SDC), disabling the tractive system.

---

## Features

- Standalone non-programmable hardware implementation
- Analog signal conditioning using LM358 op-amps
- Brake pressure and tractive current monitoring
- Adjustable sensor thresholds
- Sensor fault detection (Open Circuit / Short Circuit)
- 500 ms plausibility timer
- Direct Shutdown Circuit (SDC) control
- Designed according to Formula Student / Formula SAE BSPD requirements

---

## Repository Structure

```
.
├── BSPD.kicad_sch      # KiCad schematic
├── BSPD.kicad_pcb      # PCB layout
├── BSPD.kicad_pro
├── BSPD.kicad_prl
├── Bspd updated.pdf    # Schematic PDF
├── BSPD-backups/
└── README.md
```

---

# System Overview

The BSPD consists of four major functional blocks:

1. Signal Conditioning
2. Sensor Validation
3. Plausibility Detection
4. Shutdown Circuit Control

---

# Circuit Operation

## 1. Signal Conditioning

The brake pressure sensor and current sensor produce analog voltages proportional to brake pressure and tractive system current.

LM358 operational amplifiers (U1A and U1B) are configured as comparators to condition these signals and compare them against adjustable reference voltages.

The comparator output becomes HIGH whenever:

```
Sensor Voltage > Reference Voltage
```

This indicates:

- Hard braking detected
- Tractive system current corresponding to approximately **5 kW** or greater

The reference voltages can be adjusted using onboard potentiometers to calibrate the BSPD.

---

## 2. Sensor Validation

Sensor failures such as broken wires or short circuits can produce invalid voltages.

To detect these faults, each sensor is monitored using window comparators (U3A and U3B).

The valid operating range is:

```
0.5 V < Sensor Voltage < 4.5 V
```

Therefore,

- Voltage below **0.5 V**
  - Short to Ground
  - Open sensor
  - Broken wire

- Voltage above **4.5 V**
  - Short to Supply
  - Sensor failure

Only signals within the valid operating window are considered acceptable.

If either sensor voltage falls outside this range, the BSPD immediately opens the Shutdown Circuit.

---

## 3. Plausibility Detection

The conditioned outputs from the pressure and current comparators are connected to a **74HC08 AND gate (U2)**.

The AND gate confirms that both conditions occur simultaneously:

- Hard braking
- Current equivalent to ≥ 5 kW

Mathematically,

```
Brake AND Current
```

To prevent nuisance trips caused by noise or transient conditions, this signal passes through a **555 Timer** configured to introduce a **500 ms delay**.

The BSPD only considers the event valid if both signals remain HIGH continuously for at least **0.5 seconds**.

---

## 4. Shutdown Logic

A **74V1G27 NOR gate (U5)** controls the Shutdown Circuit (SDC).

The NOR gate monitors:

- Pressure sensor validity
- Current sensor validity
- 500 ms plausibility signal

The Shutdown Circuit opens whenever:

- Either sensor experiences an open circuit
- Either sensor experiences a short circuit
- Both plausibility conditions are not continuously satisfied for 500 ms

This immediately disables the tractive system by opening the SDC.

---

# Logic Summary

| Brake | Current | Sensor Status | Delay | BSPD Action |
|--------|---------|---------------|-------|-------------|
| No | No | Valid | — | Normal |
| Yes | No | Valid | — | Normal |
| No | Yes | Valid | — | Normal |
| Yes | Yes | Valid | <500 ms | Normal |
| Yes | Yes | Valid | ≥500 ms | Open SDC |
| Any | Any | Open Circuit | — | Open SDC |
| Any | Any | Short Circuit | — | Open SDC |

---

# Hardware Components

| Component | Description |
|------------|-------------|
| LM358 | Signal conditioning comparators |
| LM358 | Window comparator for fault detection |
| 74HC08 | AND logic gate |
| 74V1G27 | NOR gate for shutdown logic |
| NE555 | 500 ms delay timer |
| Potentiometers | Threshold adjustment |
| Passive Components | Filters, references, pull-ups and timing network |

---

# Formula Student / Formula SAE Compliance

This BSPD has been designed around the requirements specified in:

- Formula SAE Rules 2025
- Formula Student Rules 2026

Implemented requirements include:

- Standalone non-programmable circuit
- Independent brake and current sensing
- Detection of simultaneous hard braking and ≥5 kW power
- Maximum 500 ms response time
- Open circuit detection
- Short circuit detection
- Direct Shutdown Circuit activation

---

# Future Improvements

- Manual reset latch
- Improved EMC filtering
- Automotive-grade connectors
- ISO 26262-inspired diagnostic coverage
- LED status indicators
- Hardware redundancy

---

# Software

No firmware or programmable controller is required.

All safety logic is implemented entirely in hardware.

---

# PCB

The PCB was designed in **KiCad** and includes:

- Analog signal conditioning
- Sensor validation circuitry
- Logic gate implementation
- Delay timer
- Shutdown interface

---

# Author

**Mamun Or Rashid**

Mechatronics Engineering  
Rajshahi University of Engineering & Technology (RUET)

GitHub:
https://github.com/imamunorzrashid

---

# License

This project is released under the MIT License.

Feel free to use, modify, and improve this design for educational and Formula Student projects.
