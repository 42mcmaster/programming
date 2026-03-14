# Lesson 06: Light Sensor — Reading and Collecting Real Data

**Programming — Medina County Career Center**

---

## Overview

You're going to swap the potentiometer for a **photoresistor** (light sensor) and use the same `analogRead()` technique to measure light levels. Then you'll collect real data under different lighting conditions and chart it.

This is the same circuit concept as the potentiometer — a component that changes resistance, creating a variable voltage the Arduino can read. The difference is that instead of you turning a knob, **light** changes the resistance.

---

## What You Need

From your kit:
- **Photoresistor** (also called LDR — Light Dependent Resistor). Small, flat component with a squiggly pattern on top.
- **10KΩ resistor** (brown-black-orange-gold)
- 3 jumper wires
- Breadboard
- Arduino + USB cable

---

## How the Photoresistor Works

A photoresistor changes resistance based on how much light hits it:
- **Bright light** → low resistance (~1KΩ) → higher voltage at the sensor pin
- **Dark** → high resistance (~100KΩ+) → lower voltage at the sensor pin

By itself, the photoresistor just changes resistance. To turn that into a voltage the Arduino can read, we pair it with a fixed resistor to make a **voltage divider**.

---

## The Circuit

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

- [ ] Photoresistor: one leg to 5V, other leg to A0
- [ ] 10KΩ resistor: from the A0 row down to GND rail
- [ ] Arduino GND to GND rail
- [ ] A0 wire connects to the junction between the photoresistor and the 10KΩ resistor

---

## The Code

This is almost identical to the potentiometer code. The only thing that changes is what's plugged into A0.

```cpp
int sensorPin = A0;    // Analog pin for the photoresistor
int lightVal;          // Variable to store the reading
int br = 9600;         // Baud rate
int wt = 200;          // Wait time in ms

void setup() {
    pinMode(sensorPin, INPUT);
    Serial.begin(br);
    Serial.println("Light sensor ready");
}

void loop() {
    lightVal = analogRead(sensorPin);

    Serial.print("Light: ");
    Serial.println(lightVal);

    delay(wt);
}
```

Upload, open the Serial Monitor, and try:
- Cover the sensor with your hand → numbers drop
- Shine your phone flashlight on it → numbers rise
- Normal room light → somewhere in the middle

**Your range will depend on the room.** Typical indoor readings might be 300–700. Direct flashlight might push toward 900+. Fully covered might drop to 50–150.

---

## Quick Calibration

Before collecting data, figure out your sensor's range in this room:

1. Cover the sensor completely with your hand. Write down the value: **Dark = ______**
2. Shine a flashlight directly on it. Write down the value: **Bright = ______**
3. Leave it under normal room light: **Room = ______**

You'll use these to interpret your data later.

---

## Data Collection Activity

### Setup

Update your code to log data every second in CSV format:

```cpp
int sensorPin = A0;    // Analog pin for the photoresistor
int lightVal;          // Variable to store the reading
int br = 9600;         // Baud rate
int wt = 1000;         // Wait time — 1 second between readings
int seconds = 0;       // Time counter

void setup() {
    pinMode(sensorPin, INPUT);
    Serial.begin(br);
    Serial.println("Time(s), Light");
}

void loop() {
    seconds++;
    lightVal = analogRead(sensorPin);

    Serial.print(seconds);
    Serial.print(", ");
    Serial.println(lightVal);

    delay(wt);
}
```

### The Experiment

You're going to collect 30 seconds of light data while changing conditions. Here's the plan:

| Time | What to do |
|---|---|
| 0–10 sec | Leave the sensor in normal room light (don't touch it) |
| 10–15 sec | Cover the sensor with your hand |
| 15–20 sec | Remove your hand (back to room light) |
| 20–25 sec | Shine your phone flashlight on the sensor |
| 25–30 sec | Remove the flashlight (back to room light) |

### Collecting the Data

1. Upload the code
2. Open the Serial Monitor
3. **Clear the Serial Monitor** (click the clear button or close/reopen it)
4. Follow the timing plan above
5. After 30 seconds, **select all the text** in the Serial Monitor (Ctrl+A) and **copy** it (Ctrl+C)
6. Open Google Sheets or Excel
7. Paste the data (Ctrl+V)
8. If it pastes into one column, use **Data → Split text to columns** (Google Sheets) or **Text to Columns** (Excel) with comma as the delimiter

### Make the Chart

1. Select both columns of data (Time and Light)
2. Insert → Chart (Google Sheets) or Insert → Chart (Excel)
3. Choose **Line chart**
4. Add a title: "Light Sensor Readings Over Time"
5. Label axes: X = "Time (seconds)", Y = "Light Level (0–1023)"

### What Your Chart Should Show

You should see 5 distinct sections:
1. **Flat line** — normal room light (baseline)
2. **Drop** — hand covering the sensor
3. **Return to baseline** — hand removed
4. **Spike** — flashlight on
5. **Return to baseline** — flashlight removed

If your chart doesn't show clear changes, the sensor might not be wired correctly, or the room might be too bright/dark for the changes to register.

---

## Questions

Answer these after completing the data collection:

**1.** What was the approximate reading for normal room light? What about covered and flashlight?

```
YOUR ANSWER:

```

**2.** Did the sensor respond instantly when you covered it or shined the light, or was there a delay? Why might that be?

```
YOUR ANSWER:

```

**3.** Look at the "normal room light" sections. Are the readings perfectly steady or do they fluctuate a little? Why?

```
YOUR ANSWER:

```

---

## Submission Checklist

- [ ] Photoresistor circuit working — Serial Monitor shows values changing with light
- [ ] Calibration values recorded (dark, bright, room)
- [ ] 30 seconds of data collected following the timing plan
- [ ] Data pasted into a spreadsheet
- [ ] Line chart created showing the 5 sections
- [ ] 3 questions answered

**Show your chart and circuit to your instructor. You're done!**
