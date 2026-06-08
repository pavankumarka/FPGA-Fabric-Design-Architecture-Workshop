# 2. FPGA Design methodology

<img width="714" height="576" alt="image" src="https://github.com/user-attachments/assets/5daa8333-0b06-4bfb-8725-ef588d198117" />

## 1. Architecture Description

This is the planning stage where you decide what the hardware should do.

* Define the system requirements.
* Decide major blocks such as ALU, UART, memory, CPU, etc.
* Create a block diagram showing how modules connect.
* Think of this as the blueprint before construction starts.

---

## 2. RTL Design and Testbench

Here the hardware is described using Verilog or VHDL.

* Write synthesizable RTL code.
* Design modules such as ALU, counters, FSMs, memories, etc.
* Create a testbench to apply inputs and check outputs.
* No hardware is created yet; only the behavior is described.
* Xilinx Vivado can be used.

Example:

```verilog
assign y = a + b;
```

---

## 3. Behavioral Simulation

The RTL is simulated to verify functionality.

* Check whether the design behaves as expected.
* Verify logic before synthesis.
* Observe waveforms and debug errors.
* Easier and faster to fix bugs here than later.
* Xilinx Vivado can be used.

Example:

```text
A=5
B=3
ALU ADD
Output=8
```

---

## 4. Timing Constraints

Tell the FPGA tools how fast the design should run.

* Specify clock frequency.
* Define input and output timing requirements.
* Help tools optimize the design correctly.
* Incorrect constraints can cause timing failures.

Example:

```tcl
create_clock -period 10
```

This means a 100 MHz clock.

---

## 5. Pin Assignments

Map FPGA signals to physical FPGA pins.

* Connect design ports to FPGA package pins.
* Required for LEDs, switches, UART, SPI, etc.
* Usually done through constraints files.
* Ensures external hardware connects correctly.

Example:

```text
LED0 → PIN_A1
UART_TX → PIN_B2
```

---

## 6. Synthesis

RTL is converted into FPGA resources.

* Verilog/VHDL is translated into logic gates.
* Logic is mapped to LUTs, FFs, Carry Chains, BRAMs, and DSPs.
* Generates a netlist describing the hardware.
* Timing analysis is also performed.

Example:

```text
ADD
 ↓
LUTs + Carry Chain
```

---

## 7. Implementation (Place & Route)

The synthesized design is physically mapped into the FPGA.

### Place

* Decide which CLB, BRAM, or DSP will hold each logic block.

### Route

* Connect blocks using routing resources.

The tool tries to meet timing requirements while minimizing delay.

---

## 8. Timing Analysis

Checks whether all signals meet setup and hold requirements.

### Setup Time

Data must arrive before the clock edge.

### Hold Time

Data must remain stable after the clock edge.

Reports:

```text
Worst Negative Slack
Clock Frequency
Path Delays
```

If timing fails, the design may not work reliably.

---

## 9. Bitstream Generation

Creates the FPGA programming file.

* Converts implementation results into configuration bits.
* Describes LUT contents.
* Describes routing connections.
* Describes I/O settings.

Example files:

```text
.bit
.bin
.mcs
```

---

## 10. FPGA Programming

Load the bitstream into the FPGA.

* Configuration memory is programmed.
* LUTs, routing switches, FFs, BRAMs, and DSPs are configured.
* The FPGA now behaves like the designed hardware.
* This process can be repeated many times.

---

## 11. Hardware Verification

Test the design on the actual FPGA board.

* Observe LEDs, UART output, displays, etc.
* Compare actual results with simulation results.
* Measure performance and resource utilization.
* Fix issues and iterate if needed.

---

# Complete Flow

```text
Architecture Description
          ↓
RTL Design + Testbench
          ↓
Behavioral Simulation
          ↓
Timing Constraints
          ↓
Pin Assignments
          ↓
Synthesis
          ↓
Implementation
(Place & Route)
          ↓
Timing Analysis
          ↓
Bitstream Generation
          ↓
FPGA Programming
          ↓
Hardware Verification
```

### ALU Example Through the Flow

```text
ALU Verilog
      ↓
Behavioral Simulation
      ↓
Synthesis
      ↓
LUTs + Carry Chains + FFs
      ↓
Place & Route
      ↓
Bitstream
      ↓
Program FPGA
      ↓
ALU runs in hardware
```

This is the complete path from a Verilog description of an ALU to a working hardware implementation inside an FPGA.

## What cannot be Synthesised:

**Un-synthesisable constructs** are Verilog/SystemVerilog statements that work in simulation but cannot be converted into actual FPGA or ASIC hardware.

A synthesizer can only create real hardware such as:

* LUTs
* Flip-Flops
* Carry Chains
* BRAMs
* DSPs
* Gates and wires

If a construct has no equivalent hardware, it cannot be synthesized.

---

# 1. Delay Statements (`#100`)

❌ Not synthesizable

```verilog
a = 1'b1;
#100;
a = 1'b0;
```

Reason:

* FPGA hardware cannot wait an arbitrary simulation time.

✅ Use a counter instead:

```verilog
if(counter == 100)
    a <= 1'b0;
```

Hardware created:

* Counter
* Comparator
* Flip-flops

---

# 2. Initial Blocks

Usually ❌ not synthesizable (except some FPGA-specific memory initialization cases)

```verilog
initial begin
    count = 0;
end
```

Reason:

* Hardware does not execute software-like startup code.

✅ Use reset logic:

```verilog
always @(posedge clk) begin
    if(reset)
        count <= 0;
end
```

Hardware created:

* Flip-flops with reset

---

# 3. UDP (User Defined Primitives)

❌ Generally not synthesizable

```verilog
primitive my_and(y,a,b);
```

Reason:

* Synthesizers typically do not map arbitrary primitives to FPGA resources.

✅ Use RTL operators:

```verilog
assign y = a & b;
```

---

# 4. Runtime / Dynamic Memory Allocation

❌ Not synthesizable

Example (SystemVerilog):

```systemverilog
int dyn_array[];
dyn_array = new[100];
```

Reason:

* FPGA memory size must be known during synthesis.

✅ Use fixed-size memory:

```verilog
reg [7:0] mem [0:99];
```

Hardware created:

* BRAM
* Distributed RAM

---

# 5. Infinite Loops

❌ Not synthesizable

```verilog
always begin
    a = ~a;
end
```

Convert to finite loop.

Reason:

* Hardware resources would be infinite.

✅ Use finite loops:

```verilog
for(i=0; i<8; i=i+1)
```

The synthesizer can unroll this into hardware.

---

# 6. System Tasks

❌ Simulation only

```verilog
$display("Hello");
$monitor(...);
$finish;
```

Reason:

* No equivalent hardware exists.

Used only for:

* Testbenches
* Debugging

---

# 7. File Operations

❌ Not synthesizable

```verilog
$fopen(...)
$fscanf(...)
```

Reason:

* FPGA hardware cannot access simulator files.

---

# 8. Event Controls in Testbenches

❌ Simulation only

```verilog
@(posedge clk);
#10;
```

inside testbench stimulus.

Reason:

* Used by simulator, not hardware.

---

# Quick Rule

Ask yourself:

> "Can I point to actual hardware (LUT, FF, BRAM, DSP, wire) that implements this?"

If **yes** → synthesizable.

If **no** → simulation-only (unsynthesizable).

---

# Examples

| Construct      | Synthesizable? | Hardware Generated |
| -------------- | -------------- | ------------------ |
| `a & b`        | ✅              | LUT                |
| `a + b`        | ✅              | LUT + Carry Chain  |
| Counter        | ✅              | FFs + LUTs         |
| FSM            | ✅              | FFs + LUTs         |
| `#100`         | ❌              | None               |
| `$display`     | ❌              | None               |
| `$finish`      | ❌              | None               |
| Dynamic Array  | ❌              | None               |
| Infinite Loop  | ❌              | None               |
| Fixed-size RAM | ✅              | BRAM / LUT RAM     |

### ALU Example

This is synthesizable:

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

Because the synthesizer can map it to:

```text
ADD/SUB  -> Carry Chains + LUTs
AND/OR   -> LUTs
Selection-> MUXes
Register -> FFs (if added)
```


## Basys3 FPGA key components:

<img width="680" height="598" alt="image" src="https://github.com/user-attachments/assets/6b2d9a7b-f756-4ca8-a396-9769beeaf480" />

All of these correspond to real FPGA hardware resources.

## Basys 3 FPGA Board – Key Components

The board shown is the **Basys 3**, built around the **Artix-7 XC7A35T** FPGA.

## Main Components

### 1. Power Good LED

* Indicates the board is powered correctly.
* ON = power is available.

---

### 2. PMOD Connectors (2×)

* General-purpose expansion ports.
* Used to connect:

  * Sensors
  * LCDs
  * ADC/DAC modules
  * Custom hardware

---

### 3. Four-Digit Seven-Segment Display

```text
8888
```

Used for:

* Counters
* Timers
* Numeric displays
* ALU output display

---

### 4. FPGA Device (Artix-7)

The largest IC on the board.

Contains:

```text
CLBs
LUTs
Flip-Flops
Carry Chains
BRAM
DSP
Clock Resources
IO Blocks
```

This is where your Verilog design is implemented.

---

### 5. Slide Switches (16)

```text
SW15 SW14 ... SW1 SW0
```

Used as user inputs.

Examples:

* ALU operands
* Mode selection
* Enable signals

For an ALU:

```text
SW[3:0]  = A
SW[7:4]  = B
```

---

### 6. User LEDs (16)

```text
LED15 ... LED1 LED0
```

Used to display outputs.

Example:

```text
ALU Result → LEDs
```

ON = Logic 1

OFF = Logic 0

---

### 7. Push Buttons (5)

Buttons:

```text
BTNU (Up)
BTND (Down)
BTNL (Left)
BTNR (Right)
BTNC (Center)
```

Common uses:

* Reset
* Start
* Increment counter
* Change ALU operation

Example:

```text
BTNC = Reset
```

---

### 8. DONE LED

Indicates FPGA programming status.

```text
ON → Bitstream loaded successfully
OFF → FPGA not configured
```

---

### 9. FPGA Reset Button

Resets the FPGA configuration logic.

Used when:

* Reloading a design
* Recovering from errors

---

### 10. USB Host Port

Used for:

* USB keyboard
* USB mouse
* External USB devices

---

### 11. USB-HID Port

Provides USB device functionality.

Used in advanced projects.

---

### 12. VGA Connector

Used for video output.

Example resolutions:

```text
640x480
800x600
```

Projects:

* VGA games
* Graphics
* Text display

---

### 13. USB-JTAG/UART Port

Most important connector for beginners.

Used for:

### Programming FPGA

```text
Vivado
   ↓
Bitstream
   ↓
USB-JTAG
   ↓
FPGA
```

### Serial Communication

```text
FPGA ↔ UART ↔ PC
```

---

### 14. External Power Connector

Allows powering the board without USB.

Typically:

```text
5V DC
```

---

### 15. Power Switch

Turns board power ON/OFF.

---

### 16. System Clock Oscillator

Provides the FPGA clock.

Basys 3:

```text
100 MHz Clock
```

Used by:

```verilog
always @(posedge clk)
```

---

# ALU Example on Basys 3

Suppose you implement:

```verilog
assign y = a + b;
```

### Inputs

```text
SW[3:0]  -> A
SW[7:4]  -> B
```

### Operation Select

```text
BTNU -> ADD
BTND -> SUB
BTNL -> AND
BTNR -> OR
```

### Outputs

```text
LED[3:0] -> Result
```

or

```text
7-Segment Display -> Result
```

---

# Mapping to FPGA Resources

```text
Slide Switches
      │
      ▼
    IOBs
      │
      ▼
 Routing Network
      │
      ▼
     CLB
 ┌──────────┐
 │ LUTs     │
 │ Carry    │
 │ FFs      │
 └──────────┘
      │
      ▼
 Routing Network
      │
      ▼
    IOBs
      │
      ▼
 LEDs / 7-Segment
```

This makes the Basys 3 an excellent board for learning the complete flow:

```text
Verilog
   ↓
Simulation
   ↓
Synthesis
   ↓
Place & Route
   ↓
Bitstream
   ↓
Basys 3 FPGA
   ↓
LEDs / Display / VGA / UART
```

## Software links:

<img width="731" height="513" alt="image" src="https://github.com/user-attachments/assets/f543e671-70af-49f9-b35f-0119c95d1157" />

## Types of using FPGA control:

1. Local Access.
2. Remote Access.
   - Virtual I/O on FPGA Board.
   - Virtual I/O on Integrated Logic Analyzer.

in either case (1) and (2.1) the FPGA has to be connected to the system, in this workshop videos we cover both. But practically for Analysis/simulation purpose, we will use (2.2) remote access ILA approach, that will enable us an virtual reset for the architecture analysis we target using ILA (Integrated Logic Analyzer).
   
<img width="689" height="533" alt="image" src="https://github.com/user-attachments/assets/0534d403-5d1b-402b-859a-1518c11fa5c9" />


# Vivado Counter Design

Log into Lab session, open command prompt and run "vivado &" (without double quotes)

Use the UI option to create new project, add FPGA, add design and test bench files and simulate to obtain behavioral model of the 4-bit up counter.

A 4-bit up counter is implemented in Verilog HDL.

The counter:
- Increments on every positive edge of clock
- Resets when reset signal is active and when max count reached (15  = 0x0F)
- Displays waveform output

## up-counter Verilog design Code:
        
        `timescale 1ns / 1ps
        //////////////////////////////////////////////////////////////////////////////////
        // Company: 
        // Engineer: 
        // 
        // Create Date: 08.06.2026 08:33:11
        // Design Name: 
        // Module Name: counter_clk_div
        // Project Name: 
        // Target Devices: 
        // Tool Versions: 
        // Description: 
        // 
        // Dependencies: 
        // 
        // Revision:
        // Revision 0.01 - File Created
        // Additional Comments:
        // 
        //////////////////////////////////////////////////////////////////////////////////
        
        module counter_clk_div(
            input  wire clk,
            input  wire rst,
            output reg [3:0] counter_out
        );
        
        reg div_clk;
        reg [25:0] delay_count;
        
        // Clock Divider
        always @(posedge clk or posedge rst) begin
            if (rst) begin
                delay_count <= 26'd0;
                div_clk     <= 1'b0;
            end
            else begin
        
                // Simulation:
                if (delay_count == 26'd5)
        
                // Basys3 100MHz -> 1Hz:
                // if (delay_count == 26'd49_999_999)
        
                begin
                    delay_count <= 26'd0;
                    div_clk     <= ~div_clk;
                end
                else begin
                    delay_count <= delay_count + 1'b1;
                end
            end
        end
        
        // 4-bit Counter
        always @(posedge div_clk or posedge rst) begin
            if (rst)
                counter_out <= 4'd0;
            else
                counter_out <= counter_out + 1'b1;
        end
        
        endmodule

## up-counter Verilog test bench code:

       `timescale 1ns / 1ps
       //////////////////////////////////////////////////////////////////////////////////
       // Company: 
       // Engineer: 
       // 
       // Create Date: 08.06.2026 08:35:49
       // Design Name: 
       // Module Name: counter_clk_div_tb
       // Project Name: 
       // Target Devices: 
       // Tool Versions: 
       // Description: 
       // 
       // Dependencies: 
       // 
       // Revision:
       // Revision 0.01 - File Created
       // Additional Comments:
       // 
       //////////////////////////////////////////////////////////////////////////////////
       
       
       `timescale 1ns/1ps
       
       module counter_clk_div_tb;
       
       reg clk;
       reg rst;
       wire [3:0] counter_out;
       
       // DUT
       counter_clk_div dut (
           .clk(clk),
           .rst(rst),
           .counter_out(counter_out)
       );
       
       // 100 MHz Clock
       initial begin
           clk = 1'b0;
           forever #5 clk = ~clk;
       end
       
       // Test Sequence
       initial begin
       
           rst = 1'b1;
           #20;
       
           rst = 1'b0;
       
           // Run long enough to see multiple counts
           #5000;
       
           $finish;
       end
       
       // Console Output
       initial begin
       
           $display("--------------------------------------------");
           $display(" Time(ns) | Counter | Hex ");
           $display("--------------------------------------------");
       
           $monitor("%8t | %2d | 0x%h",
                     $time,
                     counter_out,
                     counter_out);
       end
       
       endmodule


# Behavioral Simulation

Behavioral simulation was performed in Vivado simulator (Run all) to verify the functionality of the counter before synthesis.

The waveform confirmed:
- Proper clock toggling
- Counter increment operation
- Reset functionality


<img width="1569" height="721" alt="image" src="https://github.com/user-attachments/assets/d0e2a758-9c7a-4f46-9706-5b406c294802" />


## Console output:

<img width="790" height="549" alt="image" src="https://github.com/user-attachments/assets/0ba3fda4-66b0-4a1e-83d8-994339b440c5" />
