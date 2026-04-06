# Arduino Walkthrough: Reading Light Levels with a Photoresistor

**Programming — Medina County Career Center**

---

## What We're Doing

You're going to wire a **photoresistor** (light sensor) to your Arduino and use `analogRead()` to measure light levels. Then you'll build an automatic nightlight that turns an LED on when it gets dark — the same concept used in real nightlights, outdoor lights, and dashboard displays.

This builds directly on what you did with the potentiometer in Lesson 05. The photoresistor is just another component that changes resistance — except instead of you turning a knob, **light** changes the resistance.

**Watch this video first:**
Science Buddies — How to Use a Photoresistor with Arduino
https://www.youtube.com/watch?v=XwJQJnY6iUs
*(Your instructor will play this for the class)*

---

## How the Photoresistor Works

A photoresistor (also called an LDR — Light Dependent Resistor) changes resistance based on light:

- **Bright light** → low resistance (below 1KΩ) → higher voltage at the sensor pin
- **Dark** → high resistance (10KΩ–20KΩ+) → lower voltage at the sensor pin

The Arduino can't measure resistance directly — it measures voltage. So we pair the photoresistor with a fixed resistor to create a **voltage divider** (same concept from the video). The changing resistance of the photoresistor causes the voltage at the middle point to change, and that's what we read with `analogRead()`.

---

## Part 1 — Find Your Components

From your kit, grab:

- **Photoresistor** — small, flat component with a squiggly pattern on the face
- **10KΩ resistor** (brown-black-orange-gold) — this is the fixed resistor in the voltage divider
- **220Ω resistor** (red-red-brown-gold) — this is for the LED
- **1 LED** (any color)
- 4–5 jumper wires
- Breadboard
- Arduino + USB cable

---

## Part 2 — Wire the Voltage Divider + LED

**Disconnect USB first.**

### Circuit Overview

```
5V ──────► [Photoresistor] ──┬──► Arduino A0
                             │
                          [10KΩ resistor]
                             │
GND ─────────────────────────┘

Arduino Pin 8 ──► [220Ω resistor] ──► [LED] ──► GND
```

### Wiring Steps

**Photoresistor + Voltage Divider:**

1. Push one leg of the **photoresistor** into the breadboard. Connect that row to **5V** with a jumper wire.
2. The other leg goes into a different row. Connect that row to **Arduino A0** with a jumper wire.
3. In that same row (the A0 side), push one leg of the **10KΩ resistor**. The other leg goes to the **GND rail**.
4. Connect **Arduino GND** to the GND rail.

**LED (same as Lesson 02):**

5. Push the LED into the breadboard — long leg (positive) and short leg (negative) in two different rows.
6. Connect **Arduino pin 8** to the long leg's row through a **220Ω resistor**.
7. Connect the short leg's row to the **GND rail**.

### Wiring Checklist

- [ ] Photoresistor: one leg to 5V, other leg to A0 row
- [ ] 10KΩ resistor: from the A0 row down to GND rail
- [ ] Arduino GND to GND rail
- [ ] LED: pin 8 → 220Ω resistor → LED long leg → LED short leg → GND rail
- [ ] A0 wire connects to the junction between the photoresistor and the 10KΩ resistor

---

## Part 3 — Read the Sensor

Plug in USB. Open the Arduino IDE. New sketch.

**Type this:**

```cpp
const int led = 8;              // led pin
const int sensor_pin = A0;      // sensor pin
int sensor;                      // sensor reading
const int threshold = 500;       // threshold to turn LED on

void setup() {
    pinMode(led, OUTPUT);        // set LED pin as output
    Serial.begin(9600);         // initialize serial communication
}

void loop() {
    sensor = analogRead(sensor_pin);    // read sensor value
    Serial.println(sensor);             // print sensor value

    delay(200);
}
```

This matches the structure from the video. Upload, open the Serial Monitor (9600 baud), and try:

- Cover the sensor with your hand → numbers drop
- Shine your phone flashlight on it → numbers rise
- Normal room light → somewhere in the middle

**Your range will depend on the room.** Typical indoor readings might be 200–700. Direct flashlight might push toward 900+. Fully covered might drop below 100.

---

## Part 4 — Quick Calibration

Before writing the nightlight code, figure out your sensor's range in this room:

1. Cover the sensor completely with your hand. Write down the value: **Dark = ______**
2. Shine a flashlight directly on it. Write down the value: **Bright = ______**
3. Leave it under normal room light: **Room = ______**

You'll use these values to pick a good threshold for your nightlight.

---

## Part 5 — Automatic Nightlight

Now add the LED control. This is the same behavior from the video — LED turns on when it gets dark, off when it's bright.

```cpp
// automatic "night light"
// turn LED on when light levels drop too low

const int led = 8;              // led pin
const int sensor_pin = A0;      // sensor pin
int sensor;                      // sensor reading
const int threshold = 500;       // threshold to turn LED on

void setup() {
    pinMode(led, OUTPUT);        // set LED pin as output
    Serial.begin(9600);         // initialize serial communication
}

void loop() {
    sensor = analogRead(sensor_pin);    // read sensor value
    Serial.println(sensor);             // print sensor value

    if (sensor < threshold) {           // if sensor reading is less than threshold
        digitalWrite(led, HIGH);        // turn LED on
    }
    else {  // else, if sensor reading is greater than threshold
        digitalWrite(led, LOW);         // turn LED off
    }

    delay(200);
}
```

This is the same code from the video.

### Test It

1. Upload the code
2. Open Serial Monitor
3. Cover the sensor — LED should turn on
4. Uncover it — LED should turn off
5. **Adjust the `threshold` variable** based on your calibration values until it triggers where you want it

**Remember from the video:** You can also experiment with changing the 10KΩ resistor value. A different resistor changes the sensitivity range of the voltage divider. But adjusting the threshold in code is usually easier.

---

## Part 6 — Try analogWrite() for Brightness

Instead of just on/off, make the LED brightness respond to light levels. For this part, **move your LED wire to pin 9** (a PWM pin — marked with `~` on the board). Then use this code:

```cpp
// smooth dimming night light
// LED brightness responds to light level

const int led = 9;              // led pin — MUST be PWM pin (3, 5, 6, 9, 10, or 11)
const int sensor_pin = A0;      // sensor pin
int sensor;                      // sensor reading

void setup() {
    pinMode(led, OUTPUT);
    Serial.begin(9600);
}

void loop() {
    sensor = analogRead(sensor_pin);

    // Map sensor value to LED brightness (inverted — darker = brighter LED)
    int brightness = map(sensor, 0, 1023, 255, 0);
    analogWrite(led, brightness);

    Serial.print("Light: ");
    Serial.print(sensor);
    Serial.print("  Brightness: ");
    Serial.println(brightness);

    delay(200);
}
```

Now the LED smoothly dims and brightens as light levels change — just like a real auto-dimming nightlight.

**Question:** Why is the `map()` range reversed (255, 0) instead of (0, 255)? What would happen if you didn't reverse it?

```
YOUR ANSWER:

```

---

## Completion Checklist

- [ ] Photoresistor + voltage divider circuit wired correctly
- [ ] Serial Monitor shows values changing when you cover/uncover the sensor
- [ ] Calibration values recorded (dark, bright, room)
- [ ] Nightlight works — LED turns on in the dark, off in the light
- [ ] Threshold adjusted for your room's conditions
- [ ] Tried the `analogWrite()` brightness version
- [ ] Question answered

**When everything works, move on to the task file: ard06a**
