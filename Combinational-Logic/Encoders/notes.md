# Encoders

An encoder is a combinational logic circuit that converts an active input into a coded binary output. An encoder with 2ⁿ input lines generally produces n output bits, assuming only one input is active at a time.

## 1. 8-to-3 Encoder

An 8-to-3 encoder converts one of eight active input lines into a 3-bit binary code.

- Inputs: D0–D7
- Outputs: x, y, z

### Boolean Expressions

- `x = D4 + D5 + D6 + D7`
- `y = D2 + D3 + D6 + D7`
- `z = D1 + D3 + D5 + D7`

Here, `+` represents the OR operation.

### Working

When one input is active, the outputs represent the binary index of that input.

For example, when `D5 = 1` and all other inputs are 0, the output is `101`.

A basic encoder assumes that only one input is active at a time. Simultaneous active inputs can produce an ambiguous output.

## 2. 4-to-2 Priority Encoder

A priority encoder produces the binary code of the highest-priority active input. Unlike a basic encoder, it can handle multiple active inputs.

- Inputs: D0–D3
- Outputs: x, y
- Valid output: V

Priority order: `D3 > D2 > D1 > D0`

### Boolean Expressions

- `x = D2 + D3`
- `y = D3 + D1·D2'`
- `V = D0 + D1 + D2 + D3`

### Working

- If `D3 = 1`, the output is `11`, regardless of the other inputs.
- Otherwise, if `D2 = 1`, the output is `10`.
- Otherwise, if `D1 = 1`, the output is `01`.
- If only `D0 = 1`, the output is `00`.
- If all inputs are 0, `V = 0`, indicating that no valid input is present.

The valid output distinguishes an active `D0` input from the condition where all inputs are 0.

## 3. Octal-to-BCD Encoder

An octal-to-BCD encoder converts an active octal input (0–7) into its corresponding BCD output.

Since octal digits range from 0 to 7, their decimal values fit within a single BCD digit.

- Inputs: 0–7 (one active input at a time)
- Outputs: Four BCD bits

### Conversion Table

| Active Input | BCD Output |
|--------------|------------|
| 0            | 0000       |
| 1            | 0001       |
| 2            | 0010       |
| 3            | 0011       |
| 4            | 0100       |
| 5            | 0101       |
| 6            | 0110       |
| 7            | 0111       |

The output represents the decimal value of the active input in BCD format.

## Proteus Implementation

The encoder circuits were implemented in Proteus using hierarchical circuit blocks.

- 8-to-3 encoder
- 4-to-2 priority encoder
- Octal-to-BCD encoder

Input switches were used to apply logic levels to the circuits and observe their outputs.

## Applications

- Digital systems and data encoding
- Interrupt-priority handling
- Keyboard and input encoding
- Digital communication and control circuits
