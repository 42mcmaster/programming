# ard03a — Binary Number Practice

**Programming — Medina County Career Center**
**Standards: ODE 5.1.1, 5.2.1, 5.2.3**

---

## Before You Start

This is a **paper and pencil** task — no Arduino needed yet. You need to be comfortable with binary conversions before building the binary counter in the next lesson.

**Watch the video first:** Paul McWhorter's Lesson 5 — https://www.youtube.com/watch?v=cSOpMpynXAI

Use the **Study Guide** as your reference while you work.

---

## Part 1: Binary to Decimal

Convert each binary number to decimal by adding up the place values.

**Worked example:**

```
Binary: 1011

Place values:  8  4  2  1
Bits:          1  0  1  1
               8 +0 +2 +1 = 11

Answer: 1011 = 11
```

### Your turn — show your work:

**1.** `0101` = ______

**2.** `1100` = ______

**3.** `1001` = ______

**4.** `1010` = ______

---

## Part 2: Decimal to Binary

Convert each decimal number to 4-bit binary using the "does it fit?" method.

**Worked example:**

```
Decimal: 10

8s: Does 8 fit into 10?  YES → 1, remainder = 2
4s: Does 4 fit into 2?   NO  → 0
2s: Does 2 fit into 2?   YES → 1, remainder = 0
1s: Does 1 fit into 0?   NO  → 0

Answer: 10 = 1010
Check: 8 + 0 + 2 + 0 = 10 ✓
```

### Your turn — show your work and check each answer:

**5.** Decimal **3** = ______

**6.** Decimal **7** = ______

**7.** Decimal **12** = ______

**8.** Decimal **14** = ______

---

## Part 3: LED States

For each number, convert to binary and write what each LED would show on pins 13, 12, 11, 10.

**Worked example:**

```
Decimal 11 → Binary 1011
Pin 13 (8s): ON    Pin 12 (4s): OFF    Pin 11 (2s): ON    Pin 10 (1s): ON
```

**9.** Decimal **6** → Binary ____

```
Pin 13 (8s):    Pin 12 (4s):    Pin 11 (2s):    Pin 10 (1s):
```

**10.** Decimal **9** → Binary ____

```
Pin 13 (8s):    Pin 12 (4s):    Pin 11 (2s):    Pin 10 (1s):
```

---

## Part 4: Thinking Questions

**11.** What is the largest number you can represent with 4 bits? What about 5 bits? Explain the pattern.

```
YOUR ANSWER:

```

**12.** Look at the binary table (0–15) in the Study Guide. Describe the pattern in each column — how often does the 1s column flip? The 2s column? The 4s? The 8s?

```
YOUR ANSWER:

```

---

## Submission Checklist

- [ ] Part 1: 4 binary-to-decimal conversions with work shown
- [ ] Part 2: 4 decimal-to-binary conversions with work and checks
- [ ] Part 3: 2 LED state problems answered
- [ ] Part 4: Both thinking questions answered in complete sentences
