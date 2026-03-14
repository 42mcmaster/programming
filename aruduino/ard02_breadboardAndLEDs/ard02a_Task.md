# ard02a — External LED Patterns

**Programming — Medina County Career Center**
**Standards: ODE 5.2.1, 5.4.2, 5.4.3, 5.4.6, 5.4.7**

---

## Before You Start

You'll be wiring LEDs on a breadboard and writing Arduino sketches to control them. For each program:

1. Build or modify the circuit as described
2. Create a new sketch in the Arduino IDE
3. Write the code, upload, and observe
4. Use the Serial Monitor to verify behavior

**Keep the Study Guide open** — it has wiring diagrams, code examples, and vocabulary you'll need.

**Important:** Always disconnect USB before changing your wiring. Reconnect when you're ready to upload.

---

## Part 1: Walkthrough Examples

---

### Walkthrough 1: Single LED Blink (Build + Copy-Paste)

**Build the circuit:**
Wire one LED on **pin 8** following the walkthrough (Part 4). If you already did this, you're set.

**Copy and paste** this sketch:

```cpp
void setup() {
    pinMode(8, OUTPUT);
    Serial.begin(9600);
    Serial.println("Single LED on pin 8 - blinking");
}

void loop() {
    digitalWrite(8, HIGH);
    delay(1000);
    digitalWrite(8, LOW);
    delay(1000);
}
```

Upload and observe.

**Question:** How is this different from the Lesson 01 blink code? What changed in the code, and what changed in the hardware?

```
YOUR ANSWER:


```

---

### Walkthrough 2: Two-LED Alternating (Build + Type)

**Add a second LED** on **pin 9** — same wiring pattern as the first one, just in different rows.

**Type this sketch:**

```cpp
void setup() {
    pinMode(8, OUTPUT);
    pinMode(9, OUTPUT);
    Serial.begin(9600);
    Serial.println("Two LEDs alternating");
}

void loop() {
    digitalWrite(8, HIGH);
    digitalWrite(9, LOW);
    Serial.println("LED 8: ON   LED 9: OFF");
    delay(500);

    digitalWrite(8, LOW);
    digitalWrite(9, HIGH);
    Serial.println("LED 8: OFF  LED 9: ON");
    delay(500);
}
```

Upload and observe.

**Question:** Why do we set pin 8 HIGH and pin 9 LOW in the same block? What would happen if we only wrote `digitalWrite(8, HIGH)` without the `digitalWrite(9, LOW)`?

```
YOUR ANSWER:


```

---

### Walkthrough 3: Three-LED Chase with a Loop (Build + Type)

**Add a third LED** on **pin 10**.

**Type this sketch:**

```cpp
void setup() {
    for (int pin = 8; pin <= 10; pin++) {
        pinMode(pin, OUTPUT);
    }
    Serial.begin(9600);
    Serial.println("3-LED chase pattern");
}

void loop() {
    for (int pin = 8; pin <= 10; pin++) {
        digitalWrite(pin, HIGH);
        Serial.print("Pin ");
        Serial.print(pin);
        Serial.println(" ON");
        delay(200);
        digitalWrite(pin, LOW);
    }
}
```

Upload and observe.

**Question:** The `for` loop in `setup()` sets all three pins as OUTPUT in one loop. Write out what three lines of code the loop replaces:

```
YOUR ANSWER:


```

**What to notice:**
- Using a loop makes the code shorter and easier to change (add pin 11 by changing `10` to `11`)
- Each LED lights up briefly, then the next one does — creating a "chase" or "running light" effect
- The `delay(200)` controls the speed of the chase

---

## Part 2: Your Tasks

---

### Task 1: Back and Forth

You should have **3 LEDs** wired on pins 8, 9, and 10 from the walkthroughs.

**What to do:**
Create a "back and forth" pattern — the light moves left to right, then right to left (like the lights on KITT from Knight Rider, or a Cylon from Battlestar Galactica).

Pattern: 8 → 9 → 10 → 9 → 8 → 9 → 10 → 9 → (repeat)

Each LED should be on for 150ms. Print which LED is active to the Serial Monitor.

**Your starter code:**
```cpp
void setup() {
    for (int pin = 8; pin <= 10; pin++) {
        pinMode(pin, OUTPUT);
    }
    Serial.begin(9600);
    Serial.println("Back and forth pattern");
}

void loop() {
    // Go forward: 8, 9, 10
    // Then go backward: 9 (skip 10 and 8 to avoid double-blink at the ends)
    // Each step: turn on LED, delay 150, turn off LED, print to Serial
}
```

**Hint:** You can use two `for` loops — one counting up (8 to 10), one counting down (9 to 9, which is just pin 9). Or you could count up 8 to 10, then do pin 9 manually.

---

### Task 2: LED Counter

**What to do:**
Use your 3 LEDs to count in binary from 0 to 7. With 3 bits, you can represent all numbers from 0 (all off) to 7 (all on).

| Decimal | Pin 10 (4s) | Pin 9 (2s) | Pin 8 (1s) |
|---|---|---|---|
| 0 | OFF | OFF | OFF |
| 1 | OFF | OFF | ON |
| 2 | OFF | ON | OFF |
| 3 | OFF | ON | ON |
| 4 | ON | OFF | OFF |
| 5 | ON | OFF | ON |
| 6 | ON | ON | OFF |
| 7 | ON | ON | ON |

Display each number for 1 second. Print the number and its LED states to the Serial Monitor. After 7, pause for 2 seconds, then start over.

**Your starter code:**
```cpp
void setup() {
    pinMode(8, OUTPUT);   // 1s place
    pinMode(9, OUTPUT);   // 2s place
    pinMode(10, OUTPUT);  // 4s place
    Serial.begin(9600);
    Serial.println("3-bit binary counter: 0 to 7");
}

void loop() {
    // 0: all off
    digitalWrite(10, LOW); digitalWrite(9, LOW); digitalWrite(8, LOW);
    Serial.println("0 = OFF OFF OFF");
    delay(1000);

    // 1: just pin 8
    digitalWrite(10, LOW); digitalWrite(9, LOW); digitalWrite(8, HIGH);
    Serial.println("1 = OFF OFF ON");
    delay(1000);

    // Continue for 2 through 7...

    // Pause before restarting
    delay(2000);
}
```

---

### Task 3: Randomized Blink

**What to do:**
Write a program that randomly picks one of the three LEDs and blinks it. Each round:
1. Pick a random pin (8, 9, or 10)
2. Turn on that LED for 300ms
3. Turn it off
4. Print which pin was selected to Serial Monitor
5. Wait 200ms before the next round

**Useful functions:**
- `random(8, 11)` — returns a random number: 8, 9, or 10 (the upper bound is excluded)
- `randomSeed(analogRead(0))` — put this in `setup()` for better randomness

**Your starter code:**
```cpp
void setup() {
    for (int pin = 8; pin <= 10; pin++) {
        pinMode(pin, OUTPUT);
    }
    Serial.begin(9600);
    randomSeed(analogRead(0));
    Serial.println("Random LED blinker");
}

void loop() {
    // Pick a random pin between 8 and 10
    // Turn it on, delay 300, turn it off
    // Print which pin blinked
    // Delay 200 before next round
}
```

**Expected Serial Monitor output (yours will be different — it's random):**
```
Random LED blinker
Pin 9 blinked
Pin 8 blinked
Pin 10 blinked
Pin 10 blinked
Pin 8 blinked
...
```

---

## Compilation Reminder

Arduino compiles and uploads in one step:
- Click the **Upload** button (right arrow)
- Watch the console at the bottom for errors or "Done uploading"

Common issues for this lesson:
- LED wired backwards — flip it (long leg toward pin wire)
- Missing GND connection — make sure Arduino GND connects to the GND rail
- Wrong pin number in code — double check which row your LED is wired to
- LEDs sharing a resistor — each LED needs its own

---

## Submission Checklist

- [ ] All walkthrough questions answered
- [ ] Task 1: Back-and-forth pattern — smooth, no double-blink at the ends
- [ ] Task 2: Binary counter 0–7 — all 8 states correct, Serial output matches LEDs
- [ ] Task 3: Random blinker — different LED each time, Serial shows which pin
- [ ] All code has comments explaining what it does
- [ ] Circuit is neat — no loose wires, LEDs clearly visible
