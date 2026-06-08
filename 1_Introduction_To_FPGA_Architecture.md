
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

#### FPGA Fabric Architect focuses on:
* LUT architecture
* Logic clusters (CLBs)
* Routing architecture
* Switch boxes
* Configuration memory
* Bitstream architecture
* CAD algorithms (placement/routing)

### 1.4 Applications of FPGA:

FPGAs are used wherever **flexibility, parallel processing, low latency, and hardware acceleration** are required.

### 1. Embedded Systems

* Industrial controllers
* Smart sensors
* Data acquisition systems
* Real-time control systems

**Examples:**

* Motor control
* Robotics
* PLCs

---

### 2. RISC-V and SoC Prototyping

* Soft RISC-V processors
* Multi-core SoCs
* Custom instruction development
* Hardware/software co-design

**Examples:**

* PicoRV32
* VexRiscv
* Rocket Chip

---

### 3. Digital Signal Processing (DSP)

* FIR filters
* FFT processing
* Audio processing
* Video processing

**Advantages:**

* Massive parallelism
* Low latency

---

### 4. Artificial Intelligence (AI) & Machine Learning (ML)

* Neural network acceleration
* Edge AI
* Computer vision
* Inferencing engines

**Examples:**

* CNN accelerators
* Object detection
* Face recognition

---

### 5. Networking & Data Centers

* Packet processing
* Load balancing
* Network acceleration
* SmartNICs

**Examples:**

* 5G infrastructure
* High-speed routers
* Cloud acceleration

---

### 6. Telecommunications

* Software Defined Radio (SDR)
* Baseband processing
* 4G/5G systems
* Signal modulation/demodulation

---

### 7. Aerospace & Defense

* Radar systems
* Sonar systems
* Electronic warfare
* Satellite communications

**Why FPGA?**

* Reliability
* Real-time performance
* Reconfigurability

---

### 8. Automotive

* ADAS (Advanced Driver Assistance Systems)
* Autonomous driving
* Sensor fusion
* Automotive networking

---

### 9. Video and Image Processing

* Video encoding/decoding
* Image enhancement
* Surveillance systems
* Machine vision

---

### 10. Security and Cryptography

* AES acceleration
* RSA acceleration
* Secure boot
* HSMs (Hardware Security Modules)

**Relevant to your interests:**

* Secure FPGA fabrics
* FPGA Root of Trust
* Cryptographic accelerators

---

### 11. Medical Electronics

* MRI systems
* Ultrasound machines
* Medical imaging
* Patient monitoring

---

### 12. Test and Measurement

* Oscilloscopes
* Logic analyzers
* Protocol analyzers
* RF test equipment

---

### 13. High-Performance Computing (HPC)

* Scientific computing
* Financial modeling
* Genomics
* Hardware acceleration

---

### 14. FPGA Fabric Research

* Custom FPGA architectures
* OpenFPGA
* SOFA FPGA
* FPGA CAD research

This is where FPGA architects work.

---

### 15. Custom Hardware Accelerators

* AI accelerators
* Cryptography engines
* Compression engines
* Database accelerators

---

Understanding FPGA applications is important because **FPGA Fabric Architects design the fabric based on the needs of these workloads**. For example:

* AI workloads → More DSPs and BRAMs
* RISC-V SoCs → More logic and memory
* Networking → Faster routing and high-speed I/O
* Security → Secure bitstream and cryptographic blocks
* DSP → Optimized DSP tiles and routing networks

## FPGA Architecture

<img width="533" height="449" alt="image" src="https://github.com/user-attachments/assets/38ad7172-1f15-4901-9411-52897eeb9522" />

### FPGA Building Blocks

An FPGA is built from several programmable hardware blocks:

```text id="3b6xv7"
                 FPGA
                   │
    ┌──────────────┼──────────────┐
    │              │              │
   CLBs          BRAMs          DSPs
    │
    ├── LUTs
    ├── Flip-Flops
    └── Carry Chains

         + Routing Network +
         + Clock Network   +
         + IO Blocks       +
```

### Main Building Blocks

#### 1. LUT (Look-Up Table)

Implements combinational logic.

Examples:

* AND
* OR
* XOR
* Multiplexers
* ALU logic

---

#### 2. Flip-Flops (FFs)

Implement sequential logic.

Used for:

* Registers
* Counters
* FSMs
* Pipelines

---

#### 3. Carry Chains

Dedicated arithmetic hardware.

Used for:

* Adders
* Subtractors
* Comparators
* ALUs

---

#### 4. Routing Network

Connects all FPGA resources.

Contains:

* Switch boxes
* Connection boxes
* Routing tracks

---

#### 5. BRAM

Embedded memory blocks.

Used for:

* Instruction memory
* Data memory
* FIFOs

---

#### 6. DSP Blocks

Dedicated arithmetic engines.

Used for:

* Multiplication
* MAC operations
* Filters

---

## ALU Example

Suppose we have a simple ALU:

```verilog
module alu(
    input  [3:0] a,
    input  [3:0] b,
    input  [1:0] op,
    output reg [3:0] y
);

always @(*) begin
    case(op)
        2'b00: y = a + b;
        2'b01: y = a - b;
        2'b10: y = a & b;
        2'b11: y = a | b;
    endcase
end

endmodule
```

---

## How FPGA Implements This ALU

### Step 1: Logic Operations

Operations:

```text id="f8h15x"
AND
OR
MUX
```

are mapped into LUTs.

Example:

```text id="pw9j4v"
A ----\
        LUT ---- Result
B ----/
```

---

### Step 2: Addition/Subtraction

Addition:

```text id="74xt4g"
A + B
```

requires:

* XOR
* AND
* Carry propagation

FPGA uses:

```text id="5n4rdz"
LUT + Carry Chain
```

instead of implementing everything in LUTs.

Example:

```text id="x5up8e"
Bit0 ---- Carry ---- Bit1 ---- Carry ---- Bit2
```

This is much faster.

---

### Step 3: Operation Selection

The `case(op)` statement becomes a multiplexer.

```text id="gm7m6w"
Add Result ----\
Sub Result -----\
AND Result ------> MUX --> Y
OR Result -------/
```

MUXes are implemented using LUTs.

---

### FPGA Resource Mapping

| ALU Function               | FPGA Resource     |
| -------------------------- | ----------------- |
| AND                        | LUT               |
| OR                         | LUT               |
| XOR                        | LUT               |
| Multiplexer                | LUT               |
| Add                        | LUT + Carry Chain |
| Subtract                   | LUT + Carry Chain |
| Output Register (optional) | Flip-Flop         |

---

## ALU Inside a RISC-V CPU

For a RISC-V ALU:

```text id="d5bl5t"
ADD
SUB
AND
OR
XOR
SLT
SLL
SRL
SRA
```

Resource usage:

```text id="4b3o1r"
          ALU
           │
   ┌───────┼────────┐
   │       │        │
 LUTs   Carry    FFs
         Chain
```

---

### Application Mapping to FPGA Resources

| Application      | FPGA Resource Used |
| ---------------- | ------------------ |
| RISC-V CPU       | LUTs, FFs, BRAM    |
| AI/ML            | DSPs, BRAM, LUTs   |
| DSP Filters      | DSPs, BRAM         |
| Networking       | LUTs, BRAM         |
| Video Processing | DSPs, BRAM         |
| Security         | LUTs, DSPs         |
| Embedded Systems | LUTs, FFs, BRAM    |

---

### FPGA Architect's View

```text
Applications
     ↓
Requirements
     ↓
FPGA Resources
     ↓
LUTs
BRAMs
DSPs
IOs
Routing
Clock Network
     ↓
FPGA Fabric Architecture
```
