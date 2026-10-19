# Code Conversion and Binary Adders

## 1. Objective

To understand BCD-to-Excess-3 code conversion, half-adder operation, and full-adder implementation using basic logic gates, and to verify their behavior through Proteus simulation.

---

## 2. BCD-to-Excess-3 Code Conversion

### Introduction

**BCD (Binary-Coded Decimal)** represents each decimal digit using four binary bits.

**Excess-3** is a non-weighted decimal code obtained by adding 3 (0011 in binary) to the BCD representation of a decimal digit.

### Conversion Table

| Decimal | BCD (A B C D) | Excess-3 (W X Y Z) |
|---:|:---:|:---:|
| 0 | 0000 | 0011 |
| 1 | 0001 | 0100 |
| 2 | 0010 | 0101 |
| 3 | 0011 | 0110 |
| 4 | 0100 | 0111 |
| 5 | 0101 | 1000 |
| 6 | 0110 | 1001 |
| 7 | 0111 | 1010 |
| 8 | 1000 | 1011 |
| 9 | 1001 | 1100 |

### Working Principle

The four input bits represent a decimal digit in BCD. The combinational circuit produces the corresponding Excess-3 code.

For example:

BCD input: `0101` (decimal 5)

Add 3:

`0101 + 0011 = 1000`

Therefore, the Excess-3 output is `1000`.

The converter can be designed by deriving Boolean expressions for each output bit from the conversion truth table and simplifying them using K-maps.

**Important:** BCD inputs from 1010 to 1111 are invalid decimal-digit representations. They may be treated as don't-care conditions during simplification when the design specification permits it.

---

## 3. Half-Adder

### Definition

A half-adder is a combinational circuit that adds two single-bit binary inputs and produces a Sum and a Carry.

Inputs: A, B

Outputs: Sum (S), Carry (C)

### Truth Table

| A | B | Sum (S) | Carry (C) |
|:-:|:-:|:-:|:-:|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |

### Boolean Expressions

**Sum:**

`S = A ⊕ B`

**Carry:**

`C = A · B`

The XOR gate produces the Sum, while the AND gate produces the Carry.

### Operation

- When the inputs differ, Sum = 1.
- When both inputs are 1, Carry = 1.
- A half-adder has no carry input from a previous stage.

### Proteus Implementation

The circuit was implemented using:
- One XOR gate for Sum.
- One AND gate for Carry.

Both outputs can be checked for all four possible input combinations.

---

## 4. Full-Adder

### Definition

A full-adder is a combinational circuit that adds three single-bit inputs: A, B, and the input carry (Cin).

It produces two outputs:
- Sum (S)
- Carry-out (Cout)

### Truth Table

| A | B | Cin | Sum | Cout |
|:-:|:-:|:-:|:-:|:-:|
| 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 | 0 |
| 0 | 1 | 0 | 1 | 0 |
| 0 | 1 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 | 0 |
| 1 | 0 | 1 | 0 | 1 |
| 1 | 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 1 | 1 |

### Boolean Expressions

**Sum:**

`S = A ⊕ B ⊕ Cin`

**Carry-out:**

`Cout = AB + ACin + BCin`

The Carry-out becomes 1 when at least two of the three inputs are 1.

### Full-Adder Using Two Half-Adders and an OR Gate

A full-adder can be constructed using two half-adders and one OR gate.

**First half-adder:**

`S1 = A ⊕ B`

`C1 = AB`

**Second half-adder:**

`S = S1 ⊕ Cin`

`C2 = S1 · Cin`

**Final carry:**

`Cout = C1 + C2`

Substituting:

`Cout = AB + (A ⊕ B)Cin`

This is equivalent to:

`Cout = AB + ACin + BCin`

### Proteus Implementation

The circuit was constructed using:
- Two XOR gates.
- Two AND gates.
- One OR gate.

The first half-adder adds A and B. The second adds the first Sum to Cin. The OR gate combines the two carry outputs.

**Key insight:** Unlike a half-adder, a full-adder accepts a carry input, allowing multiple full-adders to be connected to construct multi-bit binary adders.

---

## 5. Verification

### Half-Adder

Verify all four input combinations and compare the Sum and Carry outputs against the truth table.

### Full-Adder

Verify all eight input combinations and compare both outputs against the truth table.

### BCD-to-Excess-3 Converter

Test the ten valid BCD inputs from 0000 to 1001 and confirm that each output matches the conversion table.

---

## 6. Conclusion

This study covered three combinational logic circuits:

1. **BCD-to-Excess-3 converter:** Converts valid BCD digits into Excess-3 code.
2. **Half-adder:** Adds two single-bit inputs and generates Sum and Carry.
3. **Full-adder:** Adds two data bits and an input carry; it can be implemented using two half-adders and an OR gate.

The circuits were designed and simulated in Proteus to study their logic and verify their input-output behavior.
