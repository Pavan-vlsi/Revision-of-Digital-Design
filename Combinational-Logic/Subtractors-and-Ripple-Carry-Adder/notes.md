# Subtractors and Ripple-Carry Adder

## 1. Half Subtractor

A half subtractor subtracts input B from input A.

**Outputs:** Difference (D) and Borrow (Bo).

### Truth Table

| A | B | D | Bo |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 0 |

### Boolean Expressions

- **Difference:** `D = A XOR B`
- **Borrow:** `Bo = NOT(A) AND B`

---

## 2. Full Subtractor

A full subtractor subtracts B and the input borrow (Bin) from A.

**Outputs:** Difference (D) and Borrow out (Bo).

### Truth Table

| A | B | Bin | D | Bo |
|---|---|---|---|---|
| 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 | 1 |
| 0 | 1 | 0 | 1 | 1 |
| 0 | 1 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 | 0 |
| 1 | 0 | 1 | 0 | 0 |
| 1 | 1 | 0 | 0 | 0 |
| 1 | 1 | 1 | 1 | 1 |

### Boolean Expressions

- **Difference:** `D = A XOR B XOR Bin`
- **Borrow out:** `Bo = (NOT(A) AND B) OR (Bin AND NOT(A XOR B))`

### Implementation

The full subtractor is implemented using two half subtractors and one OR gate.

---

## 3. Four-Bit Ripple-Carry Adder

A four-bit ripple-carry adder adds two four-bit binary numbers using four cascaded full adders.

**Inputs:**
- A3, A2, A1, A0
- B3, B2, B1, B0
- Initial carry (Cin)

**Outputs:**
- Sum: S3, S2, S1, S0
- Final carry: Cout

### Boolean Expressions

For each stage `i`:

- **Sum:** `Si = Ai XOR Bi XOR Ci`
- **Carry:** `Ci+1 = (Ai AND Bi) OR (Ci AND (Ai XOR Bi))`

The carry output of one full adder becomes the carry input of the next stage.

### Important Insight

The carry propagates from the least significant bit toward the most significant bit. This makes the design straightforward, but the propagation delay can increase as more stages are added.

---

## Proteus Implementation

The following circuits were designed using logic gates and functional blocks in Proteus:

1. Half Subtractor
2. Full Subtractor using two Half Subtractors and an OR gate
3. Four-Bit Ripple-Carry Adder using four cascaded Full Adders
