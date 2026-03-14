---
marp: true
theme: default
class: invert
paginate: true
---

# Lesson 05: Reading Analog Voltages — The Potentiometer
## Programming
### Medina County Career Center
**Based on Paul McWhorter's Arduino Lesson 12**

---

## Watch the Video

**Paul McWhorter's Lesson 12** — Reading Analog Voltages:
https://www.youtube.com/watch?v=ORMlmJECabQ

Paul explains how to wire a potentiometer and use `analogRead()` to read voltages into your Arduino. These slides reinforce the key concepts.

---

## Digital vs. Analog — The Big Idea

So far, everything has been **digital** — on or off, HIGH or LOW, 1 or 0.

But the real world isn't just on and off. Temperature, light, sound, and position are all **analog** — they have a range of values.

- **Digital**: a light switch (on or off)
- **Analog**: a dimmer knob (anywhere from off to fully bright)

Today you learn to **read** analog values into the Arduino.

---

## What Is a Potentiometer?

A **potentiometer** (pot for short) is a variable resistor with a knob you can turn.

- 3 pins: **5V**, **Signal (wiper)**, **GND**
- Turning the knob changes the voltage on the middle pin
- All the way left → 0V
- All the way right → 5V
- Middle → about 2.5V

It's the simplest way to create a variable voltage for the Arduino to read.

---

## analogRead() — Reading a Voltage

```cpp
int value = analogRead(A0);   // Read voltage on analog pin A0
```

The Arduino has **6 analog input pins**: A0 through A5.

`analogRead()` converts the voltage (0V to 5V) into a number:

| Voltage | analogRead value |
|---|---|
| 0V | 0 |
| 1.25V | 256 |
| 2.5V | 512 |
| 3.75V | 768 |
| 5V | 1023 |

**10-bit resolution** → 2^10 = **1024 possible values** (0 to 1023)

---

## The Circuit

```
5V ───────────────► Potentiometer pin 1 (left)
                    Potentiometer pin 2 (middle/wiper) ──► Arduino A0
GND ──────────────► Potentiometer pin 3 (right)
```

The middle pin (wiper) goes to an **analog pin** (A0), not a digital pin.

As you turn the knob, the wiper moves between 5V and GND, producing a voltage anywhere in between.

---

## The Code

```cpp
int potPin = A0;    // Pin the potentiometer is on
int potVal;         // Variable to store the reading
int br = 9600;      // Baud rate for Serial Monitor
int wt = 100;       // Wait time in milliseconds

void setup() {
    pinMode(potPin, INPUT);   // Set analog pin as input
    Serial.begin(br);        // Start Serial Monitor
}

void loop() {
    potVal = analogRead(potPin);   // Read the voltage (0-1023)
    Serial.println(potVal);
    delay(wt);
}
```

Open the **Serial Monitor** and turn the knob. You'll see numbers from 0 to 1023 changing in real time.

**Paul's style:** Every number gets a variable at the top — no "magic numbers" buried in your code. Want to change the delay? Change `wt` once at the top.

---

## What the Numbers Mean

The `analogRead()` value maps directly to voltage:

```
Voltage = (analogRead value / 1023.0) × 5.0
```

| analogRead | Voltage | Knob position |
|---|---|---|
| 0 | 0.0V | All the way left |
| 341 | 1.67V | About 1/3 |
| 512 | 2.50V | Middle |
| 682 | 3.33V | About 2/3 |
| 1023 | 5.0V | All the way right |

You can print both the raw value and the calculated voltage:

```cpp
float voltage = (potVal / 1023.0) * 5.0;
Serial.print("Value: "); Serial.print(potVal);
Serial.print("  Voltage: "); Serial.println(voltage);
```

---

## Why This Matters

`analogRead()` is how you read **any analog sensor**:

- Potentiometer → position/rotation
- Photoresistor → light level
- Temperature sensor → temperature
- Moisture sensor → soil wetness
- Flex sensor → bending

They all work the same way: the sensor creates a variable voltage, and `analogRead()` turns it into a number 0–1023.

**Next lesson:** We'll swap the potentiometer for a photoresistor and collect real light data.

---

## Key Takeaways

- **Analog** values have a range (0 to 5V), unlike digital (just 0V or 5V)
- `analogRead(pin)` converts voltage to a number from 0 to 1023
- The **potentiometer** is a variable resistor with 3 pins: 5V, signal, GND
- Analog pins are A0–A5, and don't need `pinMode()` setup
- The Serial Monitor lets you see the values change in real time
- This same technique works for all analog sensors
