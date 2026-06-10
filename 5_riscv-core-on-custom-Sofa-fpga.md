# Day 5 - RISCV Core on Custom SOFA Fabric

The RVMYTH RISC-V processor core was successfully integrated with the custom SOFA FPGA fabric and implemented using the complete OpenFPGA and VTR design flow. The design progressed through architecture mapping, synthesis, placement, routing, and post-implementation verification stages within the open-source FPGA toolchain.

Various implementation reports, including resource utilization, timing analysis, routing statistics, and simulation waveforms, were generated and analyzed to validate the correctness of the processor implementation and its mapping onto the FPGA fabric. The results confirmed successful functionality of the RISC-V core while meeting the required timing constraints.

This work demonstrates the feasibility of deploying a processor on a custom FPGA architecture and provides practical insight into FPGA fabric design, CAD tool flows, logic mapping, routing, and architecture evaluation. The successful implementation establishes a foundation for future exploration of custom FPGA architectures, FPGA CAD research, and advanced RISC-V-based system development.


## Git repo to clone: where we will follow same steps as in SOFA counter/RISCV

<img width="1200" height="758" alt="image" src="https://github.com/user-attachments/assets/a51b2e01-717c-4b45-b93b-860cb03bd8d5" />

## we will need to change configuration files and source files:

<img width="1748" height="410" alt="image" src="https://github.com/user-attachments/assets/df7221fa-aee2-4131-b6c9-3848ede02783" />


<img width="1440" height="893" alt="image" src="https://github.com/user-attachments/assets/591ca7f3-e0ab-4590-b43f-8fc9a8839259" />


<img width="1242" height="848" alt="image" src="https://github.com/user-attachments/assets/8d6de28a-bd77-469e-b052-a5c59af65b76" />


<img width="1804" height="860" alt="image" src="https://github.com/user-attachments/assets/1d2797a9-540e-47a9-aa2a-7df45ed56582" />

configuration changes:

<img width="1750" height="842" alt="image" src="https://github.com/user-attachments/assets/67f09d29-8311-48fe-9efb-9e3bf9d654f4" />

## make openFPGA

<img width="1812" height="808" alt="image" src="https://github.com/user-attachments/assets/bc407293-c711-40b2-a612-52e64db37e3c" />


output folder:

<img width="1797" height="778" alt="image" src="https://github.com/user-attachments/assets/b32cba90-bad1-451b-8e8e-3f93cb2a0ba4" />


## Area analysis

<img width="1844" height="817" alt="image" src="https://github.com/user-attachments/assets/539a5c5d-b771-48fb-857c-33910c31b59e" />

## componenets used:

<img width="1041" height="831" alt="image" src="https://github.com/user-attachments/assets/6664fdf0-48b9-4a89-9765-2490948f473b" />


---

# SOFA RVMYTH Utilization Report

The utilization report shows the FPGA resource usage of the RVMYTH core after synthesis and mapping onto the SOFA FPGA architecture.

The design consumes LUTs, latches, CLBs, routing resources, and logic elements. This report helps in understanding the hardware cost of implementing the processor core on the FPGA fabric.

## Circuit Statistics

- Total Blocks: 5526
- Inputs: 2
- Latches: 1807
- Outputs: 8
- 0-LUTs: 4
- 4-LUTs: 3705

## Net Statistics

- Total Nets: 5518
- Average Fanout: 3.1
- Maximum Fanout: 1807
- Minimum Fanout: 1.0

## Timing Graph

- Timing Graph Nodes: 22705
- Netlist Clocks: 1

<img width="737" height="508" alt="image" src="https://github.com/user-attachments/assets/17be3dde-1973-4f0d-b3ef-595d39615bb9" />

*Detailed FPGA primitive block usage and logic element statistics for the RVMYTH implementation.*

---

# Constraints File

An SDC (Synopsys Design Constraints) file was created to define the clock timing constraints for the design.

## Constraint File Used

```tcl
create_clock -period 200 clk
set_input_delay -clock clk -max 0 [get_ports {*}]
set_output_delay -clock clk -max 0 [get_ports {*}]
```

<img width="932" height="217" alt="image" src="https://github.com/user-attachments/assets/712a55ec-d518-4c5e-ab60-5a3bb8fe44ee" />

# configuration file:

<img width="1772" height="857" alt="image" src="https://github.com/user-attachments/assets/60fb0ba7-81b5-4c36-bed0-8094a4fb3030" />

## hold and setup time reports:

<img width="1410" height="670" alt="image" src="https://github.com/user-attachments/assets/cc7c0deb-391d-44a2-9f0f-df9ca7d18b94" />

## files location:

<img width="1839" height="713" alt="image" src="https://github.com/user-attachments/assets/21510c6a-a5bd-42c7-aa3b-681c0fa58f57" />

## SLACK PASS:

<img width="1469" height="855" alt="image" src="https://github.com/user-attachments/assets/22f03308-1663-4ce2-9d3b-d01df128ec8a" />

## hold time met:

<img width="1492" height="858" alt="image" src="https://github.com/user-attachments/assets/fc883a1f-1f8f-4547-be03-48e0838c68de" />


The constraint file defines:

- Clock period
- Input delay constraints
- Output delay constraints

These constraints are used by the timing analysis engine during placement and routing.

<img width="940" height="149" alt="image" src="https://github.com/user-attachments/assets/189d0a21-364a-44cf-8984-dbb105813b27" />

*SDC constraints file used for RVMYTH implementation on the SOFA FPGA fabric.*

---

# Timing Analysis

Timing analysis was performed after placement and routing to verify whether the design satisfies setup and hold timing constraints.

The setup timing report shows that the data arrival time is within the required timing limits and timing slack is positive.

<img width="658" height="562" alt="image" src="https://github.com/user-attachments/assets/322adca8-4b7e-4e0d-9ce2-d97e25f2f13f" />

*Setup timing analysis report showing positive timing slack for the RVMYTH core.*



---

# Hold Timing Analysis

Hold timing analysis verifies that the data remains stable for the required duration after the clock edge.

<img width="703" height="608" alt="image" src="https://github.com/user-attachments/assets/56ddd848-a357-4390-9668-ffed0fdb4a0e" />

*Hold timing analysis report showing successful hold timing closure.*

---

# Post Implementation Simulation

Post implementation simulation was performed after synthesis, placement, and routing of the RVMYTH core.

<img width="1766" height="413" alt="image" src="https://github.com/user-attachments/assets/6c711f33-ae09-467d-9116-b31cc70cfe35" />


<img width="1769" height="857" alt="image" src="https://github.com/user-attachments/assets/5f30497b-75b2-4e7b-b229-f966a33a1ca3" />


<img width="1787" height="795" alt="image" src="https://github.com/user-attachments/assets/5586cb3b-a9d0-4c53-8875-a605011647ed" />


<img width="1617" height="838" alt="image" src="https://github.com/user-attachments/assets/ac17bcb1-c49f-4dd9-a56b-8f903855305a" />


<img width="1777" height="854" alt="image" src="https://github.com/user-attachments/assets/354a2598-71dd-43e0-bdce-1d640fa052c0" />


<img width="1644" height="868" alt="image" src="https://github.com/user-attachments/assets/c37024c0-53bc-4f3d-9796-9f64963080b0" />

changes:

<img width="1712" height="924" alt="image" src="https://github.com/user-attachments/assets/a8d62682-9bed-4805-acb5-b0845540ff0a" />


Run on Vivado for Behavioral simulation:

<img width="1296" height="584" alt="image" src="https://github.com/user-attachments/assets/c4e8b8f7-d3f0-4511-a303-d2f3526eef2a" />


Simulation:

<img width="1792" height="834" alt="image" src="https://github.com/user-attachments/assets/1de662ae-74de-4804-88fb-3a1900d50551" />

Test bench provides only clk and rst 

The generated waveform confirms the correct execution of the processor logic after FPGA implementation. The simulation validates that the synthesized and routed netlist behaves correctly under the given clock and reset conditions.

The waveform also demonstrates proper output transitions and stable processor execution after implementation.

<img width="973" height="258" alt="image" src="https://github.com/user-attachments/assets/0faf8ae4-f2db-4f7f-886a-d55028ed1691" />


*Post implementation simulation waveform of the RVMYTH core on SOFA FPGA fabric.*

---

# Observations

- The RVMYTH processor was successfully mapped onto the custom SOFA FPGA fabric.
- FPGA resource utilization increased significantly compared to smaller counter-based designs.
- Timing constraints were successfully met with positive setup and hold slack values.
- The OpenFPGA and VTR flow successfully generated all required reports and simulation outputs.
- Post implementation simulation verified the correctness of the synthesized FPGA netlist.

---

# Conclusion


The RVMYTH RISC-V processor was successfully mapped, synthesized, placed, and routed on the custom SOFA FPGA architecture using the OpenFPGA and VTR toolchain. Resource utilization reports, timing analysis results, and post-implementation simulation waveforms verified the correct functionality of the processor and confirmed that all design timing requirements were met.

This work demonstrated the complete open-source FPGA design flow, starting from RTL design and architecture exploration through synthesis, implementation, bitstream generation, and hardware verification. The successful integration of the RISC-V core on the SOFA FPGA fabric validates the capability of the architecture and highlights the effectiveness of modern open-source FPGA CAD tools for processor prototyping, FPGA architecture research, and custom FPGA development.

