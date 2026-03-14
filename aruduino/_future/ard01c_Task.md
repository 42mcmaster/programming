# ard01c — LED Patterns and Serial Control

**Programming — Medina County Career Center**
**Standards: ODE 5.2.1, 5.3.5, 5.3.6, 5.3.9, 5.4.6, 5.4.7, 5.5.5**

---

## Before You Start

This is the most advanced task file in Arduino Lesson 01. You'll combine everything you've learned — `digitalWrite()`, `delay()`, loops, functions, variables, and the Serial Monitor — to create more complex LED behaviors and introduce **Serial input** (reading commands from your computer).

For each program:
1. Create a new sketch in the Arduino IDE
2. Write (or paste) the code
3. Upload to your board and observe
4. Use the Serial Monitor for output and input

**Keep the Study Guide open** — it has syntax reference and examples you'll need.

---

## Part 1: Walkthrough Examples

---

### Walkthrough 1: Reading Serial Input (Copy-Paste)

So far we've only **sent** text from the Arduino to the computer. Now let's **receive** text from the computer to the Arduino. This is like `scanf` in C.

**Copy and paste** this sketch:

```cpp
void setup() {
    pinMode(13, OUTPUT);
    Serial.begin(9600);
    Serial.println("Type 'on' or 'off' to control the LED:");
}

void loop() {
    if (Serial.available() > 0) {
        char command = Serial.read();

        if (command == '1') {
            digitalWrite(13, HIGH);
            Serial.println("LED is ON");
        } else if (command == '0') {
            digitalWrite(13, LOW);
            Serial.println("LED is OFF");
        }
    }
}
```

Upload it. Open the Serial Monitor. Type `1` and press Enter — the LED turns on. Type `0` and press Enter — it turns off.

**Question:** What does `Serial.available()` check? Why do we need the `if` statement around it?

```
YOUR ANSWER:


```

**What to notice:**
- `Serial.available()` returns how many characters are waiting to be read
- `Serial.read()` reads one character at a time
- We check for `'1'` and `'0'` (character, not number — note the single quotes)
- Without the `if (Serial.available() > 0)` check, `Serial.read()` would return -1 when there's nothing to read

---

### Walkthrough 2: Blink Count from Serial Input (Type This One)

**Type this sketch** — it lets you type a number to control how many times the LED blinks:

```cpp
void setup() {
    pinMode(13, OUTPUT);
    Serial.begin(9600);
    Serial.println("Enter a digit (1-9) to blink that many times:");
}

void loop() {
    if (Serial.available() > 0) {
        char input = Serial.read();

        // Convert character digit to actual number
        // '1' is ASCII 49, '0' is ASCII 48, so '1' - '0' = 1
        if (input >= '1' && input <= '9') {
            int count = input - '0';

            Serial.print("Blinking ");
            Serial.print(count);
            Serial.println(" times...");

            for (int i = 0; i < count; i++) {
                digitalWrite(13, HIGH);
                delay(300);
                digitalWrite(13, LOW);
                delay(300);
            }

            Serial.println("Done! Enter another number:");
        }
    }
}
```

Upload and try it. Type `3` — the LED blinks 3 times. Type `7` — it blinks 7 times.

**Question:** How does `input - '0'` convert a character to a number? (Hint: Think about ASCII values from our C lessons.)

```
YOUR ANSWER:


```

**What to notice:**
- `input >= '1' && input <= '9'` validates the input before using it
- `input - '0'` converts the ASCII character to its numeric value — same trick from C!
- The `for` loop blinks exactly `count` times, then waits for more input

---

## Part 2: Your Tasks

---

### Task 1: Emergency Flasher Patterns

Create a new sketch.

**What to do:**
Write a program with **three different blink patterns** that the user can switch between by typing a number in the Serial Monitor:

- **Pattern 1** — Steady blink: 500ms on, 500ms off
- **Pattern 2** — Rapid strobe: 50ms on, 50ms off
- **Pattern 3** — Double flash: two quick flashes (100ms on, 100ms off, 100ms on) then a long pause (800ms off)

Use a variable `currentPattern` to track which pattern is active. In each cycle of `loop()`, check for Serial input to change the pattern, then execute the current pattern.

**Your starter code:**
```cpp
int ledPin = 13;
int currentPattern = 1;

void setup() {
    pinMode(ledPin, OUTPUT);
    Serial.begin(9600);
    Serial.println("Emergency Flasher");
    Serial.println("Type 1, 2, or 3 to switch patterns:");
}

void pattern1() {
    // Steady blink: 500ms on, 500ms off
}

void pattern2() {
    // Rapid strobe: 50ms on, 50ms off
}

void pattern3() {
    // Double flash: on 100, off 100, on 100, off 800
}

void loop() {
    // Check for Serial input to change pattern
    if (Serial.available() > 0) {
        char input = Serial.read();
        if (input == '1') {
            currentPattern = 1;
            Serial.println("Pattern 1: Steady");
        } else if (input == '2') {
            currentPattern = 2;
            Serial.println("Pattern 2: Strobe");
        } else if (input == '3') {
            currentPattern = 3;
            Serial.println("Pattern 3: Double Flash");
        }
    }

    // Execute the current pattern
    // Use if/else to call the right pattern function based on currentPattern
}
```

**Expected behavior:** The LED runs one pattern until you type a different number.

---

### Task 2: Reaction Time Tester

Create a new sketch.

**What to do:**
Build a simple reaction time game:

1. The LED turns off and the program waits a random amount of time (between 2 and 5 seconds)
2. The LED turns on
3. The player must type **any character** in the Serial Monitor as fast as they can
4. The program measures how long it took and prints the reaction time

**Useful functions:**
- `millis()` — returns the number of milliseconds since the Arduino started (like a stopwatch)
- `random(min, max)` — returns a random number between `min` and `max-1`
- `randomSeed(analogRead(0))` — seeds the random number generator (put in `setup()`)

**Your starter code:**
```cpp
void setup() {
    pinMode(13, OUTPUT);
    Serial.begin(9600);
    randomSeed(analogRead(0));  // Seed random number generator
    Serial.println("=== Reaction Time Tester ===");
    Serial.println("When the LED turns on, type any key as fast as you can!");
    delay(2000);
}

void loop() {
    // Turn LED off
    digitalWrite(13, LOW);
    Serial.println("Wait for it...");

    // Wait a random amount of time (2000 to 5000 ms)
    int waitTime = random(2000, 5001);
    delay(waitTime);

    // Turn LED on and record the start time
    digitalWrite(13, HIGH);
    Serial.println("NOW! Press any key!");
    unsigned long startTime = millis();

    // Wait for the player to send a character
    while (Serial.available() == 0) {
        // Do nothing — just wait
    }

    // Player responded! Calculate reaction time
    unsigned long reactionTime = millis() - startTime;

    // Clear the serial buffer
    while (Serial.available() > 0) {
        Serial.read();
    }

    // Print the result
    // YOUR CODE HERE: Print the reaction time
    // If reactionTime < 300, print "Excellent!"
    // If reactionTime < 500, print "Good!"
    // Otherwise print "Keep practicing!"

    Serial.println();
    delay(2000);  // Pause before next round
}
```

**Expected Serial Monitor output:**
```
=== Reaction Time Tester ===
When the LED turns on, type any key as fast as you can!
Wait for it...
NOW! Press any key!
Reaction time: 287ms - Excellent!

Wait for it...
NOW! Press any key!
Reaction time: 412ms - Good!
```

---

### Task 3: Binary Counter Display

Create a new sketch.

**What to do:**
Use the LED on pin 13 to **visually display a number in binary**. Count from 0 to 15 (4-bit binary), blinking each bit of the number. A long flash means `1`, a short flash means `0`.

For example, the number 13 in binary is `1101`:
- Long flash (1)
- Long flash (1)
- Short flash (0)
- Long flash (1)

After displaying all 4 bits, pause, then move to the next number.

**Hint:** To check if a specific bit is set, use the bitwise AND operator:
```cpp
if (number & (1 << bitPosition)) {
    // Bit is 1
} else {
    // Bit is 0
}
```

This is the same bitwise logic from our C lessons!

**Your starter code:**
```cpp
int ledPin = 13;
int longFlash = 600;    // Duration for '1'
int shortFlash = 150;   // Duration for '0'
int bitGap = 400;       // Gap between bits
int numberGap = 2000;   // Gap between numbers

void setup() {
    pinMode(ledPin, OUTPUT);
    Serial.begin(9600);
    Serial.println("Binary Counter: 0 to 15");
}

void blinkBit(int value) {
    // If value is 1: long flash
    // If value is 0: short flash
    // Then turn off and wait bitGap
}

void displayNumber(int num) {
    Serial.print(num);
    Serial.print(" = ");

    // Loop through bits 3 down to 0 (most significant first)
    for (int bit = 3; bit >= 0; bit--) {
        int bitValue = (num >> bit) & 1;
        Serial.print(bitValue);
        blinkBit(bitValue);
    }

    Serial.println();
}

void loop() {
    for (int i = 0; i <= 15; i++) {
        displayNumber(i);
        delay(numberGap);
    }

    Serial.println("--- Restarting ---");
    delay(3000);
}
```

**Expected Serial Monitor output:**
```
Binary Counter: 0 to 15
0 = 0000
1 = 0001
2 = 0010
3 = 0011
...
13 = 1101
14 = 1110
15 = 1111
--- Restarting ---
```

**Expected LED behavior:** For each number, you see 4 flashes — long for 1, short for 0. This ties back to the binary/encoding concepts from our C unit (competency 2.3.2).

---

## Compilation Reminder

- Click the **Upload** button (right arrow) to compile and upload
- Open **Serial Monitor** (Tools → Serial Monitor) at **9600** baud for output/input
- For input tasks: type in the text box at the top of the Serial Monitor and press Enter

Common issues at this level:
- `millis()` returns `unsigned long` — use that type for time variables
- `random()` needs `randomSeed()` in setup or it gives the same sequence every time
- `Serial.available()` counts characters waiting — check before reading
- Bitwise operators (`&`, `>>`, `<<`) work exactly like in C

---

## Submission Checklist

- [ ] All walkthrough questions answered
- [ ] Task 1: Emergency flasher — all 3 patterns work, Serial switching works
- [ ] Task 2: Reaction time tester — random wait, accurate timing, feedback messages
- [ ] Task 3: Binary counter — correct binary display, LED flashes match bits
- [ ] All code has comments explaining what it does
