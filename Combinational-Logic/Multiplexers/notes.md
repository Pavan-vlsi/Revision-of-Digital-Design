# Multiplexers (MUX)

## 1. 4:1 Multiplexer

A multiplexer (MUX) is a combinational logic circuit that selects one
of several input signals and transfers the selected input to a single
output. The select lines determine which input is selected.

- Data inputs: I0, I1, I2, I3
- Select lines: S1, S0
- Output: Y

### Selection Table

| S1 | S0 | Output |
|----|----|--------|
| 0  | 0  | I0     |
| 0  | 1  | I1     |
| 1  | 0  | I2     |
| 1  | 1  | I3     |

### Boolean Expression

Y = I0·S1'·S0' + I1·S1'·S0 + I2·S1·S0' + I3·S1·S0

Each input is associated with a unique select-line combination.
Only the selected input determines the output.

## 2. 8:1 Multiplexer

An 8:1 MUX selects one of eight data inputs using three select lines.
The three select bits provide eight possible combinations (2³ = 8).

- Data inputs: I0–I7
- Select lines: S2, S1, S0
- Output: Y

### Selection Table

| S2 | S1 | S0 | Output |
|----|----|----|--------|
| 0  | 0  | 0  | I0     |
| 0  | 0  | 1  | I1     |
| 0  | 1  | 0  | I2     |
| 0  | 1  | 1  | I3     |
| 1  | 0  | 0  | I4     |
| 1  | 0  | 1  | I5     |
| 1  | 1  | 0  | I6     |
| 1  | 1  | 1  | I7     |

### Boolean Expression

Y = I0·S2'·S1'·S0' + I1·S2'·S1'·S0
  + I2·S2'·S1·S0' + I3·S2'·S1·S0
  + I4·S2·S1'·S0' + I5·S2·S1'·S0
  + I6·S2·S1·S0' + I7·S2·S1·S0

## 3. 8:1 MUX Using Two 4:1 MUXes and an OR Gate

An 8:1 MUX can be constructed using two 4:1 MUXes and one OR gate.
This demonstrates how smaller combinational circuits can be combined
to implement a larger circuit.

### Connections

- First MUX: Data inputs I0–I3.
- Second MUX: Data inputs I4–I7.
- Both MUXes share select lines S1 and S0.
- S2 and its complement control the enable inputs.
- The outputs of both MUXes connect to an OR gate.

### Working

- When S2 = 0, the first MUX selects an input from I0–I3.
- When S2 = 1, the second MUX selects an input from I4–I7.
- The OR gate combines the two MUX outputs to produce Y.

The enable logic must ensure that only the selected MUX contributes
to the output. The unselected MUX must produce logic 0 for this
OR-gate arrangement to work correctly.

## Proteus Implementation

All three circuits were designed and simulated in Proteus.
The designs were organized using parent and child sheets, allowing
the individual circuit designs to be reused as hierarchical blocks.

## Applications

- Digital data selection and routing
- Processor datapaths and control circuits
- Communication systems
- FPGA-based digital systems
- Implementing larger combinational circuits from smaller blocks
