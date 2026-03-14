# ard02a — External LED Patterns: Teacher Solutions

**Programming — Medina County Career Center**

---

## Walkthrough Answers

### Walkthrough 1: Single LED Blink

**Q: How is this different from the Lesson 01 blink code? What changed in the code, and what changed in the hardware?**

In the code, only the pin number changed — from 13 to 8. In the hardware, instead of using the built-in LED on the board, there's now an external LED on the breadboard connected through a resistor to GND. The logic is identical: set the pin as OUTPUT, then alternate HIGH and LOW with delays.

---

### Walkthrough 2: Two-LED Alternating

**Q: Why do we set pin 8 HIGH and pin 9 LOW in the same block? What would happen if we only wrote `digitalWrite(8, HIGH)` without the `digitalWrite(9, LOW)`?**

We set both in the same block to make sure one turns on while the other turns off at the same time. If we only wrote `digitalWrite(8, HIGH)` without turning pin 9 LOW, pin 9 would stay in whatever state it was in from the previous cycle. On the first pass both LEDs would be on (since pin 9 starts HIGH from the second block of the previous loop iteration). The alternating effect requires explicitly setting both pins each time.

---

### Walkthrough 3: Three-LED Chase with a Loop

**Q: Write out what three lines of code the loop replaces:**

```cpp
pinMode(8, OUTPUT);
pinMode(9, OUTPUT);
pinMode(10, OUTPUT);
```

---

## Task Solutions

### Task 1: Back and Forth

```cpp
void setup() {
    for (int pin = 8; pin <= 10; pin++) {
        pinMode(pin, OUTPUT);
    }
    Serial.begin(9600);
    Serial.println("Back and forth pattern");
}

void loop() {
    // Forward: 8, 9, 10
    for (int pin = 8; pin <= 10; pin++) {
        digitalWrite(pin, HIGH);
        Serial.print("Pin ");
        Serial.println(pin);
        delay(150);
        digitalWrite(pin, LOW);
    }

    // Backward: 9 only (skip 10 to avoid double-blink at end,
    // skip 8 because forward loop will hit it next)
    digitalWrite(9, HIGH);
    Serial.println("Pin 9");
    delay(150);
    digitalWrite(9, LOW);
}
```

**Alternative using two for loops:**
```cpp
void loop() {
    // Forward: 8, 9, 10
    for (int pin = 8; pin <= 10; pin++) {
        digitalWrite(pin, HIGH);
        Serial.print("Pin ");
        Serial.println(pin);
        delay(150);
        digitalWrite(pin, LOW);
    }

    // Backward: 9 (only middle pin)
    for (int pin = 9; pin >= 9; pin--) {
        digitalWrite(pin, HIGH);
        Serial.print("Pin ");
        Serial.println(pin);
        delay(150);
        digitalWrite(pin, LOW);
    }
}
```

**Grading notes:** The key thing is avoiding a "double blink" at the endpoints. If pin 8 or pin 10 lights up twice in a row (once at the end of one direction, once at the start of the other), the pattern stutters. The sequence should be: 8, 9, 10, 9, 8, 9, 10, 9, ... Some students might hardcode all four steps, which is fine. Accept any approach that produces the correct visual pattern.

---

### Task 2: LED Counter (3-bit binary 0–7)

```cpp
void setup() {
    pinMode(8, OUTPUT);   // 1s place
    pinMode(9, OUTPUT);   // 2s place
    pinMode(10, OUTPUT);  // 4s place
    Serial.begin(9600);
    Serial.println("3-bit binary counter: 0 to 7");
}

void loop() {
    // 0: 000
    digitalWrite(10, LOW); digitalWrite(9, LOW); digitalWrite(8, LOW);
    Serial.println("0 = OFF OFF OFF");
    delay(1000);

    // 1: 001
    digitalWrite(10, LOW); digitalWrite(9, LOW); digitalWrite(8, HIGH);
    Serial.println("1 = OFF OFF ON");
    delay(1000);

    // 2: 010
    digitalWrite(10, LOW); digitalWrite(9, HIGH); digitalWrite(8, LOW);
    Serial.println("2 = OFF ON OFF");
    delay(1000);

    // 3: 011
    digitalWrite(10, LOW); digitalWrite(9, HIGH); digitalWrite(8, HIGH);
    Serial.println("3 = OFF ON ON");
    delay(1000);

    // 4: 100
    digitalWrite(10, HIGH); digitalWrite(9, LOW); digitalWrite(8, LOW);
    Serial.println("4 = ON OFF OFF");
    delay(1000);

    // 5: 101
    digitalWrite(10, HIGH); digitalWrite(9, LOW); digitalWrite(8, HIGH);
    Serial.println("5 = ON OFF ON");
    delay(1000);

    // 6: 110
    digitalWrite(10, HIGH); digitalWrite(9, HIGH); digitalWrite(8, LOW);
    Serial.println("6 = ON ON OFF");
    delay(1000);

    // 7: 111
    digitalWrite(10, HIGH); digitalWrite(9, HIGH); digitalWrite(8, HIGH);
    Serial.println("7 = ON ON ON");
    delay(1000);

    delay(2000);
}
```

**Grading notes:** Check that all 8 states are correct against the binary table. Common mistakes: getting the pin-to-place-value mapping backwards (pin 8 as 4s instead of 1s), or mixing up a couple of rows. If the student uses bitwise operations or a loop with bit shifting — that's impressive and should get extra credit, but it's not expected at this level.

**Extra credit version (using bitwise operations):**
```cpp
void setup() {
    pinMode(8, OUTPUT);
    pinMode(9, OUTPUT);
    pinMode(10, OUTPUT);
    Serial.begin(9600);
    Serial.println("3-bit binary counter: 0 to 7");
}

void loop() {
    for (int num = 0; num <= 7; num++) {
        digitalWrite(8, (num & 1) ? HIGH : LOW);    // 1s bit
        digitalWrite(9, (num & 2) ? HIGH : LOW);    // 2s bit
        digitalWrite(10, (num & 4) ? HIGH : LOW);   // 4s bit

        Serial.print(num);
        Serial.print(" = ");
        Serial.print((num & 4) ? "ON " : "OFF ");
        Serial.print((num & 2) ? "ON " : "OFF ");
        Serial.println((num & 1) ? "ON" : "OFF");

        delay(1000);
    }
    delay(2000);
}
```

---

### Task 3: Randomized Blink

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
    int pin = random(8, 11);   // Returns 8, 9, or 10

    digitalWrite(pin, HIGH);
    delay(300);
    digitalWrite(pin, LOW);

    Serial.print("Pin ");
    Serial.print(pin);
    Serial.println(" blinked");

    delay(200);
}
```

**Grading notes:** The critical piece is `random(8, 11)` — the upper bound is exclusive, so `random(8, 11)` gives 8, 9, or 10. Common mistake: `random(8, 10)` which only gives 8 or 9 (never 10). Also check that `randomSeed(analogRead(0))` is in `setup()` — without it, the sequence is the same every time the board resets. Some students may store the result in a variable and use it in a switch statement, which is also fine.
