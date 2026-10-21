# De-Mux and Implementation of Boolean functions using Mux and De-Mux

## 1. Full Adder Using 4:1 Multiplexers

A full adder is a combinational circuit that adds three 1-bit inputs
(A, B, Cin) and produces two outputs: Sum and Carry.

### Boolean Expressions

- Sum = A ⊕ B ⊕ Cin
- Carry = AB + ACin + BCin

### Design Using K-Maps

K-maps were used to derive the required data-input expressions for
the 4:1 multiplexers.

- Select lines: A and B
- Data input variable: Cin
- First MUX output: Sum
- Second MUX output: Carry

For each combination of A and B, the K-maps determine the required
MUX data input as a function of Cin.

### MUX Input Table

| A | B | Sum input | Carry input |
|---|---|-----------|-------------|
| 0 | 0 | Cin       | 0           |
| 0 | 1 | Cin'      | Cin         |
| 1 | 0 | Cin'      | Cin         |
| 1 | 1 | Cin       | 1           |

The table gives the data inputs selected for each A, B combination.
Cin' represents the complement of Cin.

### Proteus Implementation

Implemented the Full Adder using two 4:1 MUX blocks. A and B are
connected to the select lines of both MUXes, while the derived data
inputs generate the Sum and Carry outputs.

---

## 2. Full Adder Using a 1:8 Demultiplexer

A 1:8 demultiplexer routes its data input to one of eight outputs
according to three select lines.

### Design Approach

The full adder has three inputs: A, B and Cin. Their eight possible
combinations correspond to minterms from m0 to m7.

The DEMUX outputs were combined using OR gates to implement Sum
and Carry.

- Sum = Σm(1, 2, 4, 7)
- Carry = Σm(3, 5, 6, 7)

These minterm expressions assume A, B and Cin are ordered from
most significant to least significant bit.

### Proteus Implementation

Implemented the Full Adder using a 1:8 DEMUX and OR gates to
combine the required outputs for Sum and Carry.

---

## 3. 1:4 Demultiplexer

A 1:4 demultiplexer routes one data input to one of four outputs
using two select lines.

### Inputs and Outputs

- Data input: D
- Select lines: S1, S0
- Outputs: Y0–Y3

### Selection Table

| S1 | S0 | Selected Output |
|----|----|-----------------|
| 0  | 0  | Y0              |
| 0  | 1  | Y1              |
| 1  | 0  | Y2              |
| 1  | 1  | Y3              |

---

## 4. 1:8 Demultiplexer

A 1:8 demultiplexer routes one data input to one of eight outputs
using three select lines.

### Selection Table

| S2 | S1 | S0 | Selected Output |
|----|----|----|-----------------|
| 0  | 0  | 0  | Y0              |
| 0  | 0  | 1  | Y1              |
| 0  | 1  | 0  | Y2              |
| 0  | 1  | 1  | Y3              |
| 1  | 0  | 0  | Y4              |
| 1  | 0  | 1  | Y5              |
| 1  | 1  | 0  | Y6              |
| 1  | 1  | 1  | Y7              |

The select lines determine which output receives the input data,
assuming an active-high DEMUX.

---

## Proteus Implementation

The circuits were designed and organized in Proteus using parent
and child sheets, allowing circuit blocks to be reused in larger
designs.

## Applications

- Arithmetic circuits
- Digital data distribution
- Boolean function implementation using minterms
- Modular combinational circuit design
