# 🤖 Tight-Fit — Rover Main Control PCB

<p align="center">
  <strong>On-Spot Problem Statement • Takneek 2026 • IIT Kanpur</strong><br>
  <em>From a surprise brief to a rover-ready PCB concept in a 3-hour sprint.</em>
</p>

<p align="center">
  <a href="https://github.com/A11490M/Robotics-Club-PS">Repository</a> •
  <a href="./Project_Tight-Fit___Main_Control_PCB_20260829205302.pdf">PCB Documentation</a> •
  <a href="./Project_Tight-Fit___Main_Control_PCB_Team_Briefing_20260829190528.pdf">Team Briefing</a>
</p>

---

## ⚡ The Challenge

Takneek 2026 at **IIT Kanpur** included an on-spot problem statement where the dominant constraint was simple: **time**.

We were handed a surprise robotics requirement and had roughly **3 hours** to understand the problem, make engineering decisions, build the PCB design, document the result, and present it on the spot.

Our challenge was to design the **main control PCB for a rover** — a board-level architecture tying together control, sensing, navigation, power and external interfaces while keeping the design compact and defensible.

This repository preserves the resulting work as a snapshot of that sprint.

---

## 🎯 What We Built

**Tight-Fit** is a KiCad-based **rover main control PCB concept** centered around an ESP32 development module.

The design brings together:

- 🧠 **ESP32** — main controller and processing / communications core
- 📡 **GPS interface** — support for the GY-NEO6MV2 module
- 📏 **Ultrasonic sensing** — HC-SR04 interface for ranging and obstacle awareness
- 🔋 **Power regulation** — LM2596 DC-DC conversion stage
- 🔌 **External interfaces** — rover peripherals kept accessible through modular connections
- 📦 **3D mechanical assets** — STEP models for physical board visualization
- 🛠️ **Custom KiCad libraries** — symbols and footprints for the selected modules

The repository contains both the design assets and the generated documentation used during the sprint.

---

## 🧩 System Architecture

```text
                    ┌──────────────────────┐
                    │     Rover Battery    │
                    └──────────┬───────────┘
                               │
                        ┌──────▼──────┐
                        │   LM2596    │
                        │  DC-DC PSU  │
                        └──────┬──────┘
                               │
                     Regulated Power Rails
                               │
          ┌────────────────────▼────────────────────┐
          │                  ESP32                  │
          │        Main Control / Processing        │
          └───────┬───────────┬───────────┬────────┘
                  │           │           │
             ┌────▼────┐ ┌────▼─────┐ ┌───▼──────────┐
             │   GPS   │ │ HC-SR04  │ │   External   │
             │ NEO-6M  │ │Ultrasonic│ │    Rover     │
             │ Module  │ │  Sensor  │ │  Interfaces  │
             └─────────┘ └──────────┘ └──────────────┘
```

The core idea was to keep **power, control and sensing physically consolidated** while retaining straightforward access to the rover's peripherals.

---

## 🔧 Design Approach

### 1. Architecture before layout

Under a hard deadline, the first task was to define the functional blocks:

**Power → Controller → Sensors → Interfaces → Placement → Routing → Documentation**

This kept the board layout from becoming the architecture.

### 2. ESP32 as the control core

The ESP32 development module acts as the rover's central compute and control element. The repository includes dedicated KiCad assets for the module, including `ESP32-DEVKIT-V1`, `ESP32-DOIT-DEVKIT`, and a revised 30-pin symbol.

### 3. Rover sensing and navigation

The design provides dedicated support assets for:

- **HC-SR04** ultrasonic ranging
- **GY-NEO6MV2** GPS

This keeps common rover sensing/navigation hardware easy to interface without making the controller unnecessarily monolithic.

### 4. Explicit power conversion

A dedicated **LM2596 DC-DC** stage handles the incoming supply before it reaches the low-voltage electronics. Making the power path explicit was important for both system clarity and board-level organization.

### 5. Mechanical fit is part of electronics

The project also preserves STEP models for hardware such as the ESP32 and HC-SR04. That makes the design useful for physical fit and placement checks, not just schematic connectivity.

---

## 📐 Why “Tight-Fit”?

The name reflects the two pressures of the challenge: **limited time** and **limited board real estate**.

The goal was not to build the most elaborate rover motherboard possible. It was to produce a coherent, defensible PCB concept quickly, with engineering trade-offs that could be explained in a presentation.

> **Enough functionality to be useful. Enough structure to be reliable. No unnecessary complexity.**

That mindset was central to solving an on-spot hardware problem.

---

## ⏱️ The 3-Hour Sprint

```text
00:00  Problem statement revealed
  │
  ├── Requirements extraction
  ├── Functional block definition
  └── Component / module selection
  │
01:00  Schematic + interface architecture
  │
  ├── ESP32 core
  ├── Sensor interfaces
  ├── GPS
  └── Power conversion
  │
02:00  PCB placement + routing
  │
  ├── Physical fit
  ├── Connector accessibility
  └── Power / signal organization
  │
02:45  Verification + cleanup
  │
  └── Documentation / presentation
  │
03:00  🚀 Submission
```

The exact sequence evolved during the sprint, but the principle stayed the same: **time-box every engineering decision**.

---

## 🧠 What Made the Problem Interesting?

A normal PCB project gives you time to iterate. An on-spot problem removes that luxury.

The challenge therefore was not simply routing traces. It was deciding, quickly and confidently:

- what belongs on the main board,
- which interfaces should remain modular,
- how the power path should be organized,
- how much routing complexity is justified,
- how real modules fit physically,
- and what can actually be defended in the final presentation.

In other words, this was **systems engineering under a hard deadline**.

---

## 📁 Repository Contents

| Asset | Purpose |
|---|---|
| `Project_Tight-Fit___Main_Control_PCB_20260829205302.pdf` | Generated PCB/design documentation |
| `Project_Tight-Fit___Main_Control_PCB_Team_Briefing_20260829190528.pdf` | Team briefing and original design context |
| `ESP32-DEVKIT-V1.kicad_sym` | ESP32 DevKit KiCad symbol |
| `ESP32-DEVKIT-V1.step` | ESP32 DevKit 3D model |
| `ESP32-DOIT-DEVKIT.kicad_mod` | ESP32 DOIT DevKit footprint |
| `MODULE_ESP32_DEVKIT_V1.kicad_mod` | ESP32 module footprint asset |
| `esp32_30pin_revised.kicad_sym` | Revised ESP32 symbol |
| `HC-SR04.kicad_sym` | HC-SR04 KiCad symbol |
| `HC-SR04.step` | HC-SR04 3D model |
| `XCVR_HC-SR04.kicad_mod` | HC-SR04 footprint |
| `GY-NEO6MV2.kicad_mod` | GPS module footprint |
| `LM2596-DC-DC.kicad_mod` | DC-DC converter footprint |
| `BOB-12009.kicad_sym` | Breakout-board symbol asset |
| `BOB-12009.step` | Breakout-board 3D model |
| `CONV_BOB-12009.kicad_mod` | Breakout-board footprint |
| `MO-220-WGGD-11_SEN-12650_SPK*.kicad_mod` | Additional footprint assets |
| `Screenshot 2026-08-30 005205.png` | Design screenshot |
| `Screenshot 2026-08-30 005847.png` | Design screenshot |
| `how-to-import.htm` | External CAD asset import reference |

The repository tree confirms the preserved ESP32, GPS, ultrasonic, power-converter, STEP, footprint and documentation assets. fileciteturn5file0L2-L3

---

## 🖥️ Toolchain

**EDA:** [KiCad](https://www.kicad.org/)

**Electrical design assets:** KiCad symbols and footprints

**Mechanical design assets:** STEP models

**Documentation:** PDF exports and screenshots from the final design workflow

The supporting CAD assets are kept alongside the documentation so the work remains inspectable and reproducible rather than existing only as a presentation image.

---

## 📸 Explore the Result

### Main PCB Documentation

[**→ Open the generated PCB PDF**](./Project_Tight-Fit___Main_Control_PCB_20260829205302.pdf)

### Team Briefing

[**→ Open the team briefing PDF**](./Project_Tight-Fit___Main_Control_PCB_Team_Briefing_20260829190528.pdf)

### CAD / Library Assets

Browse the repository for the custom KiCad symbols, footprints and STEP models used to represent the selected modules.

---

## 🏁 Outcome

This repository is a record of a **rapid hardware-design challenge**: a surprise rover requirement, a three-hour clock, and a complete PCB concept produced under pressure.

It is less about presenting a production-certified rover motherboard and more about demonstrating the ability to move from:

**ambiguous requirements → system architecture → component selection → PCB implementation → presentation-ready engineering output**

in a single focused sprint.

---

## 🤝 Built for Takneek 2026

| | |
|---|---|
| **Event** | Takneek 2026 |
| **Institute** | IIT Kanpur |
| **Challenge** | On-Spot Problem Statement |
| **Domain** | Rover Electronics / PCB Design |
| **Focus** | Main Control PCB |
| **Time Constraint** | ~3 hours |

---

<p align="center">
  <sub>Built fast. Designed deliberately. Documented completely. 🚀</sub>
</p>
