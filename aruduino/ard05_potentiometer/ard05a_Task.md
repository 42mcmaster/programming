# ard05a — Dimmable LED

**Programming — Medina County Career Center**
**Standards: ODE 5.1.1, 5.2.1, 5.2.3, 5.4.2, 5.4.6**

---

## Before You Start

You should have your potentiometer wired and the basic reading code working from the walkthrough. Keep the Serial Monitor open.

**Remember Paul's style:** Declare all your variables at the top. No magic numbers in the code.

---

## Walkthrough: Verify Your Potentiometer

If you haven't already, get this working from the walkthrough:

```cpp
int potPin = A0;    // Analog pin for potentiometer
int potVal;         // Reading from the pot
int br = 9600;      // Baud rate
int wt = 200;       // Wait time in ms

void setup() {
    pinMode(potPin, INPUT);
    Serial.begin(br);
}

void loop() {
    potVal = analogRead(potPin);
    float voltage = (potVal / 1023.0) * 5.0;

    Serial.print("Raw: ");
    Serial.print(potVal);
    Serial.print("   Voltage: ");
    Serial.print(voltage);
    Serial.println("V");

    delay(wt);
}
```

Turn the knob. You should see values from 0 to 1023 in the Serial Monitor.

**Question:** What raw value do you see when the knob is at the halfway point? Is it exactly 512? Why might it be slightly off?

```
YOUR ANSWER:

```

---

## Your Task: Potentiometer-Controlled Dimmable LED

This is Paul's homework from Lesson 12. You're going to use the potentiometer to control the brightness of an LED — when the knob is all the way to the left, the LED is off. As you turn it to the right, the LED gets brighter and brighter until it's fully on.

### What You Need to Know

**`analogWrite()`** lets you set a pin to a value between 0 and 255 (not just HIGH/LOW):
- `analogWrite(pin, 0)` → LED fully off
- `analogWrite(pin, 127)` → LED about half brightness
- `analogWrite(pin, 255)` → LED fully on

**Important:** `analogWrite()` only works on **PWM pins** — these are marked with a `~` on the board. Pins **3, 5, 6, 9, 10, 11** support `analogWrite()`. Pins like 8, 12, 13 do **not**.

**The problem:** `analogRead()` gives you 0–1023, but `analogWrite()` needs 0–255. You need to convert one range to the other. The `map()` function does this:

```cpp
int brightness = map(potVal, 0, 1023, 0, 255);
// potVal 0    → brightness 0   (off)
// potVal 512  → brightness 127 (half)
// potVal 1023 → brightness 255 (full)
```

### Wire It Up

Keep your potentiometer wired (5V, A0, GND). Add one LED:

- LED on **pin 9** (this is a PWM pin — it has the `~` mark)
- Same wiring as Lesson 02: pin 9 → LED long leg → LED short leg → resistor → GND rail

### Your Starter Code

```cpp
int potPin = A0;     // Potentiometer analog pin
int potVal;          // Reading from the pot
int ledPin = 9;      // LED pin (must be a PWM pin: 3, 5, 6, 9, 10, or 11)
int br = 9600;       // Baud rate
int wt = 100;        // Wait time in ms

void setup() {
    pinMode(potPin, INPUT);
    pinMode(ledPin, OUTPUT);
    Serial.begin(br);
}

void loop() {
    potVal = analogRead(potPin);

    // Convert potVal (0-1023) to brightness (0-255) using map()

    // Write the brightness to the LED using analogWrite()

    // Print the potVal and brightness to the Serial Monitor

    delay(wt);
}
```

### What to Do

1. Use `map()` to convert `potVal` (0–1023) into a brightness value (0–255)
2. Use `analogWrite(ledPin, brightness)` to set the LED brightness
3. Print both `potVal` and `brightness` to the Serial Monitor so you can see them change
4. Upload and test — turn the knob slowly and watch the LED dim and brighten

### Expected Serial Monitor Output

```
0    ->  Brightness: 0
128  ->  Brightness: 32
512  ->  Brightness: 127
1023 ->  Brightness: 255
```

(Your formatting can be different — just show both values.)

### Expected LED Behavior

- Knob all the way left: LED is completely off
- Knob in the middle: LED is at about half brightness
- Knob all the way right: LED is fully bright
- Turning the knob smoothly changes brightness with no flickering

---

## Optional Challenge (if you finish early)

Pick **one** of these:

### Challenge A: Color Mixer (if you have an RGB LED)

If your kit has an **RGB LED** (one LED with 4 legs — red, green, blue, and ground), wire it up and use 3 potentiometers (or one potentiometer read 3 times with different mappings) to mix colors. Use `analogWrite()` on 3 different PWM pins for red, green, and blue.

### Challenge B: Blink Speed Controller

Use the potentiometer to control how fast the LED blinks instead of how bright it glows. Knob left = slow blink (1 second), knob right = fast blink (50ms).

```cpp
int blinkDelay = map(potVal, 0, 1023, 1000, 50);
```

Use `blinkDelay` in your `digitalWrite()`/`delay()` blink pattern instead of `analogWrite()`.

### Challenge C: Brightness with Serial Readout Bar

Make a visual "progress bar" in the Serial Monitor that shows the brightness level:

```
[#####...........] 127/255
[###############.] 240/255
[................] 0/255
```

Use a `for` loop to print `#` characters proportional to the brightness (out of 16 characters wide).

---

## Submission Checklist

- [ ] Walkthrough question answered
- [ ] Potentiometer controls LED brightness smoothly from off to full
- [ ] LED is on a PWM pin (3, 5, 6, 9, 10, or 11)
- [ ] Serial Monitor shows potVal and brightness values
- [ ] Code uses Paul's style — all variables declared at the top, no magic numbers
- [ ] (Optional) One challenge completed
