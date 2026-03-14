---
marp: true
theme: default
class: invert
paginate: true
---

# Lesson 04: Build a Binary Counter
## Programming
### Medina County Career Center
**Based on Paul McWhorter's Arduino Lesson 6**

---

## Today's Build

Watch **Paul McWhorter's Lesson 6** on YouTube:
https://www.youtube.com/watch?v=KEtut8pzXZA

You'll wire 4 LEDs to your Arduino and program them to count from 0 to 15 in binary.

You can follow along with Paul's video, or use the written build guide. Either way, you'll end up with the same working project.

---

## What You're Building

A 4-LED binary counter that counts from 0 to 15, displaying each number in binary.

Each LED = one bit:

| LED | Pin | Place Value |
|---|---|---|
| Leftmost | Pin 13 | **8s** |
| Second | Pin 12 | **4s** |
| Third | Pin 11 | **2s** |
| Rightmost | Pin 10 | **1s** |

**ON = 1**, **OFF = 0**

---

## Recall: Binary Numbers

From Lesson 03, you know that 4 bits can represent 0–15:

| Number | Binary | LEDs (13, 12, 11, 10) |
|---|---|---|
| 0 | 0000 | OFF OFF OFF OFF |
| 5 | 0101 | OFF ON OFF ON |
| 10 | 1010 | ON OFF ON OFF |
| 13 | 1101 | ON ON OFF ON |
| 15 | 1111 | ON ON ON ON |

Today you'll see this come alive on real hardware.

---

## Components Needed

From your kit:

- Arduino Uno R4 WiFi
- Breadboard
- **4 LEDs** (any color — red is easiest to see)
- **4 resistors** (1KΩ — brown-black-red-gold)
- **Jumper wires** (4 colored + 1 black for GND)
- USB-C cable

---

## Safety Reminders

- **One resistor per LED** — never share resistors between LEDs
- **Long leg of LED** = positive → faces the Arduino pin
- **Build the circuit BEFORE plugging in USB**
- The resistors keep current at a safe level — don't skip them

---

## The Circuit

Each LED follows the same wiring pattern from Lesson 02:

```
Arduino Pin → LED (long leg to short leg) → 1KΩ Resistor → GND rail
```

Repeat this for all four LEDs using pins 13, 12, 11, and 10.

```
Pin 13 → LED 1 → Resistor → GND rail    (8s place, leftmost)
Pin 12 → LED 2 → Resistor → GND rail    (4s place)
Pin 11 → LED 3 → Resistor → GND rail    (2s place)
Pin 10 → LED 4 → Resistor → GND rail    (1s place, rightmost)
Arduino GND → GND rail
```

---

## The Code Structure

```cpp
void setup() {
    pinMode(13, OUTPUT);  // 8s
    pinMode(12, OUTPUT);  // 4s
    pinMode(11, OUTPUT);  // 2s
    pinMode(10, OUTPUT);  // 1s
}

void loop() {
    // 0: 0000
    digitalWrite(13, LOW);  digitalWrite(12, LOW);
    digitalWrite(11, LOW);  digitalWrite(10, LOW);
    delay(500);

    // 1: 0001
    digitalWrite(13, LOW);  digitalWrite(12, LOW);
    digitalWrite(11, LOW);  digitalWrite(10, HIGH);
    delay(500);

    // ... continue for 2 through 15 ...
}
```

Each number = 4 `digitalWrite()` calls + a `delay()`.

---

## Testing and Debugging

| Problem | Fix |
|---|---|
| All LEDs stay off | Check GND wire, check pin connections |
| One LED never lights | That LED or resistor is loose or backwards |
| Counter skips a number | Check HIGH/LOW against the binary table |
| Too fast to read | Increase `delay(500)` to `delay(1000)` |
| Count looks backwards | Pins 13 and 10 might be swapped |

**Pro tip:** If it doesn't work, check the simplest things first — loose wires, backwards LED, wrong pin.

---

## What's Next

After the binary counter works, the next challenge is the **Binary Guessing Game** — the Arduino picks a random number, shows it on the LEDs, and you guess the decimal value through the Serial Monitor.

That will introduce:
- The **Serial Monitor** for two-way communication
- **Random numbers** with `random()` and `randomSeed()`
- **Custom functions** to keep code organized
- The **bitwise AND operator** (`&`) to check individual bits

---

## Key Takeaways

- 4 LEDs = 4 bits = numbers 0–15 in binary
- Each LED represents a place value: 8, 4, 2, 1
- The code is repetitive but straightforward: set 4 pins for each number
- This project directly applies the binary math from Lesson 03
- Building circuits from diagrams is a core engineering skill
