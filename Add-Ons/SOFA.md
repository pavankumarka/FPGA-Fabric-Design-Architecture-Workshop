# What is SOFA?

**SOFA (Simple Open FPGA Architecture)** is an open-source FPGA architecture project built on top of the OpenFPGA framework. It provides complete FPGA fabric implementations that researchers, students, and engineers can study, modify, and generate.

Think of SOFA as a **reference FPGA architecture**, similar to how a reference SoC helps you learn SoC design.

---

## Why SOFA Exists

Commercial FPGA architectures from:

* [AMD/Xilinx](https://www.amd.com?utm_source=chatgpt.com)
* [Intel FPGA](https://www.intel.com/content/www/us/en/products/details/fpga.html?utm_source=chatgpt.com)
* [Microchip FPGA](https://www.microchip.com/en-us/products/fpgas-and-plds.html?utm_source=chatgpt.com)

are proprietary.

You cannot easily see:

* Internal LUT design
* Routing architecture
* Configuration memory organization
* Bitstream generation process

SOFA exposes these details so you can learn and experiment.

---

# What SOFA Provides

A complete FPGA definition including:

```text
FPGA Fabric
│
├── Logic Blocks (LUTs + FFs)
├── Routing Network
├── Switch Boxes
├── Connection Boxes
├── Configuration Memory
├── IO Blocks
├── Clock Network
└── Bitstream Support
```

---

# SOFA Architecture Flow

```text
Architecture XML
        ↓
      VPR
        ↓
   OpenFPGA
        ↓
 FPGA RTL Generation
        ↓
 Bitstream Generation
        ↓
 FPGA Fabric
```

---

# Main Components

## 1. Logic Blocks

Contains:

```text
LUT
FF
MUX
Carry Chain
```

Example:

```text
Inputs
   ↓
  LUT
   ↓
   FF
   ↓
 Output
```

---

## 2. Routing Fabric

Contains:

* Routing channels
* Switch boxes
* Connection boxes

Example:

```text
CLB ---- SB ---- CLB
 |                 |
CB               CB
 |                 |
CLB ---- SB ---- CLB
```

This is where most FPGA area is spent.

---

## 3. Configuration Memory

Stores configuration bits.

Example:

```text
Bitstream
    ↓
Configuration Controller
    ↓
SRAM Cells
    ↓
Configure FPGA
```

---

## 4. Bitstream Support

SOFA can generate:

```text
Verilog Design
      ↓
Bitstream
      ↓
FPGA Configuration
```

This is a key learning feature because commercial FPGA bitstreams are usually undocumented.

---

# Why SOFA is Important for FPGA Architects

SOFA allows you to modify:

* LUT size
* Tile size
* Routing architecture
* Channel width
* Switch box topology
* Configuration network

and observe the effects.

Example experiments:

### Change LUT

```text
4-LUT
   ↓
6-LUT
```

Observe:

* Area
* Delay
* Routability

---

### Change Routing

```text
Channel Width = 16
        ↓
Channel Width = 32
```

Observe:

* Congestion
* Timing
* Area

---

# SOFA + RISC-V

A common use case:

```text
RISC-V CPU
      ↓
SOFA FPGA Fabric
      ↓
UART
SPI
GPIO
BRAM
DSP
```

You can implement soft RISC-V cores such as:

* PicoRV32
* VexRiscv

inside the generated FPGA.

---

# Why Learn SOFA?

For an FPGA architect, SOFA provides access to topics that are hidden in commercial devices:

| Topic                | Commercial FPGA | SOFA    |
| -------------------- | --------------- | ------- |
| LUT Architecture     | Hidden          | Visible |
| Routing Network      | Hidden          | Visible |
| Bitstream Format     | Hidden          | Visible |
| Configuration Memory | Hidden          | Visible |
| Tile Architecture    | Hidden          | Visible |
| FPGA RTL             | Hidden          | Visible |

---

# SOFA in Your Learning Path

```text
FPGA User
    ↓
FPGA Architecture
    ↓
CAD Algorithms (VPR)
    ↓
OpenFPGA
    ↓
SOFA
    ↓
Modify FPGA Fabric
    ↓
Build Custom FPGA
    ↓
Optimize for RISC-V
    ↓
Custom RISC-V FPGA Architect
```

### One-line Definition

**SOFA (Simple Open FPGA Architecture) is an open-source, fully customizable FPGA architecture built using OpenFPGA that allows engineers to study, modify, generate, and experiment with complete FPGA fabrics, routing networks, configuration systems, and bitstreams.**
