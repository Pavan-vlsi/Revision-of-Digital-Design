# JK Flip-Flop

## Introduction

The JK flip-flop is a sequential logic circuit that stores one bit of information. It is an improved version of the SR flip-flop, designed to eliminate the invalid input condition.

It has two inputs, J and K, and two complementary outputs, Q and Q'.

- **J:** Set input.
- **K:** Reset input.
- **Q:** Normal output.
- **Q':** Complementary output.
- **CLK:** Controls when the state changes.

## Truth Table

| J | K | Next State (Q(n+1)) | Operation |
|---|---|---------------------|-----------|
| 0 | 0 | Q(n) | No change |
| 0 | 1 | 0 | Reset |
| 1 | 0 | 1 | Set |
| 1 | 1 | Q'(n) | Toggle |

## Working Principle

1. **No Change (J=0, K=0):** The output retains its previous state.
2. **Reset (J=0, K=1):** The output Q becomes 0.
3. **Set (J=1, K=0):** The output Q becomes 1.
4. **Toggle (J=1, K=1):** The output changes to the complement of its previous state.

The toggle operation is the key feature that distinguishes the JK flip-flop from the SR flip-flop.

## Characteristic Equation

The characteristic equation describes the next state of the flip-flop:

\[
Q_{n+1}=J\overline{Q_n}+\overline{K}Q_n
\]

## Race-Around Condition

In a level-triggered JK circuit, when J=K=1 and the clock remains active for longer than the propagation delay, the output may toggle repeatedly.

This is known as the **race-around condition**.

It can be avoided by using:
- Edge-triggered JK flip-flops.
- Master-slave JK flip-flops.
- Proper clock pulse-width control.

## Preset and Clear

Some JK flip-flop ICs provide asynchronous control inputs:

- **Preset:** Forces Q to 1.
- **Clear/Reset:** Forces Q to 0.

These inputs operate independently of the clock. On the 7476, preset and clear are active-low inputs.

## Applications

- Counters and frequency division.
- Toggle circuits.
- Registers and control circuits.
- Sequential logic systems.

## Proteus Implementation

The JK flip-flop was implemented and simulated in Proteus using:

- NAND gates to construct a JK logic circuit.
- A 7476 JK flip-flop IC for comparison.
- J and K input logic switches.
- A clock source.
- Preset and reset controls.
- Q and Q' output indicators.

The simulation was used to observe the different JK operations and verify the output states.
