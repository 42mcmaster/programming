# ard03a — Binary Number Practice: Answer Key

**Programming — Medina County Career Center**

---

## Part 1: Binary to Decimal

**1.** `0101` = 0 + 4 + 0 + 1 = **5**

**2.** `1100` = 8 + 4 + 0 + 0 = **12**

**3.** `1001` = 8 + 0 + 0 + 1 = **9**

**4.** `1010` = 8 + 0 + 2 + 0 = **10**

---

## Part 2: Decimal to Binary

**5.** Decimal **3** → 8:No, 4:No, 2:Yes(1), 1:Yes(0) → **0011** — Check: 2+1 = 3 ✓

**6.** Decimal **7** → 8:No, 4:Yes(3), 2:Yes(1), 1:Yes(0) → **0111** — Check: 4+2+1 = 7 ✓

**7.** Decimal **12** → 8:Yes(4), 4:Yes(0), 2:No, 1:No → **1100** — Check: 8+4 = 12 ✓

**8.** Decimal **14** → 8:Yes(6), 4:Yes(2), 2:Yes(0), 1:No → **1110** — Check: 8+4+2 = 14 ✓

---

## Part 3: LED States

**9.** Decimal **6** → Binary **0110**
Pin 13 (8s): OFF — Pin 12 (4s): ON — Pin 11 (2s): ON — Pin 10 (1s): OFF

**10.** Decimal **9** → Binary **1001**
Pin 13 (8s): ON — Pin 12 (4s): OFF — Pin 11 (2s): OFF — Pin 10 (1s): ON

---

## Part 4: Thinking Questions

**11.** What is the largest number you can represent with 4 bits? What about 5 bits?

4 bits: **15** (1111 = 8+4+2+1). 5 bits: **31** (11111 = 16+8+4+2+1). The pattern is 2^n − 1, where n is the number of bits.

**12.** Column patterns in the binary table:

- **1s column:** Flips every number (0,1,0,1,0,1...)
- **2s column:** Flips every 2 numbers (0,0,1,1,0,0,1,1...)
- **4s column:** Flips every 4 numbers (0,0,0,0,1,1,1,1...)
- **8s column:** Flips every 8 numbers (0,0,0,0,0,0,0,0,1,1,1,1,1,1,1,1)

Each column flips at half the rate of the column to its right.
