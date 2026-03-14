# Arduino Walkthrough: Reading Analog Voltages with a Potentiometer

**Programming — Medina County Career Center**

---

## What We're Doing

You're going to wire a potentiometer to your Arduino and use `analogRead()` to read its position. You'll see the values stream to the Serial Monitor in real time as you turn the knob. This is the foundation for reading any analog sensor.

**Watch Paul McWhorter's Lesson 12 first (or follow along):**
https://www.youtube.com/watch?v=ORMlmJECabQ

---

## Part 1 — Find the Potentiometer

Open your kit and find the **potentiometer**. It's a small component with:
- A **knob** you can turn
- **3 pins** sticking out the bottom

Also grab 3 jumper wires (red, a signal color, and black is a good convention).

---

## Part 2 — Wire the Circuit

**Disconnect USB first.**

### Pin Connections

| Potentiometer Pin | Connects To |
|---|---|
| Left pin | **5V** on Arduino |
| Middle pin (wiper) | **A0** on Arduino |
| Right pin | **GND** on Arduino |

### Steps

1. Push the potentiometer into the breadboard — the 3 pins should each be in a different row
2. Jumper wire from the **left pin's row** to **Arduino 5V**
3. Jumper wire from the **middle pin's row** to **Arduino A0**
4. Jumper wire from the **right pin's row** to **Arduino GND**

That's it — three wires, no resistor needed.

### Wiring Checklist

- [ ] Potentiometer seated in breadboard, 3 pins in 3 separate rows
- [ ] Left pin → 5V
- [ ] Middle pin → A0
- [ ] Right pin → GND

---

## Part 3 — Write the Code

Plug in USB. Open the Arduino IDE. New sketch.

**Type this:**

```cpp
int potPin = A0;     // Analog pin the potentiometer is connected to
int potVal;          // Variable to store the reading
int br = 9600;       // Baud rate for Serial Monitor
int wt = 100;        // Wait time (delay) in milliseconds

void setup() {
    pinMode(potPin, INPUT);    // Set the analog pin as input
    Serial.begin(br);         // Start Serial Monitor at baud rate
    Serial.println("Potentiometer reader ready");
}

void loop() {
    potVal = analogRead(potPin);    // Read the voltage (0-1023)

    Serial.print("Value: ");
    Serial.println(potVal);

    delay(wt);    // Small delay so the Serial Monitor isn't overwhelmed
}
```

**Paul's coding style:** Notice that every number gets its own variable at the top — `br` for baud rate, `wt` for wait time. This way, if you want to change a value, you change it in one place at the top instead of hunting through your code. Paul calls this "no magic numbers."

### Upload and Test

1. Upload the code
2. Open **Serial Monitor** (Tools → Serial Monitor, or the magnifying glass icon)
3. Make sure baud rate is set to **9600**
4. Turn the potentiometer knob slowly

You should see numbers changing between **0** (knob all the way one direction) and **1023** (all the way the other direction).

If the numbers go the "wrong" direction (1023 on the left), just swap the 5V and GND wires. It doesn't matter — either orientation works.

---

## Part 4 — Add Voltage Calculation

Now let's calculate the actual voltage. Update your `loop()`:

```cpp
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

**Important:** Use `1023.0` (with the decimal) not `1023`. In Arduino (and C), dividing two integers gives an integer — so `potValue / 1023` would always be 0. Using `1023.0` forces floating-point division.

Upload. Turn the knob. You should see voltage values from 0.00V to 5.00V.

---

## Part 5 — Experiment

Try these quick modifications:

**Faster reading (remove the delay):**
What happens if you set `delay(10)` or remove the delay entirely? The Serial Monitor scrolls very fast — the Arduino can read thousands of times per second.

**Print only when the value changes significantly:**
```cpp
int lastVal = 0;

void loop() {
    potVal = analogRead(potPin);

    if (abs(potVal - lastVal) > 5) {    // Only print if changed by more than 5
        Serial.print("Value: ");
        Serial.println(potVal);
        lastVal = potVal;
    }

    delay(wt);
}
```

This is a common technique for reducing noise in sensor readings.

---

## Completion Checklist

- [ ] Potentiometer wired to 5V, A0, and GND
- [ ] Raw values (0–1023) display in Serial Monitor
- [ ] Turning the knob changes the values smoothly
- [ ] Voltage calculation shows 0.00V to 5.00V
- [ ] Can explain: why we use `1023.0` instead of `1023` in the division

**When everything works, move on to the task file.**
