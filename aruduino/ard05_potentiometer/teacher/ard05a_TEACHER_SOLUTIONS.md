# ard05a — Dimmable LED: Teacher Solutions

**Programming — Medina County Career Center**

---

## Walkthrough Question

**Q: What raw value do you see at halfway? Is it exactly 512? Why might it be slightly off?**

Typically reads close to 512 but rarely exact. The potentiometer isn't perfectly precise — mechanical tolerances, the ADC's own small inaccuracies, and electrical noise all contribute. Readings might fluctuate by 1–3 even when the knob isn't moving. This is normal for analog electronics.

---

## Main Task: Dimmable LED

```cpp
int potPin = A0;     // Potentiometer analog pin
int potVal;          // Reading from the pot
int ledPin = 9;      // LED pin (PWM)
int br = 9600;       // Baud rate
int wt = 100;        // Wait time in ms

void setup() {
    pinMode(potPin, INPUT);
    pinMode(ledPin, OUTPUT);
    Serial.begin(br);
}

void loop() {
    potVal = analogRead(potPin);

    int brightness = map(potVal, 0, 1023, 0, 255);

    analogWrite(ledPin, brightness);

    Serial.print(potVal);
    Serial.print("  ->  Brightness: ");
    Serial.println(brightness);

    delay(wt);
}
```

**Grading notes:**

- The LED **must** be on a PWM pin (3, 5, 6, 9, 10, or 11). If a student wires it to pin 8 or 13, `analogWrite()` won't work — the LED will just be off or full on. This is the most common mistake.
- `map(potVal, 0, 1023, 0, 255)` is the key line. Some students might try `potVal / 4` which is close (gives 0–255) but slightly off at the top end (1023/4 = 255.75, truncated to 255, so it works). Accept either approach.
- The LED should dim smoothly. If it flickers, check that `analogWrite()` is being used (not `digitalWrite()`).
- Serial output format doesn't matter as long as it shows both the raw pot value and the mapped brightness.
- Check that variables are declared at the top (Paul's style). Students shouldn't have `9600` or `100` as raw numbers in `setup()` or `loop()`.

---

## Challenge A: Color Mixer

Not providing a full solution since this depends on their RGB LED wiring, but the core idea:

```cpp
int redPin = 9;
int greenPin = 10;
int bluePin = 11;
// Read potVal, map different ranges to each color
// Or use 3 potentiometers on A0, A1, A2
```

---

## Challenge B: Blink Speed Controller

```cpp
int potPin = A0;
int potVal;
int ledPin = 9;
int br = 9600;

void setup() {
    pinMode(potPin, INPUT);
    pinMode(ledPin, OUTPUT);
    Serial.begin(br);
}

void loop() {
    potVal = analogRead(potPin);
    int blinkDelay = map(potVal, 0, 1023, 1000, 50);

    Serial.print("Blink delay: ");
    Serial.print(blinkDelay);
    Serial.println("ms");

    digitalWrite(ledPin, HIGH);
    delay(blinkDelay);
    digitalWrite(ledPin, LOW);
    delay(blinkDelay);
}
```

**Grading notes:** Uses `digitalWrite()` (not `analogWrite()`) since it's a blink, not a dim. The pot is re-read every blink cycle, so turning the knob changes speed in real time. Note the blink delay changes the effective loop speed, so Serial output is slower when the blink is slow.

---

## Challenge C: Brightness Bar

```cpp
void loop() {
    potVal = analogRead(potPin);
    int brightness = map(potVal, 0, 1023, 0, 255);
    analogWrite(ledPin, brightness);

    int barLength = map(brightness, 0, 255, 0, 16);

    Serial.print("[");
    for (int i = 0; i < 16; i++) {
        if (i < barLength) {
            Serial.print("#");
        } else {
            Serial.print(".");
        }
    }
    Serial.print("] ");
    Serial.print(brightness);
    Serial.println("/255");

    delay(wt);
}
```

**Grading notes:** Accept any reasonable visual representation. The `for` loop printing `#` and `.` is the trickiest part. Some students might hardcode brightness levels with if/else instead of using a loop — that's fine for partial credit.
