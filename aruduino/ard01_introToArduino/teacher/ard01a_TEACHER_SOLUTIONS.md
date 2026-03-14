# ard01a — Blink Variations: Teacher Solutions

**Programming — Medina County Career Center**

---

## Walkthrough Answers

### Walkthrough 1: Basic Blink

**Q: How many times does the LED blink in 10 seconds?**

5 times. Each full cycle is 2 seconds (1000ms on + 1000ms off), so in 10 seconds you get 10 ÷ 2 = 5 complete blinks.

---

### Walkthrough 2: Fast Blink

**Q: How does 100ms compare to 1000ms? Can you still see individual blinks?**

100ms is 1/10 of 1000ms — ten times faster. Yes, you can still see individual blinks at 100ms, though they're much quicker. The LED appears to flicker rapidly. At around 30-50ms, most people start having trouble distinguishing individual blinks.

---

### Walkthrough 3: Heartbeat Pattern

**Q: Describe the pattern you see. How is it different from a simple on/off blink?**

Two quick flashes close together, then a longer pause before repeating — like a heartbeat (lub-dub... lub-dub...). A simple blink is just one flash with even on/off timing. The heartbeat has an asymmetric rhythm created by combining multiple `digitalWrite`/`delay` calls with different pause lengths.

---

## Task Solutions

### Task 1: Slow and Steady

```cpp
void setup() {
    pinMode(13, OUTPUT);
    Serial.begin(9600);
}

void loop() {
    digitalWrite(13, HIGH);
    Serial.println("ON");
    delay(3000);

    digitalWrite(13, LOW);
    Serial.println("OFF");
    delay(1000);
}
```

**Grading notes:** The key things to check — `delay(3000)` for 3 seconds on, `delay(1000)` for 1 second off, and `Serial.println()` printing "ON" and "OFF" at the right times. Order matters: turn on, print, delay, turn off, print, delay.

---

### Task 2: Five Blinks Then Pause

```cpp
void setup() {
    pinMode(13, OUTPUT);
    Serial.begin(9600);
}

void loop() {
    for (int i = 1; i <= 5; i++) {
        Serial.print("Blink ");
        Serial.println(i);
        digitalWrite(13, HIGH);
        delay(200);
        digitalWrite(13, LOW);
        delay(200);
    }

    Serial.println("Pausing...");
    delay(2000);
}
```

**Grading notes:** The `for` loop must run exactly 5 times. Common mistakes: using `i < 5` instead of `i <= 5` (gives 4 blinks), or putting the pause inside the loop instead of after it. The print can come before or after the blink — both are acceptable.

---

### Task 3: Variable Speed Blink

```cpp
int delayTime = 1000;

void setup() {
    pinMode(13, OUTPUT);
    Serial.begin(9600);
}

void loop() {
    Serial.print("Delay: ");
    Serial.println(delayTime);

    digitalWrite(13, HIGH);
    delay(delayTime);
    digitalWrite(13, LOW);
    delay(delayTime);

    delayTime = delayTime - 100;

    if (delayTime < 100) {
        delayTime = 1000;
    }
}
```

**Grading notes:** The variable must be declared **outside** of `loop()` (global scope) so it persists between iterations. Common mistake: declaring `int delayTime = 1000;` inside `loop()` — this resets it every time. The reset condition can be `< 100`, `<= 0`, `== 0`, or similar — as long as it eventually resets. Some students may use `delayTime -= 100;` which is also correct.

---

### Task 4: Blink Counter with Total

```cpp
int blinkCount = 0;

void setup() {
    pinMode(13, OUTPUT);
    Serial.begin(9600);
    Serial.println("Blink counter started!");
}

void loop() {
    blinkCount++;

    digitalWrite(13, HIGH);
    delay(500);
    digitalWrite(13, LOW);
    delay(500);

    Serial.print("Blink #");
    Serial.print(blinkCount);
    Serial.print(" - Total time: ");
    Serial.print(blinkCount);
    Serial.println("s");
}
```

**Grading notes:** `blinkCount` must be global (outside `loop()`). The increment can happen at the start or end of the loop — if at the end, the first printed count would be 0 instead of 1, so incrementing first is better. The time calculation works because each cycle is exactly 1 second (500 + 500 = 1000ms). Some students may use `millis()` for actual elapsed time — that's more accurate and should get extra credit. Accept any reasonable formatting of the output string.

**Alternative using millis() (extra credit):**
```cpp
int blinkCount = 0;

void setup() {
    pinMode(13, OUTPUT);
    Serial.begin(9600);
    Serial.println("Blink counter started!");
}

void loop() {
    blinkCount++;

    digitalWrite(13, HIGH);
    delay(500);
    digitalWrite(13, LOW);
    delay(500);

    Serial.print("Blink #");
    Serial.print(blinkCount);
    Serial.print(" - Total time: ");
    Serial.print(millis() / 1000);
    Serial.println("s");
}
```
