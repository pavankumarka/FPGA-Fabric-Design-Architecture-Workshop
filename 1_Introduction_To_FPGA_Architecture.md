
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

The idea behind all these programmable gate arrays is to
   - Generate customiable hardware, i.e program and reprogram the device.
   - study the effects of area, speed, power of the digital circuits.

#### Basys-3: FPGA board used in this workshop: 

![Basys](https://github.com/pavankumarka/FPGA-Fabric-Design-Architecture-Workshop/blob/main/pictures/1_FPGA_Basys.PNG)

### 1.2 What is FPGA?
- A "Field Programmable Gate Array" (FPGA) is an integrated circuit designed to be configured by a designer after manufacturing.
- FPGA configuration is specified using a Hardware Description Language (HDL) such as Verilog or VHDL, similar to an ASIC (Application-Specific Integrated Circuit).
- Logic design in an FPGA is different from an ASIC:
  - Uses Look-Up Tables (LUTs)
  - Uses Flip-Flops (FFs)
  - Uses Configurable Logic Blocks (CLBs)
