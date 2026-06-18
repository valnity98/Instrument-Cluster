# Instrument Cluster — CAN Bus Simulation (Only Simulation)

> ⚠️ **This project is no longer maintained.** The repository is archived for reference only.

**MATLAB/Simulink simulation of CAN messages for a BMW E9x instrument cluster.**

Developed as part of the Master's course *Embedded systems and networking of mechatronic systems* (Mechatronics & Robotics, Frankfurt UAS, WiSe 2024/2025).

| Hardware | Simulation |
|---|---|
| ![Hardware](images/instrument-cluster-hardware.png) | ![Simulation](images/instrument-cluster-simulation.png) |

---

## Project Goals

- Simulate a functional instrument cluster using real CAN message definitions
- Create and maintain a `.dbc` file covering all relevant cluster signals
- Generate realistic signal waveforms from a MATLAB/Simulink model
- Provide an extensible architecture for adding new signals

---

## System Architecture

```
┌─────────────────────────────┐
│  Simulink Signal Generator  │  (can-signal-sim.slx)
│  - Speed ramp               │
│  - RPM sine wave            │
│  - Fuel level step          │
│  - Temperature, indicators  │
└──────────────┬──────────────┘
               │ Simulink CAN Pack / CAN Write blocks
               ▼
┌──────────────────────────────┐
│  Vehicle Network Toolbox     │  CAN channel (virtual or hardware)
│  CAN channel (Peak/IXXAT/…)  │
└──────────────┬───────────────┘
               │ Physical / virtual CAN bus
               ▼
┌──────────────────────────────┐
│  BMW E9x Instrument Cluster  │  (target hardware)
└──────────────────────────────┘
```

---

## Technical Overview

| Layer | Technology |
|---|---|
| Signal definition | DBC file (`bmw-e9x-can-database.dbc`) |
| Simulation model | MATLAB/Simulink (`can-signal-sim.slx`) |
| CAN transmission | MATLAB Vehicle Network Toolbox |
| Project management | MATLAB Project (`simulation.prj`) |

### DBC File

The `bmw-e9x-can-database.dbc` file defines all CAN messages and signals for the BMW KOMBI (Kombiinstrument). Key signals include speedometer, tachometer, fuel gauge, coolant temperature, and indicator lamps.

---

## Requirements

| Tool | Version |
|---|---|
| MATLAB | R2024b |
| Simulink | R2024b |
| Vehicle Network Toolbox | R2024b |
| CAN hardware (optional) | Peak PCAN, IXXAT, or Vector CANcase |

A virtual CAN channel can be used for simulation without hardware.

---

## Getting Started

1. Open MATLAB R2024b.
2. Open the project file: `PKW/simulation.prj`
3. Open the Simulink model: `can-signal-sim.slx`
4. Configure the CAN channel in the **CAN Configuration** block to match your hardware or select a virtual channel.
5. Run the simulation (`Ctrl+T`).

---

## Project Structure

```
Instrument-Cluster/
├── images/
│   ├── instrument-cluster-hardware.png     Hardware photo
│   └── instrument-cluster-simulation.png   Simulink model screenshot
├── PKW/
│   ├── bmw-e9x-can-database.dbc            CAN signal database
│   ├── simulation.prj                      MATLAB project file
│   └── can-signal-sim.slx                  Simulink simulation model
└── README.md
```

---

## License

Copyright (c) 2026 Mutasem Bader — All Rights Reserved.  
Viewing is permitted. Copying, modifying, or submitting as own work is strictly prohibited.  
See [LICENSE](LICENSE) for details.
