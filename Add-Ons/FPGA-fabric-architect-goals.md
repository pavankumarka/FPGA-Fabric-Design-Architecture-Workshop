# **FPGA Fabric Design Architect roadmap**:

## FPGA User → FPGA Architect → SOFA Contributor → Custom RISC-V FPGA Architect

This roadmap is ordered so that each stage builds on the previous one.

# Phase 1: FPGA User

Goal: Learn to use existing FPGAs efficiently.

## 1. FPGA Fundamentals

* What is an FPGA?
* FPGA vs ASIC
* FPGA families
* FPGA fabric overview
* FPGA development flow

### Hands-on

* Blink LED
* Counter
* UART TX/RX

---

## 2. Verilog/SystemVerilog Design

* Combinational logic
* Sequential logic
* FSM design
* Parameterized modules
* Testbenches

### Hands-on

* ALU
* FIFO
* UART Controller

---

## 3. FPGA Architecture Basics

* LUTs
* Flip-Flops
* CLBs
* Routing
* BRAM
* DSP
* Clock Networks

### Hands-on

* Resource utilization analysis
* Timing report analysis

---

## 4. FPGA Design Flow

* Synthesis
* Mapping
* Placement
* Routing
* Bitstream generation

### Tools

* Vivado
* Quartus

---

## 5. FPGA Interfaces

* GPIO
* UART
* SPI
* I2C
* DDR basics

### Hands-on

* SPI Master
* I2C Controller

---

## 6. FPGA-Based SoC Design

* Soft processors
* Bus architectures
* Memory maps

### Hands-on

* RISC-V + UART + GPIO SoC

---

# Phase 2: Advanced FPGA Designer

Goal: Understand how FPGA resources work internally.

## 7. Logic Architecture

* LUT internals
* K-LUT design
* Logic clustering
* Carry chains

### Study

* Why commercial FPGAs use 6-LUTs

---

## 8. Routing Architecture

* Routing channels
* Switch boxes
* Connection boxes
* Routing flexibility

### Study

* Wilton routing
* Universal routing
* Subset routing

---

## 9. Configuration Architecture

* SRAM FPGA
* Flash FPGA
* Antifuse FPGA

### Study

* Configuration memory
* Configuration controllers

---

## 10. FPGA Memory Architecture

* BRAM
* Distributed RAM
* Memory hierarchy

---

## 11. DSP Architecture

* Multipliers
* MAC units
* DSP pipelines

---

## 12. Clocking Architecture

* Global clocks
* Regional clocks
* PLLs
* Clock distribution

---

## 13. I/O Architecture

* I/O tiles
* DDR interfaces
* LVDS
* High-speed I/O

---

# Phase 3: FPGA Architect

Goal: Design FPGA fabrics instead of merely using them.

## 14. Tile Architecture

* Logic tiles
* BRAM tiles
* DSP tiles
* IO tiles

### Project

Design a custom FPGA tile.

---

## 15. FPGA CAD Algorithms

* Technology Mapping
* Logic Packing
* Placement
* Routing

### Tools

* VPR
* VTR

This is the most important architect-level topic.

---

## 16. CAD-Aware FPGA Architecture

* Routability
* Timing closure
* Congestion optimization
* Architecture exploration

---

## 17. FPGA Physical Design

* Floorplanning
* Timing analysis
* Power analysis
* Clock planning

---

## 18. Bitstream Architecture

* Configuration frames
* Bitstream format
* Compression
* Encryption
* Authentication

### Security Topics

* Secure Boot
* Bitstream Protection

This aligns strongly with your embedded security background.

---

# Phase 4: OpenFPGA / SOFA Contributor

Goal: Build and modify actual FPGA fabrics.

## 19. VTR Framework

Learn:

* Architecture XML
* Placement
* Routing
* Timing models

### Tool

[VTR Project](https://verilogtorouting.org/?utm_source=chatgpt.com)

---

## 20. OpenFPGA Framework

Learn:

* Fabric generation
* Bitstream generation
* Architecture customization

### Tool

[OpenFPGA](https://openfpga.readthedocs.io/?utm_source=chatgpt.com)

---

## 21. SOFA FPGA Architecture

Learn:

* SOFA tiles
* Routing fabric
* Configuration memory
* Fabric hierarchy

### Project

Modify a SOFA architecture.

### Tool

[SOFA FPGA](https://github.com/LNIS-Projects/SOFA?utm_source=chatgpt.com)

---

## 22. FPGA Fabric Customization

Projects:

* Custom LUT size
* Custom routing architecture
* Custom BRAM tile
* Custom DSP tile

---

# Phase 5: Custom RISC-V FPGA Architect

Goal: Create FPGA fabrics optimized for RISC-V systems.

## 23. RISC-V Processor Architecture

Study:

* RV32I
* RV32IM
* Privileged Architecture
* Interrupts
* MMU basics

Projects:

* PicoRV32
* VexRiscv

---

## 24. RISC-V SoC Architecture

Components:

* CPU
* Cache
* UART
* SPI
* GPIO
* Timers

Project:
Custom SoC on FPGA.

---

## 25. Custom FPGA for RISC-V

Study:

* Mapping CPU to fabric
* Routing bottlenecks
* Memory placement
* Accelerator placement

Project:
Optimize fabric specifically for RISC-V workloads.

---

## 26. FPGA Accelerators

Examples:

* AES
* SHA
* AI/ML
* DSP
* Packet processing

Project:
RISC-V + Accelerator SoC.

---

## 27. Security-Aware FPGA Architecture

Topics:

* Secure boot
* Bitstream encryption
* FPGA root of trust
* HMAC authentication
* PUF-based key storage

This is a strong specialization for you.

---

## 28. Full Custom FPGA Fabric

Final Project:

```text
Custom FPGA Fabric
│
├── Logic Tiles
├── BRAM Tiles
├── DSP Tiles
├── IO Tiles
├── Clock Network
├── Configuration Network
├── Secure Bitstream Engine
│
└── RISC-V SoC
     ├── CPU
     ├── Cache
     ├── UART
     ├── SPI
     ├── GPIO
     ├── AES Accelerator
     └── AI Accelerator
```

# Final Career Progression

```text
FPGA User
    ↓
FPGA RTL Designer
    ↓
Advanced FPGA Designer
    ↓
FPGA Architecture Engineer
    ↓
FPGA CAD Engineer
    ↓
FPGA Fabric Architect
    ↓
VTR/OpenFPGA Engineer
    ↓
SOFA FPGA Contributor
    ↓
Custom FPGA Fabric Designer
    ↓
RISC-V FPGA SoC Architect
    ↓
Secure FPGA Architect
```

At the end of this flow, you are no longer just programming FPGAs—you are designing FPGA fabrics, generating bitstreams, modifying SOFA/OpenFPGA architectures, and building custom FPGA platforms optimized for RISC-V and security workloads.

This sequence takes you from FPGA architecture fundamentals to designing a complete custom FPGA fabric capable of hosting a RISC-V SoC.

Back to [MAIN PAGE](https://github.com/pavankumarka/FPGA-Fabric-Design-Architecture-Workshop/blob/main/README.md)
