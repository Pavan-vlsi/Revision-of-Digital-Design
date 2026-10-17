# Realization of Basic Gates Using Universal Gates

## 1. Objective

To implement NOT, AND, and OR gates using NAND gates alone and NOR gates alone.

## 2. NAND Gate Realizations

A NAND gate produces:

**Y = (A · B)'**

### NOT Gate

Connect both inputs of a NAND gate to A.

**Y = (A · A)' = A'**

Number of gates: 1 NAND

### OR Gate

Using De Morgan's theorem:

**Y = A + B = (A' · B')'**

Use two NAND gates as inverters to obtain A' and B'. Connect these outputs to a third NAND gate.

Number of gates: 3 NAND

### AND Gate

First NAND operation:

**X = (A · B)'**

Invert X using another NAND gate:

**Y = (X · X)' = A · B**

Number of gates: 2 NAND

---

## 3. NOR Gate Realizations

A NOR gate produces:

**Y = (A + B)'**

### NOT Gate

Connect both inputs of a NOR gate to A.

**Y = (A + A)' = A'**

Number of gates: 1 NOR

### OR Gate

First NOR operation:

**X = (A + B)'**

Invert X using another NOR gate:

**Y = (X + X)' = A + B**

Number of gates: 2 NOR

### AND Gate

Using De Morgan's theorem:

**Y = A · B = (A' + B')'**

Use two NOR gates as inverters to obtain A' and B'. Connect these outputs to a third NOR gate.

Number of gates: 3 NOR

---

## 4. Gate Count Comparison

| Required Gate | NAND-Only Implementation | NOR-Only Implementation |
|---|---:|---:|
| NOT | 1 | 1 |
| AND | 2 | 3 |
| OR | 3 | 2 |

*Gate counts assume two-input NAND and NOR gates.*

## 5. Important Insights

- NAND and NOR are universal gates because either type alone can implement any Boolean function.
- De Morgan's theorems help transform Boolean expressions into NAND-only or NOR-only implementations.
- Different gate implementations can produce the same logical output but may differ in gate count, delay, and power in practical circuits.

## 6. Truth Table Verification

Use this truth table to verify the basic logic functions.

| A | B | NOT A | AND | OR | NAND | NOR |
|---|---|---|---|---|---|---|
| 0 | 0 | 1 | 0 | 0 | 1 | 1 |
| 0 | 1 | 1 | 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 0 | 1 | 1 | 0 |
| 1 | 1 | 0 | 1 | 1 | 0 | 0 |

### Verification Procedure

1. Implement each circuit in Proteus.
2. Apply all possible input combinations.
3. Observe the output using logic probes.
4. Compare the observed outputs with the truth table.
5. Confirm that each circuit performs the intended logic function.

## 7. Conclusion

NOT, AND, and OR functions can be implemented using NAND gates alone or NOR gates alone. This demonstrates that both NAND and NOR are universal gates.
