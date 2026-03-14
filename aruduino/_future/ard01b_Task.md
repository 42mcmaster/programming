# ard01b — Morse Code SOS

**Programming — Medina County Career Center**
**Standards: ODE 5.2.1, 5.3.6, 5.4.2, 5.4.3, 5.4.6, 5.4.7**

---

## Before You Start

In this task, you'll use the built-in LED on pin 13 to blink **Morse code** messages. Morse code uses short and long flashes of light (called dots and dashes) to represent letters. This is a classic Arduino exercise — and it's how the first long-distance messages were sent before phones existed.

For each program:
1. Create a new sketch in the Arduino IDE
2. Write (or paste) the code
3. Upload to your board and observe the LED
4. Use the Serial Monitor to verify your timing

**Keep the Study Guide open** — it has syntax reference and examples you'll need.

---

## Morse Code Basics

Morse code has specific timing rules:

| Element | Duration |
|---|---|
| **Dot** (short flash) | 1 unit |
| **Dash** (long flash) | 3 units |
| **Gap between dots/dashes** (within a letter) | 1 unit (LED off) |
| **Gap between letters** | 3 units (LED off) |
| **Gap between words** | 7 units (LED off) |

We'll use **200 milliseconds** as 1 unit. So:

| Element | Time |
|---|---|
| Dot | 200ms on |
| Dash | 600ms on |
| Gap within letter | 200ms off |
| Gap between letters | 600ms off |
| Gap between words | 1400ms off |

### SOS in Morse Code

```
S = · · ·     (three dots)
O = — — —     (three dashes)
S = · · ·     (three dots)
```

So the full SOS pattern is:
```
dot gap dot gap dot [letter gap] dash gap dash gap dash [letter gap] dot gap dot gap dot [word gap]
```

---

## Part 1: Walkthrough Examples

---

### Walkthrough 1: A Single Dot (Copy-Paste)

**Copy and paste** this sketch to see a single dot pattern:

```cpp
int ledPin = 13;
int unitTime = 200;  // 1 unit = 200ms

void setup() {
    pinMode(ledPin, OUTPUT);
    Serial.begin(9600);
}

void dot() {
    digitalWrite(ledPin, HIGH);
    delay(unitTime);              // On for 1 unit
    digitalWrite(ledPin, LOW);
    delay(unitTime);              // Off for 1 unit (gap within letter)
    Serial.print(".");
}

void loop() {
    dot();
    delay(2000);  // Pause so you can see each dot separately
}
```

Upload and observe.

**Question:** How long is the LED on for each dot? How long is it off?

```
YOUR ANSWER:


```

**What to notice:**
- We created a **function** called `dot()` that handles one dot
- Variables at the top (`ledPin`, `unitTime`) make it easy to change values
- `Serial.print(".")` logs a dot character each time — no newline so they stay on one line
- Functions in Arduino work just like functions in C

---

### Walkthrough 2: A Single Dash (Type This One)

**Add this function** to your sketch from Walkthrough 1, right below the `dot()` function:

```cpp
void dash() {
    digitalWrite(ledPin, HIGH);
    delay(unitTime * 3);         // On for 3 units
    digitalWrite(ledPin, LOW);
    delay(unitTime);              // Off for 1 unit (gap within letter)
    Serial.print("-");
}
```

Now change your `loop()` to test both:

```cpp
void loop() {
    dot();
    delay(1000);
    dash();
    delay(1000);
}
```

Upload and observe.

**Question:** Can you clearly see the difference between a dot and a dash? How much longer is the dash?

```
YOUR ANSWER:


```

**What to notice:**
- `delay(unitTime * 3)` makes the dash three times longer than a dot
- We can do math inside `delay()` — it just needs a number
- Both functions end with a 1-unit gap (the gap within a letter)

---

### Walkthrough 3: The Letter S (Type This One)

**Type this `loop()` function** to blink the letter S (three dots):

```cpp
void loop() {
    // Letter S: three dots
    dot();
    dot();
    dot();

    Serial.println(" (S)");

    delay(3000);  // Long pause before repeating
}
```

Upload and observe.

**Question:** Write out the timing of the letter S in milliseconds (how long is the LED on, how long off, for each part):

```
YOUR ANSWER:


```

---

## Part 2: Your Tasks

---

### Task 1: SOS

Create a new sketch.

**What to do:**
Write a program that blinks the Morse code **SOS** pattern on the pin 13 LED. Use the `dot()` and `dash()` helper functions from the walkthroughs. Between letters (S, O, S), add a letter gap. After the full SOS, add a word gap before repeating.

**The pattern:**
1. S — three dots
2. Letter gap (3 units total — but `dot()` already has 1 unit of off time, so add 2 extra units)
3. O — three dashes
4. Letter gap
5. S — three dots
6. Word gap (7 units total — the last dot/dash has 1 unit of off, so add 6 extra units)

**Your starter code:**
```cpp
int ledPin = 13;
int unitTime = 200;

void setup() {
    pinMode(ledPin, OUTPUT);
    Serial.begin(9600);
    Serial.println("SOS Transmitter Ready");
}

void dot() {
    digitalWrite(ledPin, HIGH);
    delay(unitTime);
    digitalWrite(ledPin, LOW);
    delay(unitTime);
    Serial.print(".");
}

void dash() {
    digitalWrite(ledPin, HIGH);
    delay(unitTime * 3);
    digitalWrite(ledPin, LOW);
    delay(unitTime);
    Serial.print("-");
}

void loop() {
    // S: three dots
    // Add letter gap: delay(unitTime * 2);
    // Print a space to Serial

    // O: three dashes
    // Add letter gap: delay(unitTime * 2);
    // Print a space to Serial

    // S: three dots

    // Print newline and "SOS" label
    Serial.println(" SOS");

    // Word gap before repeating
    // delay(unitTime * 6);
}
```

**Expected Serial Monitor output:**
```
SOS Transmitter Ready
... --- ... SOS
... --- ... SOS
... --- ... SOS
```

**Expected LED behavior:** Three short blinks, pause, three long blinks, pause, three short blinks, longer pause, repeat.

---

### Task 2: Adjustable Speed SOS

Create a new sketch.

**What to do:**
Start with your SOS program from Task 1, but add a speed control. Use a variable `unitTime` that starts at 200ms. Each time the SOS pattern completes, decrease `unitTime` by 25ms. When it reaches 50ms, reset to 200ms. Print the current speed to the Serial Monitor.

**Your starter code:**
```cpp
int ledPin = 13;
int unitTime = 200;

void setup() {
    pinMode(ledPin, OUTPUT);
    Serial.begin(9600);
    Serial.println("Speed SOS Ready");
}

// Copy your dot() and dash() functions here

void loop() {
    Serial.print("Speed: ");
    Serial.print(unitTime);
    Serial.print("ms — ");

    // Play the full SOS pattern (same as Task 1)

    Serial.println(" SOS");

    // Decrease unitTime by 25
    // If unitTime < 50, reset to 200

    delay(unitTime * 6);  // Word gap
}
```

**Expected behavior:** The SOS gets faster and faster until it resets to slow.

---

### Task 3: Spell Your Initials

Create a new sketch.

**What to do:**
Use the Morse code alphabet below to blink **your initials** (first and last name). Use the `dot()` and `dash()` functions. Add proper letter gaps between letters and a word gap at the end before repeating.

**Morse Code Alphabet:**

```
A  .-      N  -.
B  -...    O  ---
C  -.-.    P  .--.
D  -..     Q  --.-
E  .       R  .-.
F  ..-.    S  ...
G  --.     T  -
H  ....    U  ..-
I  ..      V  ...-
J  .---    W  .--
K  -.-     X  -..-
L  .-..    Y  -.--
M  --      Z  --..
```

**Example:** If your initials are "R M":
- R = `·-·` (dot dash dot)
- Letter gap
- M = `--` (dash dash)
- Word gap, repeat

**Your approach:**
1. Write out the Morse code for each letter of your initials
2. Write a function for each letter (e.g., `void letterR()`, `void letterM()`)
3. Call the letter functions in `loop()` with proper gaps
4. Print the dots, dashes, and letter names to Serial Monitor

**Starter code:**
```cpp
int ledPin = 13;
int unitTime = 200;

void setup() {
    pinMode(ledPin, OUTPUT);
    Serial.begin(9600);
    Serial.println("Morse Code: My Initials");
}

void dot() {
    digitalWrite(ledPin, HIGH);
    delay(unitTime);
    digitalWrite(ledPin, LOW);
    delay(unitTime);
    Serial.print(".");
}

void dash() {
    digitalWrite(ledPin, HIGH);
    delay(unitTime * 3);
    digitalWrite(ledPin, LOW);
    delay(unitTime);
    Serial.print("-");
}

// Write a function for each letter of your initials
// Example:
// void letterR() {
//     dot(); dash(); dot();
//     Serial.print(" (R) ");
// }

void loop() {
    // Call your letter functions with letter gaps between them
    // Add a word gap at the end

    Serial.println();
    delay(unitTime * 6);
}
```

---

## Compilation Reminder

- Click the **Upload** button (right arrow) to compile and upload
- Check the console at the bottom for errors
- Open **Serial Monitor** (Tools → Serial Monitor) to see text output
- Make sure baud rate is **9600**

Common issues at this level:
- Forgetting to define `dot()` and `dash()` before calling them in `loop()`
- Missing semicolons after `delay()` or `digitalWrite()` calls
- Using `delay(unitTime * 2)` without parentheses — it works fine, `*` happens before the function call

---

## Submission Checklist

- [ ] All walkthrough questions answered
- [ ] Task 1: SOS pattern — correct dot/dash/gap timing, Serial output matches
- [ ] Task 2: Adjustable speed SOS — speed decreases and resets properly
- [ ] Task 3: Your initials — correct Morse code, proper gaps, Serial output shows letters
- [ ] All code has comments explaining what it does
