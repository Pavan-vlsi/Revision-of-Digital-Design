# 4-Bit Adder–Subtractor and BCD Adder 

## Overview

This practical explores two combinational arithmetic circuits implemented
and simulated in Proteus:

1. A 4-bit adder–subtractor with overflow detection.
2. A Binary-Coded Decimal (BCD) adder.

The objective was to understand how binary arithmetic circuits can be
constructed from smaller digital building blocks and how additional
logic enables a circuit to perform different arithmetic operations.

---

# 1. 4-Bit Adder–Subtractor with Overflow Detection

## Objective

To implement a 4-bit arithmetic circuit that performs binary addition
or subtraction, selected using a mode input, and includes logic for
detecting signed arithmetic overflow.

## Inputs and Outputs

| Signal | Description |
|---|---|
| A3–A0 | First 4-bit operand |
| B3–B0 | Second 4-bit operand |
| M | Operation-select mode |
| S3–S0 | 4-bit arithmetic result |
| C4 | Final carry output |
| V | Signed overflow indicator |

The mode input selects the operation:

- `M = 0`: Addition, A + B
- `M = 1`: Subtraction, A - B

## Working Principle

The circuit uses four full-adder stages connected in a ripple-carry
configuration.

Each bit of operand B passes through an XOR gate controlled by M.

The modified B input is:

B'i = Bi XOR M

The initial carry input is:

C0 = M

### Addition Mode

When M = 0:

Bi XOR 0 = Bi

C0 = 0

Therefore, the circuit performs:

A + B

### Subtraction Mode

When M = 1:

Bi XOR 1 = NOT Bi

C0 = 1

Therefore, the full adders calculate:

A + NOT(B) + 1

Using two's-complement arithmetic, this is equivalent to:

A - B

This arrangement allows the same full-adder hardware to perform both
addition and subtraction.

## Full-Adder Equations

For each bit position i:

Pi = Ai XOR B'i

Si = Pi XOR Ci

C(i+1) = (Ai AND B'i) OR (Pi AND Ci)

where:

- Pi is the propagate signal.
- Ci is the carry entering the stage.
- Si is the sum output.
- C(i+1) is the carry leaving the stage.

The carry from one stage feeds the next stage. This is why the circuit
is called a ripple-carry adder.

## Signed Overflow Detection

For two's-complement arithmetic, signed overflow occurs when the
mathematical result cannot be represented using the available number
of bits.

For a 4-bit ripple-carry circuit:

V = C3 XOR C4

Here, C3 is the carry entering the most significant bit, and C4 is
the carry leaving it.

An alternative equivalent expression for a correctly implemented
two's-complement adder–subtractor is:

V = NOT(A3 XOR B3) XOR S3

where B3 refers to the original, unmodified operand B.

**Important distinction:** The final carry C4 and signed overflow V
are different indicators. Carry-out is useful for unsigned arithmetic,
whereas V detects signed two's-complement overflow.

## Verification Cases

Useful test cases for simulation include:

| A | B | M | Operation | Expected result | Overflow |
|---|---|---|---|---|---|
| 0011 | 0010 | 0 | 3 + 2 | 0101 | 0 |
| 0100 | 0011 | 0 | 4 + 3 | 0111 | 0 |
| 0111 | 0001 | 0 | 7 + 1 | 1000 | 1 |
| 0101 | 0011 | 1 | 5 - 3 | 0010 | 0 |
| 0011 | 0101 | 1 | 3 - 5 | 1110 | 0 |
| 1000 | 0001 | 1 | -8 - 1 | 0111 | 1 |

The final two examples illustrate two's-complement interpretation.
For four-bit signed arithmetic, the representable range is -8 to +7.

The result 1110 represents -2, while 0111 represents +7.

In the final test, the mathematical result -9 is outside the
four-bit signed range, so overflow is asserted.

These are expected logical results; confirm the actual circuit outputs
against them during simulation.

## Key Learning

- Addition and subtraction can share one full-adder datapath.
- XOR gates conditionally complement the B operand.
- The initial carry input supplies the +1 needed for two's-complement
  subtraction.
- Ripple-carry architecture passes carry information between stages.
- Carry-out and signed overflow must not be confused.

---

# 2. BCD Adder

## Objective

To implement and study a circuit that adds two 4-bit BCD digits and
corrects the binary sum when necessary to produce a valid BCD result.

## What Is BCD?

Binary-Coded Decimal represents each decimal digit independently
using four binary bits.

| Decimal digit | BCD representation |
|---|---|
| 0 | 0000 |
| 1 | 0001 |
| 2 | 0010 |
| 3 | 0011 |
| 4 | 0100 |
| 5 | 0101 |
| 6 | 0110 |
| 7 | 0111 |
| 8 | 1000 |
| 9 | 1001 |

The combinations from 1010 through 1111 are not valid encodings of
individual decimal digits in standard 8421 BCD.

## Why Is Correction Necessary?

A 4-bit binary adder can produce values from 0000 through 1111.
However, a single BCD digit must represent only decimal values 0–9.

When the binary sum exceeds 9, or produces a carry beyond four bits,
the result requires correction.

The correction adds binary 0110 (decimal 6) to the four-bit sum.

Adding six converts the invalid intermediate result into the proper
BCD digit and decimal carry representation.

## Circuit Structure

The BCD adder is built from:

1. A 4-bit binary adder.
2. Logic that detects when BCD correction is required.
3. A second 4-bit adder that adds 0110 when correction is required.

Let the first binary adder produce:

- C4: carry-out
- Z3, Z2, Z1, Z0: four-bit intermediate sum

The correction signal is:

K = C4 OR [Z3 AND (Z2 OR Z1)]

Equivalently:

K = C4 + Z3Z2 + Z3Z1

In these equations, `+` means OR and adjacent variables mean AND.

When K = 1, correction is necessary.

When K = 0, the intermediate result is already a valid BCD digit.

## Correction Adder

The correction value is:

0110 when K = 1

0000 when K = 0

Therefore, the four correction-adder inputs are:

- 0
- K
- K
- 0

The correction adder adds this value to the intermediate binary sum.

Its output gives the corrected BCD digit and, when needed, the decimal
carry to the next digit position.

## Example 1: 4 + 3

BCD inputs:

0100 + 0011

Binary sum:

0111

Since 7 is a valid BCD digit, correction is not required.

Result:

0111 = decimal 7

## Example 2: 5 + 7

BCD inputs:

0101 + 0111

Intermediate binary sum:

1100 = decimal 12

Since the intermediate result is greater than 9, correction is required.

Add:

1100 + 0110 = 1 0010

The corrected BCD output is:

0001 0010

This represents decimal 12:

- Decimal carry = 1
- BCD digit = 0010

## Example 3: 8 + 9

BCD inputs:

1000 + 1001

Intermediate binary result:

1 0001

The first adder produces a carry, so correction is required.

The corrected BCD result is:

0001 0111

This represents decimal 17:

- Decimal carry = 1
- BCD digit = 0111

## Verification Cases

| Decimal operation | BCD input A | BCD input B | Expected BCD result |
|---|---|---|---|
| 2 + 3 | 0010 | 0011 | 0101 |
| 4 + 3 | 0100 | 0011 | 0111 |
| 5 + 7 | 0101 | 0111 | 0001 0010 |
| 8 + 9 | 1000 | 1001 | 0001 0111 |
| 9 + 9 | 1001 | 1001 | 0001 1000 |

These are expected results for valid BCD inputs. Verify them against
the Proteus simulation.

## Key Learning

- BCD arithmetic is different from ordinary binary arithmetic.
- A binary sum from 1010 through 1111 is not a valid single BCD digit.
- The correction logic determines when six must be added.
- A BCD adder uses binary addition followed by conditional correction.
- The correction stage produces a valid BCD digit and decimal carry.

---

# Practical Summary

This work demonstrates two important applications of combinational
logic in arithmetic hardware.

The 4-bit adder–subtractor reuses full-adder stages to implement
addition and two's-complement subtraction under a mode-control input.

The BCD adder combines binary addition, correction detection, and a
second addition stage to preserve decimal-digit representation.

Both circuits illustrate how a larger digital system can be built by
connecting smaller combinational building blocks.
