# ard04a — Stoplight Challenge: Teacher Solutions

**Programming — Medina County Career Center**

---

## Task 1: Single Stoplight

```cpp
int redPin = 13;
int yellowPin = 12;
int greenPin = 11;

void setup() {
    pinMode(redPin, OUTPUT);
    pinMode(yellowPin, OUTPUT);
    pinMode(greenPin, OUTPUT);
    Serial.begin(9600);
    Serial.println("Stoplight running");
}

void loop() {
    // GREEN - Go
    digitalWrite(greenPin, HIGH);
    digitalWrite(yellowPin, LOW);
    digitalWrite(redPin, LOW);
    Serial.println("GREEN - Go");
    delay(5000);

    // YELLOW - Caution
    digitalWrite(greenPin, LOW);
    digitalWrite(yellowPin, HIGH);
    digitalWrite(redPin, LOW);
    Serial.println("YELLOW - Caution");
    delay(2000);

    // RED - Stop
    digitalWrite(greenPin, LOW);
    digitalWrite(yellowPin, LOW);
    digitalWrite(redPin, HIGH);
    Serial.println("RED - Stop");
    delay(5000);
}
```

**Grading notes:** Straightforward — the main thing to check is the correct sequence (green → yellow → red, not green → red → yellow) and that only one LED is on at a time. Some students might forget to turn off the previous LED, which would leave two on at once.

---

## Task 2: Intersection

```cpp
// Street 1
int red1 = 13;
int yellow1 = 12;
int green1 = 11;

// Street 2
int red2 = 10;
int yellow2 = 9;
int green2 = 8;

void setup() {
    for (int pin = 8; pin <= 13; pin++) {
        pinMode(pin, OUTPUT);
    }
    Serial.begin(9600);
    Serial.println("Intersection running");
}

void setLights(int r1, int y1, int g1, int r2, int y2, int g2) {
    digitalWrite(red1, r1);
    digitalWrite(yellow1, y1);
    digitalWrite(green1, g1);
    digitalWrite(red2, r2);
    digitalWrite(yellow2, y2);
    digitalWrite(green2, g2);
}

void loop() {
    // Phase 1: Street 1 green, Street 2 red
    setLights(LOW, LOW, HIGH, HIGH, LOW, LOW);
    Serial.println("St1: GREEN  |  St2: RED");
    delay(5000);

    // Phase 2: Street 1 yellow, Street 2 red
    setLights(LOW, HIGH, LOW, HIGH, LOW, LOW);
    Serial.println("St1: YELLOW |  St2: RED");
    delay(2000);

    // Phase 3: Both red (safety pause)
    setLights(HIGH, LOW, LOW, HIGH, LOW, LOW);
    Serial.println("St1: RED    |  St2: RED  (clearing)");
    delay(1000);

    // Phase 4: Street 1 red, Street 2 green
    setLights(HIGH, LOW, LOW, LOW, LOW, HIGH);
    Serial.println("St1: RED    |  St2: GREEN");
    delay(5000);

    // Phase 5: Street 1 red, Street 2 yellow
    setLights(HIGH, LOW, LOW, LOW, HIGH, LOW);
    Serial.println("St1: RED    |  St2: YELLOW");
    delay(2000);

    // Phase 6: Both red (safety pause)
    setLights(HIGH, LOW, LOW, HIGH, LOW, LOW);
    Serial.println("St1: RED    |  St2: RED  (clearing)");
    delay(1000);
}
```

**Grading notes:** The critical safety check is that both streets are NEVER green at the same time. Walk through each phase and verify that the `setLights()` arguments match the phase table. Common mistakes: forgetting a phase, skipping the all-red safety pause, or getting the `setLights()` argument order wrong (especially mixing up which street is which). If a student doesn't use the helper function and writes 6 `digitalWrite` calls per phase, that's fine — just harder to read.

---

## Task 3: Additional Features

### Option A: Flashing Red

```cpp
int cycleCount = 0;

void loop() {
    // ... (phases 1-6 from Task 2) ...

    cycleCount++;

    if (cycleCount >= 3) {
        Serial.println("Late night mode - flashing red");
        while (true) {    // Run forever
            setLights(HIGH, LOW, LOW, HIGH, LOW, LOW);
            delay(1000);
            setLights(LOW, LOW, LOW, LOW, LOW, LOW);
            delay(1000);
        }
    }
}
```

**Grading notes:** The `while(true)` loop means it stays in flashing mode permanently (until reset). Some students might use a boolean flag instead, which is also fine. The key behavior: after 3 full cycles, both reds blink in unison, all other LEDs off.

### Option B: Turn Signal

```cpp
int turnPin = 7;

void setup() {
    // ... existing setup ...
    pinMode(turnPin, OUTPUT);
}

// In the phase 3 section, replace the simple delay:
    // Phase 3: Both red + turn signal
    setLights(HIGH, LOW, LOW, HIGH, LOW, LOW);
    Serial.println("St1: RED    |  St2: RED  (left turn)");
    for (int i = 0; i < 3; i++) {
        digitalWrite(turnPin, HIGH);
        delay(200);
        digitalWrite(turnPin, LOW);
        delay(200);
    }
    delay(200);  // brief extra pause after turn blinks
```

**Grading notes:** The turn LED should only blink during the all-red phase, not during any other phase. 3 blinks at 200ms on/off = 1.2 seconds, replacing the original 1-second pause. Accept any reasonable timing.

### Option C: Countdown Timer

```cpp
    // Phase 1: Street 1 green, Street 2 red — with countdown
    setLights(LOW, LOW, HIGH, HIGH, LOW, LOW);
    for (int t = 5; t >= 1; t--) {
        Serial.print("St1: GREEN  |  St2: RED  - ");
        Serial.println(t);
        delay(1000);
    }

    // Phase 2: Street 1 yellow, Street 2 red — with countdown
    setLights(LOW, HIGH, LOW, HIGH, LOW, LOW);
    for (int t = 2; t >= 1; t--) {
        Serial.print("St1: YELLOW |  St2: RED  - ");
        Serial.println(t);
        delay(1000);
    }

    // ... same pattern for phases 3-6 ...
```

**Grading notes:** Each `delay(5000)` becomes a `for` loop running 5 times with `delay(1000)`. Each `delay(2000)` becomes 2 iterations, and `delay(1000)` becomes 1 iteration (or just stays as-is). The countdown should count down (5,4,3,2,1), not up. Accept counting up as well.
