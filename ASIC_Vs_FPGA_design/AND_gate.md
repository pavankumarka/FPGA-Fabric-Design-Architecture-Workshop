A simple AND gate is implemented very differently in an ASIC versus an FPGA.

# AND Gate in ASIC

ASICs use actual transistor-based standard cells.

### RTL

```verilog
assign y = a & b;
```

### Synthesis Result

The synthesis tool maps it to an AND gate standard cell.

```text
      A
       \
        AND ---- Y
       /
      B
```

### CMOS Implementation

A 2-input AND gate is usually built as:

```text
AND = NAND + INV
```

Transistor level:

```text
A ----\
       NAND ---- INV ---- Y
B ----/
```

Building blocks used:

* PMOS transistors
* NMOS transistors
* Standard cells
* Metal routing

---

# AND Gate in FPGA

FPGA does not contain dedicated AND gates everywhere.

Instead it uses a LUT (Look-Up Table).

### RTL

```verilog
assign y = a & b;
```

### Synthesis Result

Mapped into a LUT.

```text
       A
        \
         LUT ---- Y
        /
       B
```

---

## LUT Truth Table

For a 2-input AND:

| A | B | Y |
| - | - | - |
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

The LUT stores:

```text
Address AB

00 -> 0
01 -> 0
10 -> 0
11 -> 1
```

Internally:

```text
      A
      |
      v
   +------+
B->| LUT  |--> Y
   +------+
```

Building blocks used:

* SRAM configuration bits
* LUT multiplexers
* Routing resources

---

# FPGA vs ASIC View

| Feature                 | ASIC          | FPGA              |
| ----------------------- | ------------- | ----------------- |
| Basic Building Block    | Standard Cell | LUT               |
| AND Gate Implementation | CMOS Gate     | LUT Configuration |
| Configuration           | Fixed         | Programmable      |
| Area                    | Smaller       | Larger            |
| Speed                   | Faster        | Slower            |
| Power                   | Lower         | Higher            |

---

# Architect's View

For the same Verilog:

```verilog
assign y = a & b;
```

### ASIC Flow

```text
Verilog
   ↓
Synthesis
   ↓
AND2X1 Standard Cell
   ↓
Layout
   ↓
Silicon
```

### FPGA Flow

```text
Verilog
   ↓
Synthesis
   ↓
LUT Mapping
   ↓
Placement
   ↓
Routing
   ↓
Bitstream
   ↓
FPGA Fabric
```

This example is often the first illustration used to explain the fundamental difference between **ASIC building blocks (transistors → standard cells)** and **FPGA building blocks (LUTs → programmable fabric)**.
