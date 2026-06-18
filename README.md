# Instrument Cluster — CAN Bus Simulation

**MATLAB/Simulink simulation of CAN messages for a BMW E9x instrument cluster**

This project simulates the CAN bus signals required to drive the instrument cluster of a BMW E9x (E90/E91/E92/E93) series vehicle. Signals are defined in a DBC file and transmitted via MATLAB's Vehicle Network Toolbox, enabling hardware-in-the-loop (HIL) testing without a real vehicle.

![Instrument Cluster](Image/Instrument-cluster.png)

---

## Project Goals

- Simulate a functional instrument cluster using real CAN message definitions
- Create and maintain a `.dbc` file covering all relevant cluster signals
- Generate realistic signal waveforms from a MATLAB/Simulink model
- Provide an extensible architecture for adding new signals

---

## Technical Overview

| Layer | Technology |
|---|---|
| Signal definition | DBC file (`E9x_KOMBI_V07.dbc`) |
| Simulation model | MATLAB/Simulink (`Sim_Signale.slx`) |
| CAN transmission | MATLAB Vehicle Network Toolbox |
| Project management | MATLAB Project (`.prj`) |

### Architecture

```
┌─────────────────────────────┐
│  Simulink Signal Generator  │  (Sim_Signale.slx)
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

### DBC File

The `E9x_KOMBI_V07.dbc` file defines all CAN messages and signals for the BMW KOMBI (Kombiinstrument). Key signals include speedometer, tachometer, fuel gauge, coolant temperature, and indicator lamps.

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
2. Open the project file: `PKW_Kombiinstruments/PKW_Kombiinstruments.prj`
3. Open the Simulink model: `Sim_Signale.slx`
4. Configure the CAN channel in the **CAN Configuration** block to match your hardware or select a virtual channel.
5. Run the simulation (`Ctrl+T`).

---

## Project Structure

```
Instrument-Cluster/
├── Image/
│   └── Instrument-cluster.png      Hardware photo
├── PKW_Kombiinstruments/
│   ├── E9x_KOMBI_V07.dbc           CAN signal database
│   ├── PKW_Kombiinstruments.prj    MATLAB project file
│   ├── Sim_Signale.slx             Simulink simulation model
│   └── slprj/                      Simulink build artefacts (auto-generated)
└── README.md
```

> **Note:** The `slprj/` folder contains auto-generated simulation cache files and should be added to `.gitignore`.

---

## Future Extensions

- Add wiper, door-open, and seatbelt warning signals
- Integrate a CANoe/CANalyzer trace for validation
- Parameterise signal profiles (speed ramp rate, RPM range) via MATLAB scripts
- Export signal traces to `.blf` or `.asc` for replay

---

## Contributors

- Mutasem Bader

---

## License

Copyright (c) 2026 Mutasem Bader — All Rights Reserved.  
Viewing is permitted. Copying, modifying, or submitting as own work is strictly prohibited.  
See [LICENSE](LICENSE) for details.
  
---
