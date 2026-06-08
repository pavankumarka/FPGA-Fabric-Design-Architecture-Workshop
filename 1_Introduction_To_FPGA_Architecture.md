
# Day1 Agenda:
1. [FGPA Introduction](#1-fpga-introduction)
2. FPGA Design Methodologies
3. Advantages
4. Architecture
5. FPGA Programming (Verilog, Vivado)

## 1. FPGA Introduction

### 1.1 History of programmable logic
1. Types of programmable logic devices:
  - PLA: Progammable logic arrays
        - has few programmable devices
  - CPLD: Complex programmable logic device
        - has less programmable devices compared to FPGA
  - FPGA: Field Programmable Gate Array
        - has more number of programmable devices compared to CPLD.

The idea behind all these programmable gate arrays is
   - Generate customizable hardware, i.e program and reprogram the device.
   - study the effects of area, speed, power of the digital circuits.

#### Basys-3: FPGA board used in this workshop: 

![Basys](https://github.com/pavankumarka/FPGA-Fabric-Design-Architecture-Workshop/blob/main/Add-Ons/1_FPGA_Basys.PNG)

### 1.2 What is FPGA?
- A "Field Programmable Gate Array" (FPGA) is an integrated circuit designed to be configured by a user/ ASIC designer after manufacturing.
- FPGA is a multiple time prgrammable and reprogrammable design, where as ASIC is one time program and manufacture design.
- FPGA configuration is specified using a Hardware Description Language (HDL) such as Verilog or VHDL, similar to an ASIC (Application-Specific Integrated Circuit).
- Logic design in an FPGA is different from an ASIC:
  - Uses Look-Up Tables (LUTs)
  - Uses Flip-Flops (FFs)
  - Uses Configurable Logic Blocks (CLBs)

### 1.3 Differnce between ASIC and FPGA?

The image highlights some fundamental differences between ASICs and FPGAs.

| Aspect            | ASIC                                                   | FPGA                                        |
| ----------------- | ------------------------------------------------------ | ------------------------------------------- |
| Full Form         | Application-Specific Integrated Circuit                | Field-Programmable Gate Array               |
| Design Flow       | RTL → Synthesis → Place & Route → Layout → Fabrication | RTL → Synthesis → Place & Route → Bitstream |
| Hardware          | Custom silicon created for one design                  | Pre-manufactured programmable chip          |
| Reprogrammable    | No                                                     | Yes                                         |
| Upfront Cost      | Very high (NRE, masks, fabrication)                    | Low                                         |
| Unit Cost         | Low at high volume                                     | Higher                                      |
| Performance       | Highest                                                | Lower than ASIC                             |
| Power Consumption | Lowest                                                 | Higher than ASIC                            |
| Time to Market    | Months to years                                        | Hours to weeks                              |
| Risk              | High (fabrication mistakes are costly)                 | Low (can reprogram)                         |

### Design Flow Comparison

#### ASIC

```text
RTL (Verilog/VHDL)
        ↓
Synthesis
        ↓
Gate-Level Netlist
        ↓
Place & Route
        ↓
Physical Layout (GDSII)
        ↓
Semiconductor Foundry
        ↓
Fabricated Chip
```

#### FPGA

```text
RTL (Verilog/VHDL)
        ↓
Synthesis
        ↓
Technology Mapping
        ↓
Placement
        ↓
Routing
        ↓
Bitstream Generation
        ↓
Program FPGA
```

### AND Gate Example

#### ASIC

```text
Verilog AND
      ↓
AND Standard Cell
      ↓
Transistors (CMOS)
```

Building blocks:

* Standard cells
* PMOS/NMOS transistors
* Metal routing

#### FPGA

```text
Verilog AND
      ↓
LUT Configuration
      ↓
Bitstream
```

Building blocks:

* LUTs
* Flip-flops
* Routing switches
* Configuration SRAM

### From an Architect's Perspective

#### ASIC Architect focuses on:

* Standard cells
* SRAM design
* Physical design
* Clock tree synthesis
* DFT
* Power optimization
* Advanced process nodes


