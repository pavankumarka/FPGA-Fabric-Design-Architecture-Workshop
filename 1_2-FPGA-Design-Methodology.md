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

