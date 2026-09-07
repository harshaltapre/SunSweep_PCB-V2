# Slider Base System (Solar Cleaning Pro)

[![Hardware Revision](https://img.shields.io/badge/Hardware%20Rev-A-brightgreen.svg)](#hardware-revisions)
[![Controller](https://img.shields.io/badge/MCU-ESP32--C5-blue.svg)](#hardware-variants)
[![EDA](https://img.shields.io/badge/EDA-EasyEDA%20Pro-orange.svg)](#hardware-structure)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Hardware and firmware repository for the **Slider Base System** (Solar Cleaning Pro). This system provides an industrial-grade motorized slider controller designed for automated solar panel cleaning robots and linear motion rigs, powered by the Espressif **ESP32-C5** dual-band Wi-Fi 6 & Bluetooth 5 MCU.

---

## Key Features

- **Dual Hardware Variants**:
  - **XIAO ESP32-C5 (Compact Variant)**: Ultra-compact footprint utilizing the Seeed Studio XIAO ESP32-C5 SMD carrier.
  - **ESP32-C5 DevKitC-1 (Development Board Variant)**: Prototyping and testbed version hosting a standard ESP32-C5-DevKitC-1 module.
- **Robust Power Architecture**:
  - High-voltage DC input via 5.5×2.1mm DC barrel jack (`DC-005`) or heavy-duty screw terminal.
  - Onboard high-efficiency switching regulator (TO-263-5 DC-DC Buck converter) stepping down to +5V.
  - Dual fuse protection (`F1`, `F2` 5×20mm fuse clips) for main power and load isolation.
  - Reverse polarity and transient protection diodes (`D3`, `D5`).
- **Motor / Actuator Driving**:
  - Dual SPDT power relays (`RLY1`, `RLY2` - SRD-05VDC-SL-C) rated for DC motor forward/reverse direction control and power switching.
  - Low-side NPN driver transistors (`Q1`, `Q2`) with dedicated flyback clamping diodes (`D1`, `D4`).
  - Heavy-duty 5.0mm pitch screw terminals (`KF301`) for motor and relay contact routing.
- **Isolated Slider & Limit Sensing**:
  - Optocoupler-isolated digital inputs (`U2`, `U10` DIP-4 PC817) for endstops, slider limit switches, and safety sensors.
  - Pull-up circuitry and dedicated terminal connections for noise immunity in high-EMI outdoor environments.
- **Expansion & Interfaces**:
  - 10-pin expansion GPIO header (`H1`).
  - 6-pin I2C and telemetry sensor interface (`P1`).

---

## Hardware Variants

| Feature | XIAO ESP32-C5 Variant | ESP32-C5 DevKitC-1 Variant |
| :--- | :--- | :--- |
| **Target Controller** | Seeed Studio XIAO ESP32-C5 (SMD footprint) | Espressif ESP32-C5-DevKitC-1 (Header socket) |
| **Form Factor** | Compact Carrier (4320 × 2655 mil / ~109.7 × 67.4 mm) | Full Development Carrier |
| **Relay Channels** | 2 × SPDT (Direction / Actuation) | 2 × SPDT (Direction / Actuation) |
| **Isolated Inputs** | 2 × Optocoupled limit inputs | 2 × Optocoupled limit inputs |
| **Power Input** | DC Barrel Jack & Terminal (Fused) | DC Barrel Jack & Terminal (Fused) |
| **Design Revision** | Rev A | Rev A |

---

## Repository Structure

```text
slider-based-PCB-design/
├── README.md
├── .gitignore
│
├── hardware/
│   ├── esp32-c5-devboard/
│   │   └── rev-a/
│   │       ├── documentation/       # Schematic & PCB drawings (PDF & PNG)
│   │       ├── easyeda/             # EasyEDA Pro project source files
│   │       ├── exports/             # DXF, Netlist, and PADS export archives
│   │       └── manufacturing/
│   │           ├── 3d/              # 3D CAD STEP assembly models
│   │           ├── bom/             # Excel BOM and Interactive HTML BOM (iBOM)
│   │           ├── gerber/          # Gerber zip archives ready for fabrication
│   │           └── odb++/           # ODB++ production archives
│   │
│   └── xiao-esp32-c5/
│       └── rev-a/
│           ├── documentation/       # Board info, PCB layouts, and specifications
│           ├── easyeda/             # EasyEDA Pro project files (.epro2)
│           ├── exports/             # Netlist and PADS export archives
│           └── manufacturing/
│               ├── 3d/              # 3D CAD STEP assembly models
│               ├── bom/             # Excel BOM and Interactive HTML BOM (iBOM)
│               └── gerber/          # Gerber zip archives ready for fabrication
│
├── firmware/
│   ├── common/                      # Shared libraries, motor control state machines
│   ├── esp32-c5-devboard/           # Firmware build targets for DevKit variant
│   └── xiao-esp32-c5/               # Firmware build targets for XIAO variant
│
├── libraries/
│   ├── symbols/                     # Custom schematic component symbols
│   ├── footprints/                  # Custom PCB footprints
│   └── 3d-models/                   # STEP / 3D model library
│
└── documentation/
    ├── pinout/                      # Pin assignment guides and diagrams
    ├── wiring/                      # Field wiring and motor connection diagrams
    ├── assembly/                    # Assembly instructions and soldering guides
    └── revisions/                   # Engineering change orders (ECO) and changelogs
```

---

## Fabrication & Assembly

### 1. PCB Ordering (Gerbers)
Ready-to-order Gerber packages are located in:
- DevBoard: [`hardware/esp32-c5-devboard/rev-a/manufacturing/gerber/Gerber_PCB1_2026-09-07.zip`](hardware/esp32-c5-devboard/rev-a/manufacturing/gerber/Gerber_PCB1_2026-09-07.zip)
- XIAO Board: [`hardware/xiao-esp32-c5/rev-a/manufacturing/gerber/Gerber_PCB1_2026-09-07.zip`](hardware/xiao-esp32-c5/rev-a/manufacturing/gerber/Gerber_PCB1_2026-09-07.zip)

**Recommended PCB Specs:**
- **Layers:** 2 layers
- **Material:** FR-4 (1.6mm thickness)
- **Copper Weight:** 1 oz (2 oz recommended if driving high-current DC motors continuously)
- **Surface Finish:** HASL with lead or ENIG

### 2. Assembly & Interactive BOM (iBOM)
For rapid manual assembly and component placement, open the offline interactive BOMs in any web browser:
- DevBoard: [`hardware/esp32-c5-devboard/rev-a/manufacturing/bom/InteractiveBOM_PCB1_2026-9-7.html`](hardware/esp32-c5-devboard/rev-a/manufacturing/bom/InteractiveBOM_PCB1_2026-9-7.html)
- XIAO Board: [`hardware/xiao-esp32-c5/rev-a/manufacturing/bom/InteractiveBOM_PCB1_2026-9-7.html`](hardware/xiao-esp32-c5/rev-a/manufacturing/bom/InteractiveBOM_PCB1_2026-9-7.html)

### 3. 3D Mechanical Integration
Full 3D models are available in STEP format for enclosure design and 3D printing in the `manufacturing/3d/` folders.

---

## Hardware Revisions

| Revision | Date | Notes |
| :--- | :--- | :--- |
| **Rev A** | September 2026 | Initial baseline release with dual ESP32-C5 variants (XIAO & DevKit), dual relay drive, optocoupled inputs, and fused power supply. |

---

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
