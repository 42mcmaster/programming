# ard01a — Blink Variations

**Programming — Medina County Career Center**
**Standards: ODE 5.4.2, 5.4.3, 5.2.1, 5.2.3, 5.4.6**

---

## Before You Start

You'll be writing Arduino sketches in the **Arduino IDE** and uploading them to your Arduino Uno R4 WiFi. For each program:

1. Create a new sketch: **File → New Sketch**
2. Write (or paste) the code
3. Save it with a descriptive name
4. Click the **Upload** button (right arrow) to compile and send to the board
5. Observe the LED on pin 13

**Keep the Study Guide open** — it has syntax reference and examples you'll need.

---

## Part 1: Walkthrough Examples

These examples get you comfortable with the blink pattern. Follow the instructions for each one.

---

### Walkthrough 1: Basic Blink (Copy-Paste)

**Copy and paste** this sketch into a new file and upload it:

```cpp
void setup() {
    pinMode(13, OUTPUT);
}

void loop() {
    digitalWrite(13, HIGH);
    delay(1000);
    digitalWrite(13, LOW);
    delay(1000);
}
```

Upload and observe.

**Question:** How many times does the LED blink in 10 seconds?

```
YOUR ANSWER:


```

**What to notice:**
- `pinMode(13, OUTPUT)` is in `setup()` — it runs once
- The four lines in `loop()` run over and over: on, wait, off, wait
- 1000 milliseconds = 1 second, so this is a 2-second cycle (1s on + 1s off)

---

### Walkthrough 2: Fast Blink (Type This One)

**Type this sketch yourself** into a new file:

```cpp
void setup() {
    pinMode(13, OUTPUT);
    Serial.begin(9600);
    Serial.println("Fast blink starting!");
}

void loop() {
    digitalWrite(13, HIGH);
    delay(100);
    digitalWrite(13, LOW);
    delay(100);
}
```

Upload and observe. Open the **Serial Monitor** (Tools → Serial Monitor) to see the startup message.

**Question:** How does 100ms compare to 1000ms? Can you still see individual blinks?

```
YOUR ANSWER:


```

**What to notice:**
- `delay(100)` is 1/10 of a second — much faster than the first example
- `Serial.begin(9600)` and `Serial.println()` are in `setup()` so the message prints once
- The LED blinks rapidly but you can still see it at 100ms

---

### Walkthrough 3: Heartbeat Pattern (Type This One)

**Type this sketch** — it creates an asymmetric blink that looks like a heartbeat:

```cpp
void setup() {
    pinMode(13, OUTPUT);
}

void loop() {
    // First beat
    digitalWrite(13, HIGH);
    delay(100);
    digitalWrite(13, LOW);
    delay(100);

    // Second beat
    digitalWrite(13, HIGH);
    delay(100);
    digitalWrite(13, LOW);

    // Pause between heartbeats
    delay(700);
}
```

Upload and observe.

**Question:** Describe the pattern you see. How is it different from a simple on/off blink?

```
YOUR ANSWER:


```

**What to notice:**
- Two quick flashes followed by a longer pause creates a "heartbeat" rhythm
- The total cycle time is 100 + 100 + 100 + 100 + 700 = 1100ms (about 1.1 seconds)
- You can create complex patterns by combining `digitalWrite()` and `delay()` calls

---

## Part 2: Your Tasks

Now it's your turn. Use the Study Guide and the walkthrough examples above as reference.

---

### Task 1: Slow and Steady

Create a new sketch.

**What to do:**
Make the LED blink with a **3-second on, 1-second off** pattern. Also use `Serial.println()` to print "ON" when the LED turns on and "OFF" when it turns off.

**Your starter code:**
```cpp
void setup() {
    pinMode(13, OUTPUT);
    Serial.begin(9600);
}

void loop() {
    // Turn LED on, print "ON", wait 3 seconds
    // Turn LED off, print "OFF", wait 1 second
}
```

**Expected Serial Monitor output:**
```
ON
OFF
ON
OFF
...
```

---

### Task 2: Five Blinks Then Pause

Create a new sketch.

**What to do:**
Use a `for` loop to blink the LED **5 times quickly** (200ms on, 200ms off each), then pause for **2 seconds** before repeating. Print the blink count to the Serial Monitor.

**Here's how a for loop looks in Arduino (same as C):**
```cpp
for (int i = 1; i <= 5; i++) {
    // This runs 5 times, with i going from 1 to 5
}
```

**Your starter code:**
```cpp
void setup() {
    pinMode(13, OUTPUT);
    Serial.begin(9600);
}

void loop() {
    // Use a for loop to blink 5 times
    // Inside the loop: turn on, delay 200, turn off, delay 200
    // Print the blink number each time: "Blink 1", "Blink 2", etc.

    // After the loop: print "Pausing..." and delay 2000
}
```

**Expected Serial Monitor output:**
```
Blink 1
Blink 2
Blink 3
Blink 4
Blink 5
Pausing...
Blink 1
Blink 2
...
```

---

### Task 3: Variable Speed Blink

Create a new sketch.

**What to do:**
Start with a slow blink (1000ms delay) and gradually speed up. Use a variable called `delayTime` that starts at 1000 and decreases by 100 each time through the loop. When it reaches 100, reset it back to 1000. Print the current delay time to the Serial Monitor.

**Your starter code:**
```cpp
int delayTime = 1000;

void setup() {
    pinMode(13, OUTPUT);
    Serial.begin(9600);
}

void loop() {
    // Print the current delay time
    // Blink the LED using delayTime for both on and off

    // Decrease delayTime by 100
    // If delayTime reaches less than 100, reset it to 1000
}
```

**Expected behavior:** The LED starts blinking slowly, speeds up over about 10 cycles, then jumps back to slow and repeats.

**Expected Serial Monitor output:**
```
Delay: 1000
Delay: 900
Delay: 800
...
Delay: 200
Delay: 100
Delay: 1000
Delay: 900
...
```

---

### Task 4: Blink Counter with Total

Create a new sketch.

**What to do:**
Count how many times the LED has blinked since the program started. Blink at 500ms on, 500ms off. Print the blink number and the total elapsed time (in seconds) to the Serial Monitor.

**Hint:** If each full blink cycle is 1 second (500ms on + 500ms off), then `blinkCount` also equals the number of seconds elapsed.

**Your starter code:**
```cpp
int blinkCount = 0;

void setup() {
    pinMode(13, OUTPUT);
    Serial.begin(9600);
    Serial.println("Blink counter started!");
}

void loop() {
    // Increment blinkCount
    // Turn LED on, delay 500
    // Turn LED off, delay 500
    // Print: "Blink #X — Total time: Xs"
    // Hint: Serial.print() and Serial.println() can be chained
}
```

**Expected Serial Monitor output:**
```
Blink counter started!
Blink #1 - Total time: 1s
Blink #2 - Total time: 2s
Blink #3 - Total time: 3s
...
```

---

## Compilation Reminder

Arduino compiles and uploads in one step:
- Click the **Upload** button (right arrow)
- Watch the console at the bottom for errors or "Done uploading"

Common issues:
- Missing semicolon `;` — check the line the error points to
- Wrong case: `pinmode` should be `pinMode`, `digitalwrite` should be `digitalWrite`
- Wrong board or port selected in Tools menu
- Forgot `Serial.begin(9600)` before using `Serial.println()`

---

## Submission Checklist

- [ ] All walkthrough questions answered
- [ ] Task 1: Slow blink with Serial output — compiles, uploads, LED and serial work
- [ ] Task 2: Five blinks then pause with loop — compiles, uploads, pattern correct
- [ ] Task 3: Variable speed blink — compiles, uploads, speeds up and resets
- [ ] Task 4: Blink counter — compiles, uploads, count and time display correctly
- [ ] All code has comments explaining what it does
