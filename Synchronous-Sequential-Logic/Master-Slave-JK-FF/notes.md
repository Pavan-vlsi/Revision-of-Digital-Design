# Master-Slave JK Flip-Flop

## 1. Introduction

A Master-Slave JK flip-flop is a sequential circuit constructed using two interconnected latches: a Master and a Slave.

It eliminates the race-around condition associated with a level-triggered JK flip-flop by allowing the Master and Slave to operate during opposite clock phases.

## 2. Working Principle

- The Master latch accepts the J and K inputs during one clock phase.
- The Slave latch updates the output during the opposite clock phase.
- The output does not repeatedly toggle during the same clock pulse.
- The final output depends on the J and K inputs and the previous state.

## 3. Truth Table

| J | K | Next State | Operation |
|---|---|---|---|
| 0 | 0 | Q(n) | No Change |
| 0 | 1 | 0 | Reset |
| 1 | 0 | 1 | Set |
| 1 | 1 | Q'(n) | Toggle |

## 4. Preset and Reset

Preset and Reset are asynchronous control inputs that operate independently of the clock.

In this circuit, both controls are active-LOW.

- **Preset (PRE):** When PRE = 0, Q is forced to 1.
- **Reset (RST):** When RST = 0, Q is forced to 0.
- When both controls are 1, they are inactive and normal JK operation is enabled.

### Preset and Reset Truth Table

| PRE | RST | Q | Q' | Operation |
|---|---|---|---|---|
| 0 | 0 | 1 | 1 | Forbidden |
| 0 | 1 | 1 | 0 | Asynchronous Set |
| 1 | 0 | 0 | 1 | Asynchronous Reset |
| 1 | 1 | Previous Q | Complement of Q | Normal Operation |

**Important Points:**

- When both controls are LOW, both outputs become HIGH, violating their complementary relationship.
- When PRE = 0, the output is forced to the SET state.
- When RST = 0, the output is forced to the RESET state.
- Before testing the JK input combinations, release both asynchronous controls by setting PRE = RST = 1.

## 5. Race-Around Condition

The race-around condition occurs in a level-triggered JK flip-flop when J = K = 1 and the clock remains active long enough for the output to toggle repeatedly.

The Master-Slave arrangement prevents this condition by separating the input and output operations into opposite clock phases.

## 6. Proteus Implementation

The Master-Slave JK flip-flop was designed and simulated in Proteus using:

- NAND gates
- NOT gate
- J and K inputs
- Clock input
- Preset and Reset controls
- Q and Q' outputs

The circuit was used to observe the Set, Reset, Hold and Toggle operations.

The asynchronous Preset and Reset controls were used to initialize the output before testing the JK input combinations.

## 7. Applications

- Counters
- Registers
- Frequency division
- Sequential logic circuits
- Digital control systems
