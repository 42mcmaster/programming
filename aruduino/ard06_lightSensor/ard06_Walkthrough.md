# Arduino Walkthrough: Reading Light Levels with a Photoresistor

**Programming — Medina County Career Center**

---

## What We're Doing

You're going to wire a **photoresistor** (light sensor) to your Arduino and use `analogRead()` to measure light levels. This builds directly on what you did with the potentiometer in Lesson 05 — the photoresistor is just another component that changes resistance. The difference is that instead of you turning a knob, **light** changes the resistance.

**Watch this video first:**
Science Buddies — How to Use a Photoresistor with Arduino
https://www.youtube.com/watch?v=XwJQJnY6iUs
*(Your instructor will play this for the class)*

---

## Part 1 — Find Your Components

From your kit, grab:

- **Photoresistor** — small, flat component with a squiggly pattern on the face
- **10KΩ resistor** (brown-black-orange-gold) — this is the fixed resistor in the voltage divider
- 3 jumper wires
- Breadboard
- Arduino + USB cable

---

## Part 2 — Wire the Voltage Divider

**Disconnect USB first.**

A photoresistor changes resistance based on light, but the Arduino can't measure resistance directly — it measures voltage. So we pair the photoresistor with a fixed resistor to create a **voltage divider** (same concept from the video). The changing resistance of the photoresistor causes the voltage at the middle point to change, and that's what we read with `analogRead()`.

### Circuit Overview

```
5V ──────► [Photoresistor] ──┬──► Arduino A0
                             │
                          [10KΩ resistor]
                             │
GND ─────────────────────────┘
```

### Wiring Steps

1. Push one leg of the **photoresistor** into the breadboard. Connect that row to **5V** with a jumper wire.
2. The other leg goes into a different row. Connect that row to **Arduino A0** with a jumper wire.
3. In that same row (the A0 side), push one leg of the **10KΩ resistor**. The other leg goes to the **GND rail**.
4. Connect **Arduino GND** to the GND rail.

### Wiring Checklist

- [ ] Photoresistor: one leg to 5V, other leg to A0 row
- [ ] 10KΩ resistor: from the A0 row down to GND rail
- [ ] Arduino GND to GND rail
- [ ] A0 wire connects to the junction between the photoresistor and the 10KΩ resistor

---

## Part 3 — Read the Sensor

Plug in USB. Open the Arduino IDE. New sketch.

**Type this:**

```cpp
const int sensor_pin = A0;      // sensor pin
int sensor;                      // sensor reading

void setup() {
    pinMode(sensor_pin, INPUT);  // set sensor pin as input
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

Before moving on to the task, figure out your sensor's range in this room:

1. Cover the sensor completely with your hand. Write down the value: **Dark = ______**
2. Shine a flashlight directly on it. Write down the value: **Bright = ______**
3. Leave it under normal room light: **Room = ______**

You'll use these values to pick a good threshold in the task.

---

## Completion Checklist

- [ ] Photoresistor + voltage divider circuit wired correctly
- [ ] Serial Monitor shows values changing when you cover/uncover the sensor
- [ ] Calibration values recorded (dark, bright, room)
- [ ] Can explain: what a voltage divider does and why we need one for the photoresistor

**When everything works, move on to the task file: ard06a**
