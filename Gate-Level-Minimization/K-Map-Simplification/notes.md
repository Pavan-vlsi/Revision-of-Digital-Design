# K-Map Simplification: 3-Variable and 4-Variable Maps

## 1. Objective

To simplify Boolean functions using three-variable and four-variable Karnaugh maps (K-maps) and obtain minimal Sum-of-Products (SOP) or Product-of-Sums (POS) expressions.

## 2. Introduction to K-Maps

A Karnaugh map is a graphical method for simplifying Boolean functions by identifying adjacent cells with identical output values.

- A 3-variable K-map contains 2³ = 8 cells.
- A 4-variable K-map contains 2⁴ = 16 cells.
- Each cell represents one minterm or one maxterm, depending on the function representation.
- Rows and columns follow Gray-code order: 00, 01, 11, 10.
- Adjacent cells differ in exactly one variable.

### SOP and POS

| Feature | SOP | POS |
|---|---|---|
| Full form | Sum of Products | Product of Sums |
| Group | Adjacent 1s | Adjacent 0s |
| Result | Product terms joined by OR | Sum terms joined by AND |
| Canonical notation | F = Σm(...) | F = ΠM(...) |

**Important:** Group 1s for SOP simplification and 0s for POS simplification.

---

## 3. Grouping Rules

Valid group sizes are powers of two.

| Group size | Standard name |
|---:|---|
| 16 cells | Group of 16 |
| 8 cells | Octet |
| 4 cells | Quad |
| 2 cells | Pair |
| 1 cell | Singleton |

A group of 16 is possible only in a four-variable K-map.

### Rules to Remember

1. Prefer larger groups because they eliminate more variables.
2. Cover every required 1 for SOP or every required 0 for POS.
3. Groups may overlap when necessary to obtain a simpler expression.
4. A cell may belong to more than one group.
5. Diagonal cells are not adjacent.
6. Opposite edges of a K-map are adjacent.
7. The four corner cells of a four-variable K-map form a valid quad.
8. Use the fewest suitable groups that cover all required cells while producing a minimal expression.
9. Singleton groups are used when a required cell cannot be combined with another required cell.

**Note:** Choosing the largest group first is a useful strategy, but it does not always guarantee the minimum expression. The final group selection must cover all required cells with a minimal combination of terms.

### Deriving Terms for SOP

Within each group:
- A variable that remains 1 appears uncomplemented.
- A variable that remains 0 appears complemented.
- A variable that changes is eliminated.

### Deriving Terms for POS

Within each group of zeros:
- A variable that remains 0 appears uncomplemented.
- A variable that remains 1 appears complemented.
- A variable that changes is eliminated.

---

## 4. Three-Variable K-Map

For variables A, B, and C:

- Rows represent A.
- Columns represent BC in Gray-code order.
- There are eight cells, corresponding to minterms m0 through m7.

### K-Map Layout

| A \ BC | 00 | 01 | 11 | 10 |
|---|---|---|---|---|
| 0 | m0 | m1 | m3 | m2 |
| 1 | m4 | m5 | m7 | m6 |

### Simplification Example

Given:

**F(A, B, C) = Σm(1, 2, 3, 5, 7)**

This means the function is 1 at minterms 1, 2, 3, 5, and 7.

#### Step 1: Fill the K-map

| A \ BC | 00 | 01 | 11 | 10 |
|---|---|---|---|---|
| 0 | 0 | 1 | 1 | 1 |
| 1 | 0 | 1 | 1 | 0 |

#### Step 2: Form the groups

**Group 1: Octet not possible; form a quad**

Group minterms m1, m3, m5, and m7.

In all four cells, C = 1.

Therefore, the simplified term is:

**C**

**Group 2: Pair**

Group minterms m2 and m3.

For both cells:
- A = 0, so A appears complemented.
- B = 1, so B appears uncomplemented.
- C changes, so C is eliminated.

Therefore, the simplified term is:

**A'B**

#### Step 3: Write the simplified expression

OR the terms obtained from both groups.

**F = C + A'B**

This is the minimal SOP expression.

---

## 5. Four-Variable K-Map

For variables A, B, C, and D:

- Rows represent AB in Gray-code order.
- Columns represent CD in Gray-code order.
- There are 16 cells, corresponding to minterms m0 through m15.

### K-Map Layout

| AB \ CD | 00 | 01 | 11 | 10 |
|---|---|---|---|---|
| 00 | m0 | m1 | m3 | m2 |
| 01 | m4 | m5 | m7 | m6 |
| 11 | m12 | m13 | m15 | m14 |
| 10 | m8 | m9 | m11 | m10 |

### Simplification Example

Given:

**F(A, B, C, D) = Σm(0, 2, 5, 7, 8, 10, 13, 15)**

#### Step 1: Fill the K-map

| AB \ CD | 00 | 01 | 11 | 10 |
|---|---|---|---|---|
| 00 | 1 | 0 | 0 | 1 |
| 01 | 0 | 1 | 1 | 0 |
| 11 | 0 | 1 | 1 | 0 |
| 10 | 1 | 0 | 0 | 1 |

#### Step 2: Form the groups

**Group 1: Quad using the four corners**

Group minterms m0, m2, m8, and m10.

The four corners are adjacent through edge wrapping.

In this group:
- B = 0, so B' remains.
- D = 0, so D' remains.
- A and C change and are eliminated.

Term obtained:

**B'D'**

**Group 2: Quad**

Group minterms m5, m7, m13, and m15.

In this group:
- B = 1, so B remains.
- D = 1, so D remains.
- A and C change and are eliminated.

Term obtained:

**BD**

#### Step 3: Write the simplified expression

Combine the two product terms using OR.

**F = B'D' + BD**

This is the minimal SOP expression.

---

## 6. Prime Implicants

An **implicant** is a product term that covers one or more 1s without covering any 0s.

A **prime implicant** is an implicant that cannot be combined into a larger valid group.

An **essential prime implicant** covers at least one required 1 that no other prime implicant covers.

Essential prime implicants must be included in the final SOP expression.

For POS simplification, the corresponding groups are formed from zeros, and the resulting terms are sum terms.

---

## 7. Five-Variable K-Maps

A five-variable function contains:

**2⁵ = 32 cells**

A five-variable K-map can be represented using two linked four-variable maps, one for each value of the fifth variable.

Although five-variable K-maps are possible, their layout and adjacency relationships become more complicated. Manual grouping becomes increasingly difficult as the number of variables increases.

### Quine–McCluskey Method

The Quine–McCluskey method is a systematic tabular method for minimizing Boolean functions.

It is useful when:
- The function contains many variables.
- Manual K-map grouping becomes inconvenient.
- A systematic or computer-assisted minimization procedure is preferred.

**Note:** The method is not restricted to functions with more than four variables. It can also be used for smaller functions, although K-maps are often more convenient for three or four variables.

---

## 8. Important Insights

- K-map simplification eliminates variables that change within a group.
- Gray-code ordering ensures that adjacent cells differ in only one variable.
- Larger groups generally produce simpler terms.
- SOP uses groups of 1s; POS uses groups of 0s.
- K-map simplification helps reduce the logic required to implement combinational circuits.
- The resulting Boolean expression can be implemented using logic gates or described in Verilog HDL.

## 9. Conclusion

Three-variable and four-variable K-maps provide a visual method for simplifying Boolean functions.

Correct cell placement, adjacency, grouping, and term derivation are essential for obtaining minimal expressions in SOP or POS form.

For functions with more variables, methods such as Quine–McCluskey can provide a more systematic approach to minimization.
