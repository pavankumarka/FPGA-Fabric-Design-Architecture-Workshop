
# Day1 Agenda:
1. [FGPA Introduction](#1-fpga-introduction)
2. [FPGA Design Methodologies](#2-FPGA-Design-methodology)
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

### RISC-V and SoC Prototyping

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


An **FPGA (Field Programmable Gate Array)** is a programmable digital device consisting of configurable logic resources, programmable interconnects, memory blocks, DSP blocks, clock networks, I/O blocks, and configuration memory. After synthesis and implementation, a **bitstream** configures these resources to implement the desired hardware circuit.

+---------------------------------------------------+
| IOB  IOB  IOB  IOB  IOB  IOB  IOB  IOB           |
+---------------------------------------------------+

| CLB | ROUTE | CLB | BRAM | CLB | DSP | CLB |

| ROUTE | ROUTE | ROUTE | ROUTE | ROUTE |

| CLB | CLB | CLB | CLB | CLB | CLB | CLB |

| ROUTE | ROUTE | ROUTE | ROUTE | ROUTE |

| CLB | DSP | CLB | BRAM | CLB | CLB | CLB |

+---------------------------------------------------+
| IOB  IOB  IOB  IOB  IOB  IOB  IOB  IOB           |
+---------------------------------------------------+

---

## Complete FPGA Architecture

```text
+--------------------------------------------------------------------+
|                        I/O BLOCKS (IOBs)                           |
+--------------------------------------------------------------------+

      Routing        Routing        Routing        Routing

+-----------+     +---------+     +-----------+     +---------+
|    CLB    |-----|  BRAM   |-----|    CLB    |-----|   DSP   |
+-----------+     +---------+     +-----------+     +---------+
      |                                   |
      |                                   |
      |                               Carry Chain
      |                                   |
+-----------+     +-----------+     +-----------+     +-----------+
|    CLB    |-----|    CLB    |-----|    CLB    |-----|    CLB    |
+-----------+     +-----------+     +-----------+     +-----------+

      Routing        Routing        Routing        Routing

+--------------------------------------------------------------------+
|                     Global Clock Network                           |
+--------------------------------------------------------------------+

Configuration SRAM distributed throughout the FPGA fabric
```

---

## FPGA Building Blocks

### 1. Configurable Logic Blocks (CLBs)

CLBs are the primary logic resources of an FPGA.

#### Contains

```text
CLB
├── LUTs
├── Multiplexers (MUXes)
├── Carry Chains
└── Flip-Flops (FFs)
```

#### Used For

* Combinational logic
* Sequential logic
* Arithmetic operations
* State machines
* CPU implementation

---

### LUT (Look-Up Table)

A LUT implements combinational logic.

Example functions:

```text
AND
OR
XOR
NOT
MUX
Comparator
```

#### Location

```text
Inside CLBs
```

---

### 3. Multiplexers (MUX)

Used for selecting signals.

Example:

```text
ADD Result ----\
SUB Result -----\
AND Result ------> MUX --> Output
OR Result -------/
```

#### Location

```text
Inside CLBs
```

---

### 4. Carry Chains

Dedicated arithmetic hardware for fast carry propagation.

Used for:

```text
Adders
Subtractors
Comparators
Counters
ALUs
```

#### Location

```text
Inside CLBs
Between vertically adjacent CLBs
```

---

### 5. Flip-Flops (FFs)

Used for sequential logic.

Applications:

```text
Registers
Counters
FSMs
Pipelines
CPU Registers
```

#### Location

```text
Inside CLBs
```

---

<img width="510" height="432" alt="image" src="https://github.com/user-attachments/assets/4f569bac-f6a5-411d-b9e8-4f157ab106e1" />


### 6. Programmable Routing Network

Connects all FPGA resources.

#### Contains

```text
Routing Network
├── Horizontal Wires
├── Vertical Wires
├── Switch Boxes
└── Connection Boxes
```

#### Purpose

```text
CLB ↔ CLB
CLB ↔ BRAM
CLB ↔ DSP
CLB ↔ IOB
```

#### Location

```text
Between FPGA resources
```

---

### 7. I/O Blocks (IOBs)

Interface between FPGA and external world.

Used for:

```text
GPIO
UART
SPI
I2C
DDR
Ethernet
```

#### Location

```text
Around FPGA perimeter
```

---

### 8. BRAM (Block RAM)

Dedicated memory blocks.

Used for:

```text
Instruction Memory
Data Memory
FIFO
Buffer
Cache
```

#### Location

```text
Dedicated BRAM columns
```

---

### 9. DSP Blocks

Dedicated arithmetic units.

Used for:

```text
Multiplication
MAC
FIR Filters
FFT
AI/ML Acceleration
```

#### Location

```text
Dedicated DSP columns
```

---

### 10. Clock Network

Distributes clocks across FPGA.

Contains:

```text
Global Clock Trees
Regional Clock Networks
Clock Buffers
PLLs
```

#### Purpose

```text
Low Skew
High-Speed Operation
```

#### Location

```text
Across entire FPGA
```

---

### 11. Configuration Memory

Usually SRAM cells.

Stores:

```text
LUT Contents
Routing Configuration
MUX Selections
IO Settings
BRAM Modes
DSP Modes
```

#### Location

```text
Distributed throughout FPGA
```

---

## FPGA Programming Flow

### Step 1: Write RTL

Example:

```verilog
assign y = a + b;
```

---

### Step 2: Synthesis

RTL is converted into FPGA resources.

```text
RTL
 ↓
LUTs
Carry Chains
MUXes
FFs
```

---

### Step 3: Place & Route

Tool decides:

```text
Which CLB?
Which Routing Path?
Which BRAM?
Which DSP?
Which IOB?
```

---

### Step 4: Bitstream Generation

```text
RTL
 ↓
Synthesis
 ↓
Place & Route
 ↓
Bitstream
```

---

### Step 5: Configure FPGA

```text
Bitstream
 ↓
Configuration SRAM
 ↓
FPGA Fabric Configured
```

---

## ALU Example

Consider a simple ALU:

```verilog
always @(*) begin
    case(op)
        2'b00: y = a + b;
        2'b01: y = a - b;
        2'b10: y = a & b;
        2'b11: y = a | b;
    endcase
end
```

---

## How FPGA Implements This ALU

### AND Operation

```verilog
y = a & b;
```

Implemented using:

```text
LUT
```

Location:

```text
Inside CLB
```

---

### OR Operation

```verilog
y = a | b;
```

Implemented using:

```text
LUT
```

Location:

```text
Inside CLB
```

---

### Addition

```verilog
y = a + b;
```

Implemented using:

```text
LUTs + Carry Chains
```

Example:

```text
Bit0 → Carry → Bit1 → Carry → Bit2 → Carry → Bit3
```

Location:

```text
Inside and between CLBs
```

---

### Subtraction

```verilog
y = a - b;
```

Implemented using:

```text
LUTs + Carry Chains
```

Location:

```text
Inside and between CLBs
```

---

### Operation Selection

The `case(op)` statement becomes a multiplexer.

```text
ADD Result ----\
SUB Result -----\
AND Result ------> MUX ---> Y
OR Result -------/
```

Location:

```text
Inside CLB
```

---

### Registered ALU Output

```verilog
always @(posedge clk)
    y <= result;
```

Implemented using:

```text
Flip-Flop
```

Location:

```text
Inside CLB
```

Clock supplied by:

```text
Global Clock Network
```

---

## ALU Physical Mapping Inside FPGA

```text
FPGA Pin
   │
  IOB
   │
Routing Network
   │
+------------------------------------------------+
|                    CLB                         |
|                                                |
| A ----> LUT ----\                              |
|                 MUX ----> FF ----> Output      |
| B ----> LUT ----/                              |
|                                                |
|       Carry Chain (for ADD/SUB)                |
+------------------------------------------------+
   │
Routing Network
   │
 IOB
   │
FPGA Pin
```

---

## If ALU Is Inside a RISC-V CPU

```text
RISC-V CPU
│
├── ALU
├── Register File
├── Control Unit
├── Instruction Decoder
└── Program Counter
```

For a RISC-V ALU: Instructions used

ADD
SUB
AND
OR
XOR
SLT
SLL
SRL
SRA

FPGA resources used:

| CPU Block           | FPGA Resource       |
| ------------------- | ------------------- |
| ALU                 | LUTs + Carry Chains |
| Registers           | FFs                 |
| Instruction Memory  | BRAM                |
| Data Memory         | BRAM                |
| Multiplier          | DSP                 |
| Control Logic       | LUTs                |
| Clocking            | Clock Network       |
| External Interfaces | IOBs                |
| Connectivity        | Routing Network     |

---

## Summary

When an ALU is synthesized:

| ALU Function                   | FPGA Block Used    |
| ------------------------------ | ------------------ |
| AND / OR / XOR                 | LUT                |
| Add / Subtract                 | LUT + Carry Chain  |
| Operation Select               | MUX                |
| Register Output                | FF                 |
| Signal Connections             | Routing Network    |
| External Pins                  | IOB                |
| Instruction/Data Storage (CPU) | BRAM               |
| Multiplication                 | DSP                |
| Clock Distribution             | Clock Network      |
| Resource Configuration         | Configuration SRAM |

The **bitstream programs the distributed configuration SRAM**, which configures every LUT, routing switch, MUX, FF, BRAM, DSP, and IOB to transform the generic FPGA fabric into the desired ALU or complete RISC-V processor.


## LUT explaination using 2X1 MUX

<img width="549" height="444" alt="image" src="https://github.com/user-attachments/assets/b00330a9-38b2-4c63-865b-8b2df7305887" />

How does a LUT look for a 2X1 mux on an FPGA?

From the diagram, we can see Look-up table with N-inputs can be used to implement any combinational function of N inputs.

To trace the diagram in-backwards or other way round, consider input S first, then A, followed by B, then output Z. 

each line is expanded into wider view.

A 2X1 mux will have 2 inputs, a select line and an output.

Above diagram is a connection of multiple Multiplexers. a 2x1 mux uses 2^3 - 1 2x1 mux

| Variables | Number of 2:1 MUXes |
| --------- | ------------------- |
| 1         | (2^1-1=1)           |
| 2         | (2^2-1=3)           |
| 3         | (2^3-1=7)           |
| 4         | (2^4-1=15)          |
| 6         | (2^6-1=63)          |

Internally it can be viewed as:
        
              MUX
             /   \
           MUX   MUX
          / \    / \
        MUX MUX MUX MUX

Number of 2:1 MUXes:

Level 1 : 4
Level 2 : 2
Level 3 : 1
----------------
Total   : 7

4+2+1=7=2^3−1

Eg2: 4-Input LUT

Stores:

2^4 = 16

configuration bits.

MUX tree:

Level 1 : 8
Level 2 : 4
Level 3 : 2
Level 4 : 1
----------------
Total   : 15

8+4+2+1=15=2^4-1 

### FPGA Architect View
A K-LUT is often modeled as:
- 2^K SRAM configuration bits
- 2^(K−1) 2:1 multiplexers

For heigher bits: 

| LUT Size | SRAM Bits | 2:1 MUXes |
| -------- | --------- | --------- |
| 4-LUT    | 16        | 15        |
| 5-LUT    | 32        | 31        |
| 6-LUT    | 64        | 63        |

## How Interconnects play the role in FPGA Programming.

<img width="709" height="524" alt="image" src="https://github.com/user-attachments/assets/4f2be055-b71f-484d-b04b-0ba682867fca" />

See F1 and F2 work.

  - 2 inputs x1 and x2 are the interconnects connected to F1 inside CLB that has LUT.
  
  - intermediate output F1 = x1 + x2 is connected to one of the interconnect.
  
  - x3 is drawn from one more interconnect (track the red line drawn over black )
  
  - F1 and x3 is connected to next CLB which has LUT.
  
  - F2 is the final output that has F1 + x3 = x1 + x2 + x3.

This is how an interconnect and CLB come together to make the FPGA work. 

## FPGA Programming:

1. The "'standard" Hardware description Language.
2. Many Tool provide front-ends of both verilog/VHDL.
3. High Level programming: C, C++, Python

This workshop uses Verilog HDL -> Synthesizable bitstream -> program FPGA.


