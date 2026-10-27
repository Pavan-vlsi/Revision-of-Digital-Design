# Synchronous Sequential Logic

## 1. Introduction

Digital circuits are classified into two main categories:

- **Combinational circuits:** The output depends only on the present inputs. They do not store information.
- **Sequential circuits:** The output depends on the present inputs and the circuit's stored state. They have memory.

Sequential circuits are used in digital systems to store, retain, and retrieve binary information.

Examples include registers, counters, memory units, and control circuits.

## 2. Sequential Circuits

A sequential circuit consists of:
- Combinational logic
- Storage elements
- Feedback paths connecting the storage elements and logic

The storage elements retain binary information. The information stored at a particular time defines the **state** of the circuit.

The output of a sequential circuit depends on:
1. Present external inputs
2. Present state stored in the storage elements

The external inputs and present state determine the circuit's output and the conditions for changing its state.

### 2.1 Types of Sequential Circuits

Sequential circuits are classified into two types:

| Type | Description |
|---|---|
| Asynchronous sequential circuits | The state can change in response to changes in the inputs, without waiting for a clock signal. |
| Synchronous sequential circuits | State changes are coordinated by a clock signal. |

### 2.2 Synchronous Sequential Circuits

Synchronous sequential circuits use a clock signal to control when their storage elements update.

The clock signal determines the timing of state changes, allowing the circuit to operate in a coordinated manner.

A synchronous sequential circuit generally consists of combinational logic connected to storage elements such as flip-flops.

**Clock pulse:** A transition or pulse of the clock signal that controls the operation of the storage elements.

**Flip-flop:** A storage element that stores one bit of binary information and, in a typical synchronous circuit, updates its state in response to the active clock edge.

The combinational logic determines the data to be stored, while the storage elements retain the state between updates.

## 3. Storage Elements: Latches

A storage element maintains a binary state as long as power is supplied, until its state is changed by the appropriate input signals.

The two important types of storage elements are:

- **Latch:** A level-sensitive storage element.
- **Flip-flop:** An edge-triggered storage element.

A latch responds to the levels of its control signals, whereas a flip-flop responds to a specified clock edge.

Latches form the basic storage circuits from which flip-flops can be constructed.

## 4. SR Latch

An SR latch is a basic storage circuit with two inputs:

- **S — Set:** Sets the output `Q` to `1`.
- **R — Reset:** Resets the output `Q` to `0`.

An SR latch can be constructed using either:
- Two cross-coupled NOR gates
- Two cross-coupled NAND gates

The outputs are normally complementary:

- `Q` — Normal output
- `Q'` — Complemented output

### 4.1 SR Latch Using NOR Gates

The NOR-based SR latch has active-HIGH inputs.

| S | R | Next state of Q | Operation |
|---:|---:|---|---|
| 0 | 0 | No change | Hold |
| 0 | 1 | 0 | Reset |
| 1 | 0 | 1 | Set |
| 1 | 1 | Invalid | Forbidden condition |

**Operation:**

- `S = 1, R = 0`: The latch enters the set state, so `Q = 1`.
- `S = 0, R = 1`: The latch enters the reset state, so `Q = 0`.
- `S = 0, R = 0`: The latch retains its previous state.
- `S = 1, R = 1`: Both outputs become `0`, violating the normal complementary-output relationship. This condition is forbidden.

The inputs should not both be set to `1` simultaneously.

### 4.2 SR Latch Using NAND Gates

The NAND-based SR latch uses active-LOW inputs, commonly written as `S'` and `R'`.

| S' | R' | Next state of Q | Operation |
|---:|---:|---|---|
| 1 | 1 | No change | Hold |
| 1 | 0 | 0 | Reset |
| 0 | 1 | 1 | Set |
| 0 | 0 | Invalid | Forbidden condition |

**Operation:**

- `S' = 0, R' = 1`: The latch enters the set state.
- `S' = 1, R' = 0`: The latch enters the reset state.
- `S' = 1, R' = 1`: The latch retains its previous state.
- `S' = 0, R' = 0`: Both outputs become `1`, violating the normal complementary-output relationship. This condition is forbidden.

### 4.3 NOR and NAND SR Latches Compared

| Feature | NOR-based SR latch | NAND-based SR latch |
|---|---|---|
| Input polarity | Active-HIGH | Active-LOW |
| Set condition | `S = 1, R = 0` | `S' = 0, R' = 1` |
| Reset condition | `S = 0, R = 1` | `S' = 1, R' = 0` |
| Hold condition | `S = 0, R = 0` | `S' = 1, R' = 1` |
| Forbidden condition | `S = 1, R = 1` | `S' = 0, R' = 0` |

## 5. SR Latch with Control Input

A control input, commonly called **Enable (En)**, can be added to an SR latch to determine when the S and R inputs are allowed to affect the stored state.

For an active-HIGH enable:

- `En = 0`: The latch holds its current state.
- `En = 1`: The latch responds to the S and R inputs.

The control input gates the S and R signals before they reach the basic latch.

### Function Table

| En | S | R | Next state of Q |
|---:|---:|---:|---|
| 0 | X | X | No change |
| 1 | 0 | 0 | No change |
| 1 | 0 | 1 | Reset (`Q = 0`) |
| 1 | 1 | 0 | Set (`Q = 1`) |
| 1 | 1 | 1 | Invalid |

`X` means that the input can be either `0` or `1` because it does not affect the output in that condition.

The forbidden condition occurs when the enable is active and both S and R are `1`.

## 6. D Latch (Transparent Latch)

The D latch avoids the forbidden input combination of the basic SR latch by using a single data input, `D`.

It has two main inputs:

- **D — Data:** The value to be stored.
- **En — Enable:** Controls when the data can affect the output.

The D input is used to derive the set and reset signals internally, preventing the user from applying the forbidden SR input combination directly.

### 6.1 Function Table

| En | D | Next state of Q | Operation |
|---:|---:|---|---|
| 0 | X | No change | Hold |
| 1 | 0 | 0 | Store 0 |
| 1 | 1 | 1 | Store 1 |

### 6.2 Operation

- **En = 0:** The latch retains its previously stored value, regardless of changes in `D`.
- **En = 1:** The latch is transparent, meaning `Q` follows `D`.
- When the enable returns to `0`, the last value present at `D` is retained at `Q`.

The D latch stores one bit of information.

### 6.3 Why It Is Called a Transparent Latch

When `En = 1`, changes in the data input pass through to the output. This behaviour is called transparency.

When `En = 0`, the output retains the stored value even if the data input changes.

## 7. Key Differences

| Feature | SR Latch | SR Latch with Enable | D Latch |
|---|---|---|---|
| Main inputs | S and R | S, R and En | D and En |
| Storage | 1 bit | 1 bit | 1 bit |
| Hold operation | Yes | Yes | Yes |
| Controlled by enable | No | Yes | Yes |
| Forbidden input combination | Yes | Yes, when enabled | Avoided by the D-input arrangement |
| Main purpose | Basic set/reset storage | Controlled set/reset storage | Controlled data storage |

## 8. Important Points to Remember

- Combinational circuits have no memory; sequential circuits have memory.
- The **state** of a sequential circuit is the binary information currently stored in its storage elements.
- Synchronous sequential circuits coordinate state updates using a clock.
- Latches are level-sensitive; flip-flops are edge-triggered.
- An SR latch has Set and Reset inputs.
- The NOR-based SR latch uses active-HIGH inputs.
- The NAND-based SR latch uses active-LOW inputs.
- The basic SR latch has a forbidden input condition.
- An enable input controls when an SR latch responds to its inputs.
- A D latch has one data input and avoids the forbidden SR input combination.
- A D latch is transparent when its enable is active and holds its value when its enable is inactive.
