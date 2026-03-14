# Lesson 03: How Computers Think — Binary Numbers
## Study Guide & Reference

**Programming — Medina County Career Center**

---

This guide covers the binary number system concepts from Paul McWhorter's Lesson 5. Use it as a reference while working through the task file and during the build project in Lesson 04.

---

## 1. NUMBER SYSTEMS

### Decimal (Base 10) — What You Already Know

You count in base 10 every day. The "base" means how many digits the system uses.

Base 10 uses digits **0 through 9**. Each position is worth 10 times the position to its right.

```
The number 2,537:
  Thousands  Hundreds  Tens  Ones
     2          5       3     7

= (2 × 1000) + (5 × 100) + (3 × 10) + (7 × 1)
= 2000 + 500 + 30 + 7
= 2537
```

### Binary (Base 2) — How Computers Think

Base 2 uses only two digits: **0** and **1**. Each position is worth 2 times the position to its right.

```
The binary number 1101:
  Eights  Fours  Twos  Ones
    1       1      0     1

= (1 × 8) + (1 × 4) + (0 × 2) + (1 × 1)
= 8 + 4 + 0 + 1
= 13 in decimal
```

### Why Binary?

Computers are built from billions of tiny transistors — switches that are either ON or OFF. There's no "halfway" — it's one state or the other. Binary maps perfectly to this: 1 = ON, 0 = OFF.

---

## 2. PLACE VALUES

### Decimal Place Values

```
... 10000  1000  100  10  1
    10^4   10^3  10^2 10^1 10^0
```

### Binary Place Values

```
... 128  64  32  16  8  4  2  1
    2^7  2^6 2^5 2^4 2^3 2^2 2^1 2^0
```

For 4-bit binary (which is what we'll use with 4 LEDs):

| Position | 3 (leftmost) | 2 | 1 | 0 (rightmost) |
|---|---|---|---|---|
| Place value | **8** | **4** | **2** | **1** |

The rightmost bit is the **least significant bit** (smallest value).
The leftmost bit is the **most significant bit** (largest value).

---

## 3. CONVERTING BINARY TO DECIMAL

**Method:** Add up the place values wherever there's a 1.

### Worked Examples

**Convert 1010:**
```
Bit:          1    0    1    0
Place value:  8    4    2    1
              8  + 0  + 2  + 0  = 10
```

**Convert 0110:**
```
Bit:          0    1    1    0
Place value:  8    4    2    1
              0  + 4  + 2  + 0  = 6
```

**Convert 1111:**
```
Bit:          1    1    1    1
Place value:  8    4    2    1
              8  + 4  + 2  + 1  = 15
```

**Convert 0001:**
```
Bit:          0    0    0    1
Place value:  8    4    2    1
              0  + 0  + 0  + 1  = 1
```

---

## 4. CONVERTING DECIMAL TO BINARY

**Method:** Start with the largest place value. Ask "does it fit?" If yes, write a 1 and subtract. If no, write a 0. Move to the next place value.

### Worked Examples

**Convert 9 to binary:**
```
8s: Does 8 fit into 9?  YES → write 1, remainder = 9 - 8 = 1
4s: Does 4 fit into 1?  NO  → write 0
2s: Does 2 fit into 1?  NO  → write 0
1s: Does 1 fit into 1?  YES → write 1, remainder = 0

Answer: 1001
Check: 8 + 0 + 0 + 1 = 9 ✓
```

**Convert 6 to binary:**
```
8s: Does 8 fit into 6?  NO  → write 0
4s: Does 4 fit into 6?  YES → write 1, remainder = 6 - 4 = 2
2s: Does 2 fit into 2?  YES → write 1, remainder = 0
1s: Does 1 fit into 0?  NO  → write 0

Answer: 0110
Check: 0 + 4 + 2 + 0 = 6 ✓
```

**Convert 15 to binary:**
```
8s: Does 8 fit into 15? YES → write 1, remainder = 15 - 8 = 7
4s: Does 4 fit into 7?  YES → write 1, remainder = 7 - 4 = 3
2s: Does 2 fit into 3?  YES → write 1, remainder = 3 - 2 = 1
1s: Does 1 fit into 1?  YES → write 1, remainder = 0

Answer: 1111
Check: 8 + 4 + 2 + 1 = 15 ✓
```

---

## 5. THE COMPLETE 4-BIT TABLE

Memorizing this table will make Lesson 04 much easier. At minimum, you should be able to quickly derive any row.

| Decimal | Binary | How to remember |
|---|---|---|
| 0 | 0000 | All off |
| 1 | 0001 | Just the 1s place |
| 2 | 0010 | Just the 2s place |
| 3 | 0011 | 2 + 1 |
| 4 | 0100 | Just the 4s place |
| 5 | 0101 | 4 + 1 |
| 6 | 0110 | 4 + 2 |
| 7 | 0111 | 4 + 2 + 1 (all but the 8) |
| 8 | 1000 | Just the 8s place |
| 9 | 1001 | 8 + 1 |
| 10 | 1010 | 8 + 2 |
| 11 | 1011 | 8 + 2 + 1 |
| 12 | 1100 | 8 + 4 |
| 13 | 1101 | 8 + 4 + 1 |
| 14 | 1110 | 8 + 4 + 2 (all but the 1) |
| 15 | 1111 | All on |

**Pattern to notice:** The 1s column alternates every number. The 2s column alternates every 2 numbers. The 4s column alternates every 4. The 8s column switches at 8.

---

## 6. BITS AND BYTES

| Term | Bits | Values | Range |
|---|---|---|---|
| 1 bit | 1 | 2 | 0–1 |
| Nibble | 4 | 16 | 0–15 |
| Byte | 8 | 256 | 0–255 |
| Two bytes | 16 | 65,536 | 0–65,535 |
| Four bytes | 32 | 4,294,967,296 | 0–4,294,967,295 |

**The formula:** *n* bits can represent **2^n** different values.

### Why This Matters for Arduino

In Arduino (and C), the `int` data type uses 4 bytes (32 bits) and can store numbers from about −2 billion to +2 billion. The `byte` type uses 1 byte (8 bits) and stores 0–255. When you choose a data type, you're choosing how many bits to use.

---

## 7. BINARY AND LEDS

This is the connection between binary math and your Arduino:

| Binary digit | LED state | Arduino command |
|---|---|---|
| 1 | ON | `digitalWrite(pin, HIGH)` |
| 0 | OFF | `digitalWrite(pin, LOW)` |

With 4 LEDs, you have 4 bits, which means 16 possible combinations (0–15). Each LED represents one place value:

| LED (left to right) | Pin | Place value |
|---|---|---|
| LED 1 (leftmost) | Pin 13 | 8s |
| LED 2 | Pin 12 | 4s |
| LED 3 | Pin 11 | 2s |
| LED 4 (rightmost) | Pin 10 | 1s |

**Example:** To display the number 11 (binary 1011):
- Pin 13: HIGH (8s bit is 1)
- Pin 12: LOW (4s bit is 0)
- Pin 11: HIGH (2s bit is 1)
- Pin 10: HIGH (1s bit is 1)

---

## 8. COUNTING PATTERNS IN BINARY

Binary counting follows a predictable pattern. Watch the rightmost bit — it flips every number. The next bit flips every 2 numbers. The next every 4, and so on.

```
0000  ←  all off
0001  ←  1s bit flips
0010  ←  2s bit flips, 1s resets
0011  ←  1s bit flips
0100  ←  4s bit flips, 2s and 1s reset
0101  ←  1s bit flips
0110  ←  2s bit flips, 1s resets
0111  ←  1s bit flips
1000  ←  8s bit flips, all others reset
...
```

This is exactly like a decimal counter: 09 → 10 (ones reset, tens increment), 99 → 100 (ones and tens reset, hundreds increment).

---

## VOCABULARY

**Binary** — A number system using only two digits (0 and 1). Also called base 2.

**Decimal** — The standard number system using ten digits (0–9). Also called base 10.

**Bit** — A single binary digit, either 0 or 1. Short for "binary digit."

**Nibble** — A group of 4 bits. Can represent values 0–15.

**Byte** — A group of 8 bits. Can represent values 0–255. The fundamental unit of computer memory.

**Place Value** — The value a digit represents based on its position. In binary: 1, 2, 4, 8, 16, 32, 64, 128, etc.

**Most Significant Bit (MSB)** — The leftmost bit, representing the highest place value.

**Least Significant Bit (LSB)** — The rightmost bit, representing the lowest place value (1).

**Base** — The number of unique digits in a number system. Binary is base 2; decimal is base 10.

**Transistor** — A tiny electronic switch inside a computer chip. Can be ON or OFF, which maps to 1 or 0.

---

## ODE COMPETENCIES COVERED

**5.1.1** — Describe how computer programs and scripts can be used to solve problems
**5.2.1** — Data types and variables (understanding how data is stored in binary)
**5.2.3** — Arithmetic operations (binary arithmetic and conversions)
