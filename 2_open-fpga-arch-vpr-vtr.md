# Day 2 - OpenFPGA, VPR and VTR Flow

## Introduction

Day 2 focused on understanding the open-source FPGA CAD flow using:
- OpenFPGA
- VPR (Versatile Place and Route)
- VTR (Verilog-To-Routing)

The complete flow from Verilog RTL to FPGA routing and timing analysis was explored. Timing constraints, post-synthesis simulation, power analysis and generated reports were also studied.

---

# Introduction to OpenFPGA

<img width="1029" height="710" alt="image" src="https://github.com/user-attachments/assets/e3cf4cd6-2e51-4755-ba39-8da174b7b836" />

OpenFPGA is an open-source FPGA framework used for:
- FPGA architecture exploration
- Bitstream generation
- FPGA fabric generation
- CAD automation
- Verification and testing

### difference bwtween standard FPGA flow vs Open FPGA.

<img width="1020" height="659" alt="image" src="https://github.com/user-attachments/assets/69ff8a0d-c0cf-4bbb-b166-811a6544dd61" />

### need for custom FPGA:

<img width="1014" height="731" alt="image" src="https://github.com/user-attachments/assets/b31dc025-4615-4196-93ba-56b15c6530b4" />

- For max performance.
- Reduce time to realize/simulate our own design.
- Since custom FPGA is costly, better to go with open FPGA.
  
The framework supports:
- Verilog-to-Bitstream flow
- Custom FPGA architecture exploration
- Automated FPGA fabric generation

---

#### Steps and types open FPGA supports

<img width="1047" height="785" alt="image" src="https://github.com/user-attachments/assets/4c4b2921-4f6e-4f0c-92b9-e3fc7418d2e8" />

In above picture, we follow and reach result analysis, by starting in 2 stages, one as intermediate stage (where first half of the files are available for VTR ), other one is starting from initial level (where all files are gereated/ added starting RTL) from begining of the flow.

### open FPGA documentation: (Both initiatives and installation steps)

<img width="1024" height="556" alt="image" src="https://github.com/user-attachments/assets/bfb782d3-ae50-47d3-9d31-2124128cc5e1" />

### FPGA design - electrical representation using code

<img width="735" height="462" alt="image" src="https://github.com/user-attachments/assets/a7779a59-0fc9-482b-9476-26526de9ab23" />

## VTR - Verilog to Routing is the stage in the Open FPGA flow, using specific tool to generate the output.

<img width="1086" height="674" alt="image" src="https://github.com/user-attachments/assets/7eae6423-c639-44c0-bfde-e928839bd80d" />

### VTR tools: Automated (OdinII -> ABC -> VPR)

<img width="635" height="466" alt="image" src="https://github.com/user-attachments/assets/fc9c40e9-0409-41a5-88e2-7abb2b12f355" />

#### 2 stage flow: we follow in this workshop.

<img width="664" height="454" alt="image" src="https://github.com/user-attachments/assets/6085bfff-38f7-476a-8105-6ed6f56b24df" />

#### steps to follow:

<img width="1207" height="790" alt="image" src="https://github.com/user-attachments/assets/d6e09c94-5bcb-4fdd-8a7a-f8f8a95aa442" />

<img width="587" height="413" alt="image" src="https://github.com/user-attachments/assets/0fc1310e-8e0f-4e9c-9557-d2f64b4e1571" />

## Introduction to VPR

VPR (Versatile Place and Route) is an open-source CAD tool used for Net-list associated :

1. Packing  
2. Placement  
3. Routing  
4. Timing Analysis  

---

## VPR stages:

<img width="620" height="411" alt="image" src="https://github.com/user-attachments/assets/232aa99c-0fbb-4a6b-88f8-417bf4a88360" />

<img width="543" height="387" alt="image" src="https://github.com/user-attachments/assets/4848a1ac-3b8b-4e70-8290-4914eb10d6c6" />

<img width="1537" height="835" alt="image" src="https://github.com/user-attachments/assets/dd803ae0-88ac-459c-8b1c-3fcb15ad1e39" />

#### VTR_ROOT: location of tool installed

<img width="998" height="561" alt="image" src="https://github.com/user-attachments/assets/15151ad8-f7b1-424e-a826-43179a16438d" />

<img width="989" height="563" alt="image" src="https://github.com/user-attachments/assets/0ab93f16-0649-4a30-b65b-f58273369eea" />

#### Netlist generated technology mapping file

<img width="1482" height="1016" alt="image" src="https://github.com/user-attachments/assets/e540f2ee-c5ca-407d-ae94-e57568b6bb98" />

##### EArch is 40nm Technology mapping architecture driven file

linking XML to Placement of FPGA Architecture.

<img width="1188" height="839" alt="image" src="https://github.com/user-attachments/assets/78798610-f2fd-4280-8a93-44d77a4daf4a" />

- EArch.xml = Architecture File
- Blif = design / Module details
- route-chan-width = Routing channel Architecture channel width. 

# VPR Flow Command

```bash
$VTR_ROOT/vpr/vpr \
$VTR_ROOT/vtr_flow/arch/timing/EArch.xml \
<blif-file-path> \
--route_chan_width 100 \
--disp on
```

---

# VPR Architecture Flow

The VPR flow performs:

## Packing
Combines logic primitives into FPGA logic blocks.

## Placement
Places logic blocks inside FPGA grid.

## Routing
Creates interconnections between FPGA logic blocks.

## Timing Analysis
Analyzes setup and hold timing paths.

---

# VPR GUI Visualization

VPR GUI was used to visualize:
- FPGA grid
- Routing resources
- Logic placement
- Nets and critical paths

## VPR Visualization

<img width="940" height="771" alt="image" src="https://github.com/user-attachments/assets/af78fc1d-c4be-40b9-9910-12a2a8a96c13" />


*VPR placement and routing visualization.*

---

# EArch FPGA Architecture Analysis using VPR

The `EArch.xml` FPGA architecture file was analyzed using the VPR flow. The architecture visualization, routing resources, nets, logical connections and timing reports were generated and studied.

The VPR flow was executed using the following command:

```bash
$VTR_ROOT/vpr/vpr \
$VTR_ROOT/vtr_flow/arch/timing/EArch.xml \
$VTR_ROOT/vtr_flow/benchmarks/blif/tseng.blif \
--route_chan_width 100 \
--disp on
```
<img width="642" height="209" alt="image" src="https://github.com/user-attachments/assets/03cb25dd-fcb2-4f99-8710-ef0a2b624990" />

### follow cmd prompt to run in command from your working directory of your choice.

<img width="1549" height="673" alt="image" src="https://github.com/user-attachments/assets/46fe7bfb-f752-4011-a5a3-622617ebc0b4" />

Initial Placement is done and paused (check cmd prompt)

#### Further Zoom in to see what type of cell is that?

<img width="1838" height="756" alt="image" src="https://github.com/user-attachments/assets/30a89342-4ce7-4b8f-90d5-e8ed85d4ca7f" />

#### click on proceed to see following step:

<img width="1849" height="826" alt="image" src="https://github.com/user-attachments/assets/23c8e49e-b4ca-482d-baf1-a28bd52e18b9" />

#### further routing is shown above and entire structure of FPGA architecture is shown below

<img width="1591" height="857" alt="image" src="https://github.com/user-attachments/assets/d083661d-23be-4cf1-9190-4d582b5ce166" />

<img width="1531" height="865" alt="image" src="https://github.com/user-attachments/assets/e82891d2-5b42-4aa4-9b95-73a6f9766b45" />

#### congestion percentage wrt color is shown below:

<img width="1920" height="838" alt="image" src="https://github.com/user-attachments/assets/9625e4e9-b5d9-4c66-96ce-ddbcc1a2a43c" />

#### critical path is shown below:

<img width="1920" height="955" alt="image" src="https://github.com/user-attachments/assets/08a597b4-8a6d-49e7-aa5e-f0b67dfdbfa3" />

### block critical view :

<img width="1366" height="728" alt="image" src="https://github.com/user-attachments/assets/c7d04efa-be87-4a69-a5bb-28b1c51b8039" />

---

# FPGA Architecture Visualization

The FPGA architecture generated using `EArch.xml` contains:
- Logic blocks
- Routing channels
- Switch blocks
- Interconnect resources
- FPGA grid structure


# Nets Analysis

The nets report contains:
- Source and destination nodes
- Interconnect paths
- Net routing information
- Routing resource usage

## Nets Report

<img width="940" height="720" alt="image" src="https://github.com/user-attachments/assets/709a35a3-7938-491d-8c06-9a9130a1cfbf" />

*Net connections generated after routing.*

---

# Logical Connections

Logical connections show:
- Signal interconnections
- Routing connectivity
- Logic block communication

## Logical Connections Report

<img width="940" height="709" alt="image" src="https://github.com/user-attachments/assets/cdf823c2-2ea1-4c48-85c4-6ad9fe6846de" />

*Logical interconnections generated during routing.*

---

# Critical Path Analysis

Critical path analysis determines:
- Longest timing path
- Maximum propagation delay
- Maximum operating frequency

The critical path directly impacts FPGA performance.

## Critical Path Report

<img width="940" height="711" alt="image" src="https://github.com/user-attachments/assets/44e6e49c-3f2b-412e-81ba-1414fa151c5b" />


*Critical timing path generated during timing analysis.*

---

# Routing Utilization

Routing utilization shows:
- Channel occupancy
- Routing efficiency
- Congestion distribution
- Resource utilization

## Routing Utilization Report

<img width="940" height="721" alt="image" src="https://github.com/user-attachments/assets/42dc365d-d40b-463f-8e63-024111186a4c" />

*Routing utilization generated after placement and routing.*

---

# Timing Analysis using Constraints

Timing constraints were added using an SDC file.

The constraints file defines:
- Clock period
- Input delays
- Output delays

---

# SDC Constraint File

## Constraint File

```tcl
create_clock -period 10 -name pclk
set_input_delay -clock pclk -max 0 [get_ports {*}]
set_output_delay -clock pclk -max 0 [get_ports {*}]
```

---

# Running VPR with Constraints

```bash
$VTR_ROOT/vpr/vpr \
$VTR_ROOT/vtr_flow/arch/timing/EArch.xml \
$VTR_ROOT/vtr_flow/benchmarks/blif/tseng.blif \
--route_chan_width 100 \
--sdc_file tseng.sdc \
--disp on
```

---

# Setup Timing Analysis

Setup timing checks whether data reaches destination registers before the active clock edge.

After adding constraints:
- Setup slack improved
- Timing closure was achieved
- Violations were reduced

## Setup Timing Report

<img width="940" height="486" alt="image" src="https://github.com/user-attachments/assets/d1ab7bd8-25ce-4826-8ce1-c80a23df133c" />

*Setup timing report after applying timing constraints.*

---

# Hold Timing Analysis

Hold timing ensures data remains stable after the active clock edge.

## Hold Timing Report

<img width="940" height="194" alt="image" src="https://github.com/user-attachments/assets/eb897b40-8f6c-4ddf-98ee-b4b0dee00bfa" />

*Hold timing report generated using VPR timing analysis.*

---

# Introduction to VTR

VTR (Verilog-To-Routing) is a complete open-source FPGA CAD flow.

The VTR flow performs:
- RTL Elaboration
- Synthesis
- Technology Mapping
- Packing
- Placement
- Routing
- Timing Analysis

Tools involved:
- ODIN II
- ABC
- VPR

---

# VTR Flow Command

```bash
$VTR_ROOT/vtr_flow/scripts/run_vtr_flow.py \
counter.v \
$VTR_ROOT/vtr_flow/arch/timing/EArch.xml \
-temp_dir . \
-route_chan_width 100
```

---

# Counter Design for VTR Flow

The following counter design was used for VTR implementation.

## Counter Verilog Code

```verilog
/*Important: Once you run ./a.out, it will keep running infinitely, because it is in an always block. You need to hit Ctrl + Z to stop it, else, the vcd will become a large file and will never end.
*/

module up_counter (
out      ,
enable   ,
clk      ,
reset
);

output [3:0] out;

input enable, clk, reset;

reg [3:0] out;

always @(posedge clk)

if (reset) begin
    out = 4'b0 ;
end

else if (enable) begin
    out = out + 1;
end

endmodule
```

---

# VTR Flow Stages

The VTR flow performed the following stages:

1. Elaboration and Synthesis using ODIN II  
2. Logic Optimization using ABC  
3. Packing using VPR  
4. Placement using VPR  
5. Routing using VPR  
6. Timing Analysis  

---

# Generated VTR Outputs

The VTR flow generated:
- `.net`
- `.place`
- `.route`
- `.blif`
- Timing reports
- Routing reports
- Placement reports

---

# Nets and Logical Connections

The generated reports included:
- Nets
- Routing utilization
- Critical paths
- Logical interconnections

## Nets Report

<img width="940" height="691" alt="image" src="https://github.com/user-attachments/assets/fcb0ac03-e295-4f8c-a568-46af29977e44" />

*Generated net connections*

## Logical Connections

<img width="940" height="756" alt="image" src="https://github.com/user-attachments/assets/f27bb6e5-088c-49f3-8603-83bcca565393" />

*Logical routing connections generated by VPR.*

---

# Critical Path Analysis

Critical path analysis was performed after routing.

The critical path determines:
- Maximum operating frequency
- Worst-case delay path

## Critical Path Report

!<img width="940" height="782" alt="image" src="https://github.com/user-attachments/assets/0cb2e8be-232b-4ce8-9d5f-af98a2b580e7" />


*Critical timing path generated during routing.*

---

# Timing Analysis using Constraints

Timing constraints were added using `.sdc` file.

The constraints define:
- Clock period
- Input delays
- Output delays

---
# Setup Timing Report

## Setup Timing

<img width="940" height="473" alt="image" src="https://github.com/user-attachments/assets/789f07a7-4fdf-4651-bcdc-943e2f095a66" />


*Setup timing report before applying constraints.*

---

# Hold Timing Report

## Hold Timing

<img width="940" height="550" alt="image" src="https://github.com/user-attachments/assets/702ba1e6-d8ab-4793-a580-681d6d97afb0" />


*Hold timing report generated by VPR before constraints.*

---

# SDC Constraint File

## Constraint File

```tcl
create_clock -period 10 up_counter_clk
set_input_delay -clock up_counter_clk -max 0 [get_ports {*}]
set_output_delay -clock up_counter_clk -max 0 [get_ports {*}]
```

---

# Running VPR with Constraints

```bash
$VTR_ROOT/vpr/vpr \
$VTR_ROOT/vtr_flow/arch/timing/EArch.xml \
counter.pre-vpr.blif \
--route_chan_width 100 \
--sdc_file counter.sdc
```

---

# Setup Timing Report

After adding timing constraints:
- Setup slack improved
- Timing requirements were met

## Setup Timing

<img width="940" height="619" alt="image" src="https://github.com/user-attachments/assets/71a1a2fa-7149-4880-9904-13b02eb13a0b" />


*Setup timing report after applying constraints.*

---

# Post Synthesis Simulation

Post synthesis simulation was performed using:
- Generated post synthesis netlist
- SDF timing file
- Vivado simulator

The generated files:
- `up_counter_post_synthesis.v`
- `up_counter_post_synthesis.sdf`

---

# Generating Post Synthesis Netlist

```bash
$VTR_ROOT/vpr/vpr \
$VTR_ROOT/vtr_flow/arch/timing/EArch.xml \
counter.pre-vpr.blif \
--gen_post_synthesis_netlist on
```

---

# Testbench for Post Synthesis Simulation

## Counter Testbench

```verilog
`timescale 1ns/1ps

module upcounter_testbench();

reg clk, reset, enable;
wire [3:0] out;

up_counter dut(
    .\up_counter^enable (enable),
    .\up_counter^clk (clk),
    .\up_counter^reset (reset),
    .\up_counter^out~0 (out[0]),
    .\up_counter^out~1 (out[1]),
    .\up_counter^out~2 (out[2]),
    .\up_counter^out~3 (out[3])
);

initial $sdf_annotate("up_counter_post_synthesis.sdf", dut);

initial begin

clk=0;
enable=0;
reset=1;

#20;

reset=0;
enable=1;

end

always
#5 clk=~clk;

endmodule
```

---

# Post Synthesis Simulation Results

The generated post synthesis simulation verified:
- Timing behavior
- Routing delays
- Gate-level functionality

## Post Synthesis Waveform

<img width="871" height="278" alt="image" src="https://github.com/user-attachments/assets/b656b2b0-47f4-4870-b87b-b8f8eaeb0307" />


*Post synthesis simulation waveform.*

---

# Power Analysis using VTR

Power estimation was performed using VTR power analysis flow.

The flow estimated:
- Dynamic power
- Routing power
- Clock power
- Leakage power

---

# Power Analysis Command

```bash
$VTR_ROOT/vtr_flow/scripts/run_vtr_flow.py \
counter.v \
$VTR_ROOT/vtr_flow/arch/timing/k6_frac_N10_mem32K_40nm.xml \
-power \
-temp_dir . \
-route_chan_width 100
```

---

## stdout.log report

<img width="940" height="389" alt="image" src="https://github.com/user-attachments/assets/15846909-5252-489f-a236-85ffe7b730ce" />

*stdout.log report generated using VTR.*

# Power Report

## Power Analysis

<img width="940" height="463" alt="image" src="https://github.com/user-attachments/assets/a3728e51-12e1-46be-b4a8-7c16d556aec0" />

*Power estimation report generated using VTR.*

---

# VTR Generated Reports

Generated reports included:
- Timing reports
- Routing reports
- Power reports
- Placement reports
- Post synthesis netlists

---

# Important Commands Used

## Running VTR Flow

```bash
$VTR_ROOT/vtr_flow/scripts/run_vtr_flow.py \
counter.v \
$VTR_ROOT/vtr_flow/arch/timing/EArch.xml \
-temp_dir . \
-route_chan_width 100
```

---

## Running VPR GUI

```bash
$VTR_ROOT/vpr/vpr \
$VTR_ROOT/vtr_flow/arch/timing/EArch.xml \
counter.pre-vpr.blif \
--route_chan_width 100 \
--disp on
```

---

## Running VPR with Constraints

```bash
$VTR_ROOT/vpr/vpr \
$VTR_ROOT/vtr_flow/arch/timing/EArch.xml \
counter.pre-vpr.blif \
--route_chan_width 100 \
--sdc_file counter.sdc
```

---

## Generating Post Synthesis Netlist

```bash
$VTR_ROOT/vpr/vpr \
$VTR_ROOT/vtr_flow/arch/timing/EArch.xml \
counter.pre-vpr.blif \
--gen_post_synthesis_netlist on
```

