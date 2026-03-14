# Arduino Walkthrough: Build a 4-LED Binary Counter

**Programming — Medina County Career Center**

---

## What We're Doing

You're going to wire 4 LEDs on your breadboard and program them to count from 0 to 15 in binary. This project puts your binary math knowledge from Lesson 03 into action on real hardware.

**Your options:**
- **Option A:** Watch Paul McWhorter's Lesson 6 on YouTube and follow along: https://www.youtube.com/watch?v=KEtut8pzXZA
- **Option B:** Follow this written guide below — same result, your own pace

Either way, complete the task at the bottom of this document.

---

## Part 1 — Gather Your Components

From your kit:

- Arduino Uno R4 WiFi (with USB cable)
- Breadboard
- **4 LEDs** (red recommended — easiest to see)
- **4 × 1KΩ resistors** (brown-black-red-gold)
- **5 jumper wires** (4 for signal pins + 1 for GND)

**Don't plug in USB yet.** Build the circuit first.

---

## Part 2 — Build the Circuit

### Pin Assignments

| LED Position | Arduino Pin | Place Value | Role |
|---|---|---|---|
| Leftmost | Pin 13 | 8s | Most significant bit |
| Second from left | Pin 12 | 4s | |
| Second from right | Pin 11 | 2s | |
| Rightmost | Pin 10 | 1s | Least significant bit |

### Wiring Pattern (Repeat 4 Times)

Each LED follows the same pattern you learned in Lesson 02:

```
Arduino Pin  →  LED long leg(+)  →  LED short leg(−)  →  1KΩ resistor  →  GND rail
```

### Step-by-Step

**Step 1: Wire LED 1 (Pin 13 — 8s place)**
1. Push LED into the breadboard: long leg in one row, short leg in the next row
2. Resistor from the short leg's row to the GND rail
3. Jumper wire from Arduino **pin 13** to the long leg's row

**Step 2: Wire LED 2 (Pin 12 — 4s place)**
Same pattern, a few rows over from LED 1.

**Step 3: Wire LED 3 (Pin 11 — 2s place)**
Same pattern, a few rows over from LED 2.

**Step 4: Wire LED 4 (Pin 10 — 1s place)**
Same pattern, a few rows over from LED 3.

**Step 5: Connect GND**
One jumper wire from **Arduino GND** to the **GND rail** (− rail) on the breadboard.

### Layout Example

```
Arduino                        Breadboard
─────────                      ──────────────────────────────────────
Pin 13 ──[wire]──────────────► row 5   [LED+]──[LED−] row 6 ──[1KΩ]──► GND rail
Pin 12 ──[wire]──────────────► row 10  [LED+]──[LED−] row 11──[1KΩ]──► GND rail
Pin 11 ──[wire]──────────────► row 15  [LED+]──[LED−] row 16──[1KΩ]──► GND rail
Pin 10 ──[wire]──────────────► row 20  [LED+]──[LED−] row 21──[1KΩ]──► GND rail
GND    ──[wire]──────────────► GND rail (− rail)
```

Leave a few rows between each LED so the circuit isn't cramped.

### Wiring Checklist

Before plugging in USB:
- [ ] All 4 LED long legs (+) face the Arduino pin wires
- [ ] All 4 LED short legs (−) connect through a resistor to GND
- [ ] Each LED has its **own** resistor — no sharing
- [ ] One GND wire connects Arduino GND to the breadboard GND rail
- [ ] Pin assignments: leftmost LED = Pin 13 (8s), rightmost = Pin 10 (1s)
- [ ] Nothing is loose — push components in firmly

---

## Part 3 — Write the Code

Plug in your Arduino via USB. Open the Arduino IDE. Create a new sketch.

### Setup

Declare all four pins as OUTPUT:

```cpp
void setup() {
    pinMode(13, OUTPUT);  // 8s place (leftmost LED)
    pinMode(12, OUTPUT);  // 4s place
    pinMode(11, OUTPUT);  // 2s place
    pinMode(10, OUTPUT);  // 1s place (rightmost LED)
}
```

### The Counter

Each number gets its own block of four `digitalWrite` lines followed by a `delay`. Use the binary table from Lesson 03 — go row by row.

Here are the first several numbers. **You need to fill in 5 through 15:**

```cpp
void loop() {

    // 0 — 0000 (all off)
    digitalWrite(13, LOW); digitalWrite(12, LOW); digitalWrite(11, LOW); digitalWrite(10, LOW);
    delay(500);

    // 1 — 0001
    digitalWrite(13, LOW); digitalWrite(12, LOW); digitalWrite(11, LOW); digitalWrite(10, HIGH);
    delay(500);

    // 2 — 0010
    digitalWrite(13, LOW); digitalWrite(12, LOW); digitalWrite(11, HIGH); digitalWrite(10, LOW);
    delay(500);

    // 3 — 0011
    digitalWrite(13, LOW); digitalWrite(12, LOW); digitalWrite(11, HIGH); digitalWrite(10, HIGH);
    delay(500);

    // 4 — 0100
    digitalWrite(13, LOW); digitalWrite(12, HIGH); digitalWrite(11, LOW); digitalWrite(10, LOW);
    delay(500);

    // 5 through 15: use the binary table and continue the pattern...
    // (you need to write these yourself)



    // Pause at the end before counting again
    delay(2000);
}
```

### Upload and Test

```
Tools → Board → Arduino UNO R4 WiFi
Tools → Port → (your board's COM port)
Click Upload →
```

Watch your LEDs. They should count up from 0 (all off) through 15 (all on), pause, then start over.

Press the **reset button** on the board (small white button) to restart from 0.

---

## Part 4 — Troubleshoot

| Problem | Likely Cause |
|---|---|
| All LEDs stay off | Wiring issue — check GND connection and long leg direction |
| One LED never turns on | That LED or its resistor is loose or backwards |
| Counter skips a number | Check the HIGH/LOW values for that row against the binary table |
| Counter is too fast to read | Increase `delay(500)` to `delay(1000)` |
| Upload fails | Check Tools → Port and make sure USB is connected |
| Count looks mirrored | Pin 13 and Pin 10 might be swapped in your wiring |

---

## Part 5 — Complete the Counter

Your job: fill in numbers 5 through 15. Use the binary table from Lesson 03:

| Decimal | Pin 13 (8s) | Pin 12 (4s) | Pin 11 (2s) | Pin 10 (1s) |
|---|---|---|---|---|
| 5 | LOW | HIGH | LOW | HIGH |
| 6 | LOW | HIGH | HIGH | LOW |
| 7 | LOW | HIGH | HIGH | HIGH |
| 8 | HIGH | LOW | LOW | LOW |
| 9 | HIGH | LOW | LOW | HIGH |
| 10 | HIGH | LOW | HIGH | LOW |
| 11 | HIGH | LOW | HIGH | HIGH |
| 12 | HIGH | HIGH | LOW | LOW |
| 13 | HIGH | HIGH | LOW | HIGH |
| 14 | HIGH | HIGH | HIGH | LOW |
| 15 | HIGH | HIGH | HIGH | HIGH |

---

## Completion Checklist

- [ ] Circuit wired: 4 LEDs on pins 13, 12, 11, 10 with resistors
- [ ] Code compiles and uploads without errors
- [ ] Counter displays all 16 numbers (0–15) correctly
- [ ] LEDs match the binary table for every number
- [ ] 2-second pause at the end before restarting
- [ ] Code has comments labeling each number

**When your counter is working correctly, show it to your instructor. You're done!**
