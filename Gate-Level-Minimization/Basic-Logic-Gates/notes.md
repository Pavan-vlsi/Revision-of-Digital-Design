# Digital Logic Gates

## 1. AND Gate
The AND gate produces HIGH (1) only when all its inputs are HIGH (1). Otherwise, its output is LOW (0).

**Boolean Expression:** F = A · B

## 2. OR Gate
The OR gate produces HIGH (1) when at least one input is HIGH (1). Its output is LOW (0) only when all inputs are LOW (0).

**Boolean Expression:** F = A + B

## 3. NOT Gate (Inverter)
The NOT gate produces the complement of its input. A HIGH input produces a LOW output, and vice versa.

**Boolean Expression:** F = A′

## 4. Buffer
A buffer produces the same logic value as its input. It does not invert the signal.

**Boolean Expression:** F = A

## 5. NAND Gate
The NAND gate is the complement of the AND gate. Its output is LOW (0) only when all inputs are HIGH (1).

**Boolean Expression:** F = (A · B)′

## 6. NOR Gate
The NOR gate is the complement of the OR gate. Its output is HIGH (1) only when all inputs are LOW (0).

**Boolean Expression:** F = (A + B)′

## 7. Exclusive-OR (XOR) Gate
The XOR gate produces HIGH (1) when its two inputs are different and LOW (0) when they are the same.

**Boolean Expression:** F = A′B + AB′

## 8. Exclusive-NOR (XNOR) Gate
The XNOR gate produces HIGH (1) when its two inputs are the same and LOW (0) when they are different.

**Boolean Expression:** F = AB + A′B′

---

## Truth Tables

### AND, OR, NAND, NOR, XOR and XNOR Gates

| A | B | AND | OR | NAND | NOR | XOR | XNOR |
|---|---|-----|----|------|-----|-----|------|
| 0 | 0 |  0  | 0  |  1   |  1  |  0  |  1   |
| 0 | 1 |  0  | 1  |  1   |  0  |  1  |  0   |
| 1 | 0 |  0  | 1  |  1   |  0  |  1  |  0   |
| 1 | 1 |  1  | 1  |  0   |  0  |  0  |  1   |

### NOT Gate and Buffer

| A | NOT (A′) | Buffer |
|---|----------|--------|
| 0 | 1        | 0      |
| 1 | 0        | 1      |

---




