# ard_lesson05 — Binary Counter: Build Guide + Follow-On Task

**Programming — Medina County Career Center**
**Hardware: Arduino UNO R4**

---

## Your Options for This Lesson

After watching **Lesson 5** (binary numbers https://www.youtube.com/watch?v=cSOpMpynXAI), you have two ways to complete the binary counter build:

- 📺 **Option A:** Watch Lesson 6 on YouTube and follow along with Paul (https://www.youtube.com/watch?v=KEtut8pzXZA)
- 📄 **Option B:** Follow this written guide below — same result, your own pace

Either way, complete the follow-on task at the bottom of this document.

---

## Quick Binary Review (From Lesson 5)

Each LED represents one binary digit (bit). ON = 1, OFF = 0.

With 4 LEDs you can represent numbers 0–15:

| Decimal | Pin 13 (8s) | Pin 12 (4s) | Pin 11 (2s) | Pin 10 (1s) |
|---|---|---|---|---|
| 0  | OFF | OFF | OFF | OFF |
| 1  | OFF | OFF | OFF | ON  |
| 2  | OFF | OFF | ON  | OFF |
| 3  | OFF | OFF | ON  | ON  |
| 4  | OFF | ON  | OFF | OFF |
| 5  | OFF | ON  | OFF | ON  |
| 6  | OFF | ON  | ON  | OFF |
| 7  | OFF | ON  | ON  | ON  |
| 8  | ON  | OFF | OFF | OFF |
| 9  | ON  | OFF | OFF | ON  |
| 10 | ON  | OFF | ON  | OFF |
| 11 | ON  | OFF | ON  | ON  |
| 12 | ON  | ON  | OFF | OFF |
| 13 | ON  | ON  | OFF | ON  |
| 14 | ON  | ON  | ON  | OFF |
| 15 | ON  | ON  | ON  | ON  |

> **Tip:** Print or sketch this table before you start coding. Switching between the table and your code is much easier than trying to work out the binary in your head while typing.

---

## Safety Reminders

- **One 1KΩ resistor per LED** — no sharing
- **Long leg of LED faces the Arduino pin** — short leg faces GND
- **Build the circuit before plugging in USB**
- Max **8mA per pin** — the resistors are what keep you in that range

---

## Part 1: Build the Circuit

### Components Needed
- Arduino UNO R4
- 4 LEDs (red)
- 4 × 1KΩ resistors (brown-black-red-gold)
- Several jumper wires (red and black recommended)
- Breadboard

---

### Wiring Diagram

Each LED follows the same pattern. Wire all four the same way, using pins 13, 12, 11, and 10.

**Single LED wiring (repeat 4 times):**
```
Arduino Pin  →  LED long leg(+)  →  LED short leg(–)  →  1KΩ resistor  →  GND rail
```

**Full breadboard layout (top-down view):**

```
Arduino                        Breadboard
─────────                      ──────────────────────────────────────
Pin 13 ──[red wire]──────────► col A  [LED+]──[LED-] col B ──[1KΩ]──► GND rail
Pin 12 ──[red wire]──────────► col D  [LED+]──[LED-] col E ──[1KΩ]──► GND rail
Pin 11 ──[red wire]──────────► col G  [LED+]──[LED-] col H ──[1KΩ]──► GND rail
Pin 10 ──[red wire]──────────► col J  [LED+]──[LED-] col K ──[1KΩ]──► GND rail
GND    ──[black wire]────────► bottom power rail (GND rail)
```

**Side view of one LED + resistor across the trench:**
```
         TRENCH
left side  |  right side
           |
[LED+] [LED-] | [resistor leg 1] [resistor leg 2] → GND rail
  ^                                                      ^
  |                                                      |
Pin wire                                           black wire to GND
```

> **The resistor jumps the trench.** One leg goes in the same column as the LED's short leg (left side of trench), the other leg lands on the right side and connects down to the GND rail.

---

### Wiring Checklist (do this before plugging in USB)
- [ ] All 4 LED long legs (positive +) face LEFT (toward Arduino pins)
- [ ] All 4 LED short legs (negative -) face RIGHT (toward resistors)
- [ ] Each LED has its own resistor — no sharing
- [ ] All resistors connect to the GND rail on the right
- [ ] One black jumper wire runs from Arduino GND to the GND rail
- [ ] Pin assignments: leftmost LED = Pin 13, rightmost = Pin 10

---

## Part 2: Write the Code

Open Arduino IDE. Go to **File → Examples → Basic → Bare Minimum** to start clean.

### Step 1 — Setup (runs once)

Declare all four pins as OUTPUT:

```cpp
void setup() {
  pinMode(13, OUTPUT);  // 8s place (leftmost LED)
  pinMode(12, OUTPUT);  // 4s place
  pinMode(11, OUTPUT);  // 2s place
  pinMode(10, OUTPUT);  // 1s place (rightmost LED)
}
```

---

### Step 2 — The Counter (in loop)

Each number gets its own block of four `digitalWrite` lines followed by a `delay`. Use the table at the top of this document — go row by row.

Here is the pattern for the first several numbers. Fill in the rest using the table:

```cpp
void loop() {

  // 0 — all off
  digitalWrite(13, LOW); digitalWrite(12, LOW); digitalWrite(11, LOW); digitalWrite(10, LOW);
  delay(500);

  // 1
  digitalWrite(13, LOW); digitalWrite(12, LOW); digitalWrite(11, LOW); digitalWrite(10, HIGH);
  delay(500);

  // 2
  digitalWrite(13, LOW); digitalWrite(12, LOW); digitalWrite(11, HIGH); digitalWrite(10, LOW);
  delay(500);

  // 3
  digitalWrite(13, LOW); digitalWrite(12, LOW); digitalWrite(11, HIGH); digitalWrite(10, HIGH);
  delay(500);

  // 4
  digitalWrite(13, LOW); digitalWrite(12, HIGH); digitalWrite(11, LOW); digitalWrite(10, LOW);
  delay(500);

  // 5 — 15: follow the table above and continue the pattern...
  // (complete the remaining numbers using the binary table)

  delay(2000);  // Pause at the end before counting again
}
```

> **Important:** The `delay(2000)` at the very end gives a 2-second pause before the counter restarts at 0. Without it, the jump from 15 back to 0 looks like just another step.

---

### Step 3 — Upload and Test

```
Tools → Board → Arduino UNO R4 Minima (or WiFi)
Tools → Port → (your board's COM port)
Click Upload →
```

Watch your LEDs. Press the **reset button** on the board to restart from 0 if needed (small white button).

**If something looks wrong, check these first:**

| Problem | Likely Cause |
|---|---|
| All LEDs stay off | Wiring issue — check long leg direction and pin connections |
| One LED never turns on | That LED or its resistor is loose or backwards |
| Counter skips a number | Check the HIGH/LOW values for that row against the table |
| Counter is too fast to read | Increase `delay(500)` to `delay(1000)` |
| Upload fails | Check Tools → Port and make sure USB is connected |

---
