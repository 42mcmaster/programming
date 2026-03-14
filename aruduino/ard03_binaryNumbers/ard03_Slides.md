---
marp: true
theme: default
class: invert
paginate: true
---

# Lesson 03: How Computers Think — Binary Numbers
## Programming
### Medina County Career Center
**Based on Paul McWhorter's Arduino Lesson 5**

---

## Today's Lesson

Watch **Paul McWhorter's Lesson 5** on YouTube:
https://www.youtube.com/watch?v=cSOpMpynXAI

This video explains how all computers — including your Arduino — think in binary numbers. These slides reinforce the key concepts from the video.

---

## Why Binary?

Computers are built from tiny switches (transistors) that are either **ON** or **OFF**.

- ON = 1
- OFF = 0

That's it. Everything a computer does — numbers, text, images, music, video games — is built from combinations of 1s and 0s.

**Binary** is the number system that uses only two digits: **0** and **1**.

---

## How We Normally Count: Decimal (Base 10)

The number system you've used your whole life is **base 10** (decimal).

Each position is worth **10 times** more than the one to its right:

| Position | Thousands | Hundreds | Tens | Ones |
|---|---|---|---|---|
| Place value | 1000 | 100 | 10 | 1 |
| The number 3,427 | 3 | 4 | 2 | 7 |

**3,427** = (3 × 1000) + (4 × 100) + (2 × 10) + (7 × 1)

Why base 10? Because we have 10 fingers. That's literally it.

---

## How Computers Count: Binary (Base 2)

In binary, each position is worth **2 times** more than the one to its right:

| Position | Eights | Fours | Twos | Ones |
|---|---|---|---|---|
| Place value | 8 | 4 | 2 | 1 |
| Binary digits | 1 or 0 | 1 or 0 | 1 or 0 | 1 or 0 |

Each position is called a **bit** (binary digit).

4 bits together can represent numbers from **0 to 15**.

---

## Converting Binary to Decimal

To convert a binary number, add up the place values where there's a 1:

**Example: 1011 in binary**

| Bit | 1 | 0 | 1 | 1 |
|---|---|---|---|---|
| Place value | 8 | 4 | 2 | 1 |
| Calculation | 8 | 0 | 2 | 1 |

**8 + 0 + 2 + 1 = 11** (decimal)

So 1011 in binary = 11 in decimal.

---

## Converting Decimal to Binary

Start with the largest place value and work down. Ask: "Does it fit?"

**Example: Convert 13 to binary**

- **8s place:** Does 8 fit into 13? Yes → write **1**, remainder = 13 − 8 = **5**
- **4s place:** Does 4 fit into 5? Yes → write **1**, remainder = 5 − 4 = **1**
- **2s place:** Does 2 fit into 1? No → write **0**
- **1s place:** Does 1 fit into 1? Yes → write **1**, remainder = 0

**Answer: 1101**

---

## The First 16 Binary Numbers

| Decimal | Binary | Place Values |
|---|---|---|
| 0 | 0000 | nothing |
| 1 | 0001 | 1 |
| 2 | 0010 | 2 |
| 3 | 0011 | 2 + 1 |
| 4 | 0100 | 4 |
| 5 | 0101 | 4 + 1 |
| 6 | 0110 | 4 + 2 |
| 7 | 0111 | 4 + 2 + 1 |
| 8 | 1000 | 8 |
| 9 | 1001 | 8 + 1 |
| 10 | 1010 | 8 + 2 |
| 11 | 1011 | 8 + 2 + 1 |
| 12 | 1100 | 8 + 4 |
| 13 | 1101 | 8 + 4 + 1 |
| 14 | 1110 | 8 + 4 + 2 |
| 15 | 1111 | 8 + 4 + 2 + 1 |

---

## Bits and Bytes

| Term | How many bits | Range |
|---|---|---|
| 1 bit | 1 | 0 – 1 |
| 4 bits (nibble) | 4 | 0 – 15 |
| 8 bits (byte) | 8 | 0 – 255 |
| 16 bits | 16 | 0 – 65,535 |
| 32 bits | 32 | 0 – 4,294,967,295 |

**Pattern:** With *n* bits, you can represent 2^n different values (0 through 2^n − 1).

4 bits → 2^4 = 16 values (0–15)
8 bits → 2^8 = 256 values (0–255)

---

## Binary and Your Arduino

Your Arduino uses binary constantly:

- `digitalWrite(pin, HIGH)` sends a **1** (5 volts)
- `digitalWrite(pin, LOW)` sends a **0** (0 volts)
- Each LED on your breadboard represents **one bit**
- 4 LEDs = 4 bits = numbers 0–15

In the next lesson, you'll build a circuit with 4 LEDs and program the Arduino to count from 0 to 15 in binary — one LED per bit.

---

## How Everything Becomes Binary

Computers don't just store numbers in binary — **everything** is binary:

- **Text**: Each letter has a number (A = 65, B = 66, ...) stored in binary
- **Colors**: Each pixel has red, green, blue values (0–255 each) — that's 3 bytes per pixel
- **Sound**: Audio is sampled thousands of times per second, each sample stored as a number
- **Images**: Millions of pixels, each with color values, all in binary

Your Arduino sends HIGH and LOW signals — that's binary at the hardware level.

---

## Key Takeaways

- Computers think in **binary** (base 2) because they're built from on/off switches
- Each binary digit is called a **bit**; 8 bits = 1 **byte**
- To convert binary to decimal: add up the place values (8, 4, 2, 1) where there's a 1
- To convert decimal to binary: subtract the largest place value that fits, repeat
- 4 bits can represent 0–15; 8 bits can represent 0–255
- Everything in a computer — numbers, text, images, sound — is stored in binary
- **Next lesson**: You'll build a 4-LED binary counter on your Arduino!
