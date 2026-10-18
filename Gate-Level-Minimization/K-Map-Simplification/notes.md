# K-Map Simplification: 3-Variable and 4-Variable Maps

## 1. Objective

To simplify Boolean functions using three-variable and four-variable Karnaugh maps (K-maps), obtain minimal SOP and POS expressions, and implement the resulting circuits using basic logic gates.

## 2. Introduction

A Karnaugh map is a graphical technique for simplifying Boolean functions by grouping adjacent cells.

- 3-variable K-map: 2³ = 8 cells.
- 4-variable K-map: 2⁴ = 16 cells.
- Each cell represents a minterm or maxterm, depending on the representation.
- Rows and columns follow Gray-code order: 00, 01, 11, 10.
- Adjacent cells differ in exactly one variable.

### SOP and POS

| Feature | SOP | POS |
|---|---|---|
| Full form | Sum of Products | Product of Sums |
| Group | Adjacent 1s | Adjacent 0s |
| Result | Product terms joined by OR | Sum terms joined by AND |
| Notation | F = Σm(...) | F = ΠM(...) |

**Remember:** Group 1s for SOP and 0s for POS.

---

## 3. Grouping Rules

| Group size | Name |
|---:|---|
| 16 cells | Group of 16 |
| 8 cells | Octet |
| 4 cells | Quad |
| 2 cells | Pair |
| 1 cell | Singleton |

A group of 16 is possible in a four-variable K-map.

### Important Rules

1. Prefer the largest valid groups to eliminate more variables.
2. Cover every required 1 for SOP or every required 0 for POS.
3. Groups may overlap when doing so helps simplify the expression.
4. Diagonal cells are not adjacent.
5. Opposite edges of the K-map are adjacent.
6. The four corner cells of a four-variable map form a valid quad.
7. Use the smallest suitable collection of groups that covers all required cells and produces a minimal expression.

### Obtaining Terms

**For SOP (grouping 1s):**
- Variable fixed at 1 → appears uncomplemented.
- Variable fixed at 0 → appears complemented.
- Variable that changes → eliminated.

**For POS (grouping 0s):**
- Variable fixed at 0 → appears uncomplemented.
- Variable fixed at 1 → appears complemented.
- Variable that changes → eliminated.

---

## 4. Three-Variable K-Map

For variables A, B, and C, the rows represent A and the columns represent BC.

### K-Map Layout

| A \ BC | 00 | 01 | 11 | 10 |
|---|---|---|---|---|
| 0 | m0 | m1 | m3 | m2 |
| 1 | m4 | m5 | m7 | m6 |

### Worked Example

Given:

**F(A, B, C) = Σm(1, 2, 3, 5, 7)**

#### Step 1: Fill the K-map

| A \ BC | 00 | 01 | 11 | 10 |
|---|---|---|---|---|
| 0 | 0 | 1 | 1 | 1 |
| 1 | 0 | 1 | 1 | 0 |

#### Step 2: Form the groups

**Group 1 — Quad:** m1, m3, m5, m7.

C remains 1, while A and B change.

Term obtained: **C**

**Group 2 — Pair:** m2, m3.

A = 0 and B = 1 remain constant, while C changes.

Term obtained: **A'B**

#### Step 3: Simplified expression

**F = C + A'B**

This is the minimal SOP expression.

---

## 5. Four-Variable K-Map Simplification

### Problem

Simplify the Boolean function:

**F(A, B, C, D) = Σm(0, 2, 3, 5, 7, 8, 9, 10, 11, 13, 15)**

### Step 1: Construct the K-map

Rows and columns follow Gray-code order.

| AB \ CD | 00 | 01 | 11 | 10 |
|:---:|:---:|:---:|:---:|:---:|
| 00 | 1 (m0) | 0 (m1) | 1 (m3) | 1 (m2) |
| 01 | 0 (m4) | 1 (m5) | 1 (m7) | 0 (m6) |
| 11 | 0 (m12) | 1 (m13) | 1 (m15) | 0 (m14) |
| 10 | 1 (m8) | 1 (m9) | 1 (m11) | 1 (m10) |

### Step 2: Identify the groups

**Group 1 — Quad: BD**

Group the four cells where B = 1 and D = 1:

m5, m7, m13, m15

A and C change, so they are eliminated.

Term: **BD**

**Group 2 — Quad: B'D'**

Group the four corner cells:

m0, m2, m8, m10

The map wraps around at its edges. B = 0 and D = 0 remain constant, while A and C change.

Term: **B'D'**

**Group 3 — Quad: CD**

Group the four cells:

m3, m7, m11, m15

C = 1 and D = 1 remain constant.

Term: **CD**

**Group 4 — Quad: AD**

Group the four cells:

m9, m11, m13, m15

A = 1 and D = 1 remain constant.

Term: **AD**

### Step 3: Write the simplified expression

Combining the four product terms:

**F = BD + B'D' + CD + AD**

This is the simplified SOP expression obtained from the K-map.

### Step 4: Proteus implementation

The simplified function was implemented using basic logic gates.

- NOT gates generate B' and D'.
- AND gates generate BD, B'D', CD, and AD.
- An OR gate combines the four product terms to produce F.

The output was checked against the original function's minterms.

Expected output HIGH for:

**m(0, 2, 3, 5, 7, 8, 9, 10, 11, 13, 15)**


---

## 6. Prime Implicants

An **implicant** is a valid group of cells representing a product term in SOP simplification.

A **prime implicant** is an implicant that cannot be expanded into a larger valid group.

An **essential prime implicant** covers at least one required 1 that no other prime implicant covers.

### Simplification Procedure

1. Identify all prime implicants.
2. Identify the essential prime implicants.
3. Include all essential prime implicants.
4. Check which required 1s remain uncovered.
5. Select additional prime implicants to cover the remaining 1s.
6. Compare valid selections if multiple choices exist.

The same general principle applies to POS simplification, but the groups contain 0s and produce sum terms.

---

## 7. Product-of-Sums (POS) Simplification

For POS simplification, group adjacent 0s instead of 1s.

Each group produces a sum term, and the resulting terms are ANDed together.

### Rules for a POS Group

- Variable fixed at 0 → appears uncomplemented.
- Variable fixed at 1 → appears complemented.
- Variable that changes → eliminated.

The final expression has the form:

**F = (sum term 1)(sum term 2)...**

### Important Distinction

- SOP: group 1s and OR the resulting product terms.
- POS: group 0s and AND the resulting sum terms.

Both methods simplify the same Boolean function and can produce equivalent implementations.

---

## 8. Five-Variable K-Map

A five-variable Boolean function contains:

**2⁵ = 32 cells**

A five-variable map can be represented as two linked four-variable maps, one for each value of the fifth variable.

As the number of variables increases, the number of cells grows exponentially and the geometry of adjacency becomes more complicated.

For this reason, larger K-maps become increasingly difficult to simplify manually.

### Quine–McCluskey Method

The Quine–McCluskey method is a systematic tabular method for Boolean-function minimization.

It is useful when:
- The number of variables makes manual K-map grouping inconvenient.
- A systematic minimization procedure is required.
- Computer-assisted Boolean minimization is desired.

It is not restricted to functions with more than four variables; it can also be used for smaller functions.

---

## 9. Important Insights

- K-maps eliminate variables that change within a group.
- Gray-code ordering ensures that adjacent cells differ in only one variable.
- Larger valid groups generally produce simpler terms.
- SOP groups 1s; POS groups 0s.
- Prime implicants help identify the possible product terms in a minimized SOP expression.
- Essential prime implicants must be included in a minimal SOP cover.
- The simplified expression can be implemented using basic gates or described using Verilog HDL.

## 10. Conclusion

Three-variable and four-variable K-maps provide a visual method for minimizing Boolean functions.

Correct cell placement, grouping, prime-implicant selection, and term derivation are essential for obtaining a simplified expression.

For this study, the simplified four-variable expression was implemented in Proteus using basic logic gates:

**F = BD + B'D' + CD + AD**

Five-variable functions contain 32 cells, making manual grouping more complicated. Systematic methods such as Quine–McCluskey can be useful for larger functions.
