# T Flip-Flop

## 1. Introduction

A T (Toggle) flip-flop is a sequential circuit that either holds its previous state or toggles its output depending on the input T.

- When T = 0, the output remains unchanged.
- When T = 1, the output toggles to its complement.

The next state depends on the present state and the T input.

## 2. Truth Table

| T | Q(n) | Q(n+1) | Operation |
|---|------|--------|-----------|
| 0 | 0 | 0 | Hold |
| 0 | 1 | 1 | Hold |
| 1 | 0 | 1 | Toggle |
| 1 | 1 | 0 | Toggle |

**Characteristic Equation:**

`Q(n+1) = T ⊕ Q(n)`

## 3. T Flip-Flop Using NAND Gates (Level-Triggered)

A T flip-flop was implemented in Proteus using NAND gates with feedback connections.

The circuit uses:
- T input
- Enable input
- Preset and Reset inputs
- Feedback connections from Q and Q'
- NAND gates to implement the logic

### Working

- When Enable = 0, the circuit holds its previous state.
- When Enable = 1 and T = 0, the output remains unchanged.
- When Enable = 1 and T = 1, the feedback logic causes the output to toggle.

The circuit was implemented and simulated in Proteus to observe its behaviour.

**Note:** A level-sensitive implementation can be susceptible to repeated toggling while the enable remains active. Edge-triggered flip-flops avoid this issue by changing state at a clock edge.

## 4. T Flip-Flop Using JK Flip-Flop (Edge-Triggered)

A T flip-flop can be implemented using a JK flip-flop by connecting both J and K inputs to the T input.

Therefore:

`J = K = T`

### JK Flip-Flop Truth Table

| J | K | Q(n+1) | Operation |
|---|---|--------|-----------|
| 0 | 0 | Q(n) | Hold |
| 0 | 1 | 0 | Reset |
| 1 | 0 | 1 | Set |
| 1 | 1 | Q'(n) | Toggle |

### Derivation Using the Excitation Table

The excitation table of a JK flip-flop specifies the required J and K inputs for a given transition.

| Q(n) | Q(n+1) | J | K |
|------|--------|---|---|
| 0 | 0 | 0 | X |
| 0 | 1 | 1 | X |
| 1 | 0 | X | 1 |
| 1 | 1 | X | 0 |

Here, X represents a don't-care condition.

Using the T flip-flop truth table and the JK excitation table:

**For J:**

| Q(n) | T | Q(n+1) | J |
|------|---|--------|---|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 1 | X |
| 1 | 1 | 0 | X |

Simplifying using a K-map:

`J = T`

**For K:**

| Q(n) | T | Q(n+1) | K |
|------|---|--------|---|
| 0 | 0 | 0 | X |
| 0 | 1 | 1 | X |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |

Simplifying using a K-map:

`K = T`

Therefore, the final connections are:

`J = K = T`

### Working

- When T = 0, J = K = 0, so the JK flip-flop holds its previous state.
- When T = 1, J = K = 1, so the JK flip-flop toggles its output.
- The output changes only at the active clock edge.

The circuit was implemented in Proteus using a JK flip-flop IC, with T connected to both J and K inputs.

## 5. Applications of T Flip-Flops

- Binary counters
- Frequency division
- Toggle circuits
- Sequential logic circuits
- Digital counting systems

## 6. Practical Implementation

The following circuits were designed and simulated in Proteus:

1. Level-triggered T flip-flop using NAND gates.
2. Edge-triggered T flip-flop using a JK flip-flop.

The JK-to-T conversion was derived using the excitation table and K-map simplification.
