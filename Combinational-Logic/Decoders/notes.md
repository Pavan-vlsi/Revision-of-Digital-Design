# Decoders

A decoder is a combinational circuit that converts an n-bit binary input into one of 2ⁿ output lines. For each valid input combination, the corresponding output is selected.

## 1. 2:4 Decoder

A 2:4 decoder uses 2 input lines to select one of 4 output lines.

- Inputs: A, B
- Outputs: D0, D1, D2, D3

| A | B | D0 | D1 | D2 | D3 |
|---|---|----|----|----|----|
| 0 | 0 | 1  | 0  | 0  | 0  |
| 0 | 1 | 0  | 1  | 0  | 0  |
| 1 | 0 | 0  | 0  | 1  | 0  |
| 1 | 1 | 0  | 0  | 0  | 1  |

**Boolean expressions:**

- D0 = A'B'
- D1 = A'B
- D2 = AB'
- D3 = AB

Each output represents one minterm of the two input variables.

## 2. Active-Low 2:4 Decoder
An active-low decoder produces a LOW output for the selected input combination, while the remaining outputs stay HIGH.
In this implementation, the outputs are active LOW. Therefore, the selected output is 0 rather than 1.

| A | B | D0 | D1 | D2 | D3 |
|---|---|----|----|----|----|
| 0 | 0 | 0  | 1  | 1  | 1  |
| 0 | 1 | 1  | 0  | 1  | 1  |
| 1 | 0 | 1  | 1  | 0  | 1  |
| 1 | 1 | 1  | 1  | 1  | 0  |

**Boolean expressions:**

- D0 = (A'B')'
- D1 = (A'B)'
- D2 = (AB')'
- D3 = (AB)'

The selected output is LOW for each input combination, while all other outputs remain HIGH.

## 3. Full Adder Using a 3:8 Decoder

A full adder adds three 1-bit inputs and produces Sum and Carry outputs.

- Inputs: A, B, Cin
- Outputs: Sum, Carry

The 3:8 decoder generates the eight minterms for the three inputs. The required decoder outputs are combined using OR gates to obtain Sum and Carry.

**Boolean functions:**

- Sum = Σm(1, 2, 4, 7)
- Carry = Σm(3, 5, 6, 7)

Equivalently:

- Sum = A ⊕ B ⊕ Cin
- Carry = AB + ACin + BCin

The decoder-based implementation generates both outputs from the same set of minterms.

## Proteus Implementation

The decoder circuits and the full adder using a 3:8 decoder were implemented in Proteus. The project is organized using a parent sheet and child sheets containing the individual circuits.

## Applications

- Memory address decoding
- Instruction decoding in processors
- Selecting one output from multiple lines
- Implementing combinational logic functions
- Arithmetic circuit implementation
