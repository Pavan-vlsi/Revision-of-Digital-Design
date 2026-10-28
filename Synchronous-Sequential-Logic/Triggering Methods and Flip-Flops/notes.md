# Synchronous Sequential Logic — Flip-Flops

## 1. Sequential Circuits

A sequential circuit is a digital circuit whose output depends on the present inputs and the previous state.

It consists of combinational logic and storage elements. The stored binary information represents the current state of the circuit.

| Combinational Circuit | Sequential Circuit |
|---|---|
| Output depends on present inputs. | Output depends on present inputs and previous state. |
| Does not store previous state. | Stores binary information. |
| Examples: Adders, MUX, Decoders. | Examples: Flip-flops, Registers, Counters. |

## 2. Storage Elements

Storage elements retain binary information.

- **Latch:** A level-sensitive storage element.
- **Flip-flop:** An edge-triggered storage element.

A flip-flop stores one bit of information. Its outputs are commonly represented as `Q` and `Q'`, where `Q'` is the complement of `Q`.

### Clock Signal

A clock is a periodic digital signal used to control state changes in synchronous circuits.

- **Positive edge:** Clock transition from `0` to `1`.
- **Negative edge:** Clock transition from `1` to `0`.

A positive-edge-triggered flip-flop responds to the rising edge, while a negative-edge-triggered flip-flop responds to the falling edge.

## 3. SR Flip-Flop

An SR flip-flop has two control inputs:

- `S` — Set
- `R` — Reset

Outputs:

- `Q` — Normal output
- `Q'` — Complementary output

### Block Representation

```text
          ┌───────────┐
    S ────┤ S       Q ├──── Q
          │           │
  CLK  ───┤> CLK      │
          │           │
    R ────┤ R      Q' ├──── Q'
          └───────────┘
```

The triangle at the clock input represents edge triggering. The symbol shown here represents a positive-edge-triggered device.

### Truth Table

The following table describes the operation at the active clock edge.

| Clock Event | S | R | Q(next) | Operation |
|---|---|---|---|---|
| No active edge | X | X | Q | Hold |
| Rising edge | 0 | 0 | Q | Hold |
| Rising edge | 0 | 1 | 0 | Reset |
| Rising edge | 1 | 0 | 1 | Set |
| Rising edge | 1 | 1 | Invalid | Forbidden condition |

`X` means the input can be either `0` or `1` without affecting the result for that row.

The condition `S = 1, R = 1` is forbidden for the conventional SR flip-flop.

### Characteristic Equation

For valid input combinations:

`Q(next) = S + R'Q`

The equation does not apply to the forbidden input combination.

### Operation

- **Hold:** The stored state remains unchanged.
- **Set:** The output becomes `1`.
- **Reset:** The output becomes `0`.
- **Forbidden:** Both control inputs are asserted simultaneously.

## 4. D Flip-Flop

A D flip-flop stores the value present at its data input when the active clock edge occurs.

Input:
- `D` — Data input
- `CLK` — Clock input

Outputs:
- `Q` — Stored output
- `Q'` — Complementary output

### Block Representation

```text
          ┌───────────┐
    D ────┤ D       Q ├──── Q
          │           │
   CLK ───┤>CLK       │
          │           │
          │        Q' ├──── Q'
          └───────────┘
```

The triangle at the clock input represents edge triggering.

### Truth Table

| Clock Event | D | Q(next) | Operation |
|---|---|---|---|
| No active edge | X | Q | Hold |
| Rising edge | 0 | 0 | Store 0 |
| Rising edge | 1 | 1 | Store 1 |

### Characteristic Equation

`Q(next) = D`

The D flip-flop avoids the forbidden input combination found in the conventional SR flip-flop.

## 5. Clock-Edge Triggering

Flip-flops can be designed to respond to either the rising or falling edge of the clock.

| Triggering Type | Clock Transition | Action |
|---|---|---|
| Positive-edge triggering | `0 → 1` | Samples the input |
| Negative-edge triggering | `1 → 0` | Samples the input |

The stored output remains unchanged between active clock edges unless an asynchronous control input changes the state.

## 6. Practical Implementation in Proteus

### SR Flip-Flop

- Implemented the SR storage circuit using logic gates.
- Applied Set and Reset inputs.
- Observed the normal and complementary outputs.
- Examined the hold, set, and reset operations.

### D Flip-Flop

- Implemented the D storage circuit using logic gates.
- Applied data values at the D input.
- Used a clock signal to control state changes.
- Observed the normal and complementary outputs.

### Clock-Edge Demonstration

- Demonstrated positive-edge triggering.
- Demonstrated negative-edge triggering.
- Compared the rising and falling transitions of the clock signal.

## 7. Applications of Flip-Flops

- Registers and shift registers
- Counters
- Data storage
- State registers
- Synchronous control circuits
- Finite-state machines

## Key Points

- Sequential circuits retain information about their previous state.
- Latches are level-sensitive; flip-flops are edge-triggered.
- An SR flip-flop supports Set, Reset, and Hold operations.
- The conventional SR flip-flop has a forbidden input combination.
- A D flip-flop stores the input value at the active clock edge.
- Positive-edge triggering responds to `0 → 1`.
- Negative-edge triggering responds to `1 → 0`.
