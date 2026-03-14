# Lesson 02: Breadboards, Resistors, and External LEDs
## Study Guide & Reference

**Programming — Medina County Career Center**

---

This guide is your reference for everything in Arduino Lesson 02. Use it while you work through the task files — it has diagrams, explanations, and vocabulary you'll need.

---

## 1. THE BREADBOARD

A **breadboard** is a reusable platform for building electronic circuits without soldering. Components push into the holes and connect through metal strips hidden underneath.

### Connection Layout

```
Power Rails       Component Area                Power Rails
(+) (−)     a  b  c  d  e  ║  f  g  h  i  j    (+) (−)
 │   │      ═══════════════║═══════════════      │   │
 │   │      ●──●──●──●──●  ║  ●──●──●──●──●     │   │    ← Row 1
 │   │      ●──●──●──●──●  ║  ●──●──●──●──●     │   │    ← Row 2
 │   │      ●──●──●──●──●  ║  ●──●──●──●──●     │   │    ← Row 3
 │   │           ...        ║       ...           │   │
 ▼   ▼                      ║                     ▼   ▼
vertical                  TRENCH                 vertical
```

### Connection Rules

| What | Connected? |
|---|---|
| Same row, same side of trench (e.g., a5 and d5) | **Yes** |
| Same row, opposite sides of trench (e.g., e5 and f5) | **No** |
| Different rows, same side (e.g., a5 and a6) | **No** |
| Holes on the same power rail (+) or (−) | **Yes** (whole strip) |

### What goes where

- **Power rail (+)**: Connect to Arduino 5V if you need a shared power source
- **Power rail (−)**: Connect to Arduino GND — this is your **ground bus**
- **Component area**: Where LEDs, resistors, wires, and other parts go

---

## 2. LEDs (LIGHT EMITTING DIODES)

An LED converts electrical current into light. Unlike a regular light bulb, an LED only works in **one direction**.

### Identifying the Legs

| Feature | Positive (Anode) | Negative (Cathode) |
|---|---|---|
| Leg length | **Long** | Short |
| Plastic body | Round side | **Flat edge** |
| Connects to | Arduino pin (signal) | GND (through resistor) |

### What happens if it's backwards?

Nothing bad — it just won't light up. Flip it around and try again.

### LED Colors and Forward Voltage

Different color LEDs need slightly different voltages to turn on:

| Color | Forward Voltage | Brightness with 220Ω |
|---|---|---|
| Red | ~1.8V | Bright |
| Yellow | ~2.0V | Bright |
| Green | ~2.2V | Bright |
| Blue | ~3.0V | Dimmer |
| White | ~3.2V | Dimmer |

You don't need to worry about this much — the resistor handles it. But if a blue or white LED seems dimmer than a red one with the same resistor, this is why.

---

## 3. RESISTORS

A **resistor** limits the flow of electrical current. Without one, an LED will draw too much current and burn out.

### Why we need them

The Arduino outputs 5V on a digital pin. Most LEDs only need about 2V and 20mA of current. The resistor "uses up" the extra voltage and keeps the current at a safe level.

**Formula (for reference, not required):**
```
Resistance = (Supply Voltage - LED Voltage) / Desired Current
           = (5V - 2V) / 0.02A
           = 150Ω minimum
```

We use **220Ω** (safe and bright) or **1KΩ** (safe and dimmer) — both work fine.

### Reading Resistor Bands

| Resistor | Band 1 | Band 2 | Multiplier | Tolerance |
|---|---|---|---|---|
| 220Ω | Red (2) | Red (2) | Brown (×10) | Gold (±5%) |
| 1KΩ | Brown (1) | Black (0) | Red (×100) | Gold (±5%) |
| 10KΩ | Brown (1) | Black (0) | Orange (×1000) | Gold (±5%) |

**Tip:** Resistors have no polarity — they work in either direction.

---

## 4. THE COMPLETE CIRCUIT

Every external LED circuit follows this path:

```
Arduino Pin  →  LED (+ to −)  →  Resistor  →  GND
```

### Schematic View

```
Pin 8 ──────► [LED +]──[LED −] ──► [Resistor] ──► GND rail ──► Arduino GND
              (long leg)  (short leg)
```

### Current Flow

1. Arduino sets pin 8 to HIGH (5V)
2. Current flows out of pin 8
3. Current passes through the LED (lighting it up)
4. Current passes through the resistor (limiting the flow)
5. Current returns to the Arduino through GND

When pin 8 is set to LOW (0V), no current flows and the LED turns off.

---

## 5. WIRING MULTIPLE LEDs

Each LED needs:
- Its own **Arduino pin** (for individual control)
- Its own **resistor** (no sharing!)
- A connection to the **shared GND rail**

### Example: 4 LEDs on pins 8, 9, 10, 11

```
Pin 8  → LED 1 → Resistor → GND rail
Pin 9  → LED 2 → Resistor → GND rail
Pin 10 → LED 3 → Resistor → GND rail
Pin 11 → LED 4 → Resistor → GND rail
Arduino GND → GND rail
```

All four LEDs share one GND rail, connected to the Arduino's GND pin with a single wire.

---

## 6. CODE FOR EXTERNAL LEDs

The code is identical to Lesson 01 — the only difference is the pin number.

### Single External LED

```cpp
void setup() {
    pinMode(8, OUTPUT);     // External LED on pin 8
}

void loop() {
    digitalWrite(8, HIGH);  // LED on
    delay(1000);
    digitalWrite(8, LOW);   // LED off
    delay(1000);
}
```

### Multiple LEDs

```cpp
void setup() {
    pinMode(8, OUTPUT);
    pinMode(9, OUTPUT);
    pinMode(10, OUTPUT);
}

void loop() {
    // Turn on one at a time
    digitalWrite(8, HIGH);
    digitalWrite(9, LOW);
    digitalWrite(10, LOW);
    delay(300);

    digitalWrite(8, LOW);
    digitalWrite(9, HIGH);
    digitalWrite(10, LOW);
    delay(300);

    digitalWrite(8, LOW);
    digitalWrite(9, LOW);
    digitalWrite(10, HIGH);
    delay(300);
}
```

### Using a For Loop with Multiple LEDs

```cpp
void setup() {
    for (int pin = 8; pin <= 11; pin++) {
        pinMode(pin, OUTPUT);
    }
}

void loop() {
    // Light each LED in sequence
    for (int pin = 8; pin <= 11; pin++) {
        digitalWrite(pin, HIGH);
        delay(200);
        digitalWrite(pin, LOW);
    }
}
```

**Why this works:** Pins 8, 9, 10, 11 are consecutive numbers, so a `for` loop can iterate through them. This is much cleaner than writing 4 separate `digitalWrite` calls.

---

## 7. COMMON MISTAKES AND FIXES

**LED doesn't light up:**
- Check polarity — flip the LED around
- Check that the resistor connects to the GND rail
- Check that a wire runs from Arduino GND to the GND rail
- Check that your code uses the correct pin number

**LED is very dim:**
- You might be using a larger resistor than needed (e.g., 10KΩ instead of 220Ω)
- Blue and white LEDs are naturally dimmer than red/yellow/green with the same resistor

**LED stays on all the time:**
- Your code might not have a `delay()` between HIGH and LOW
- Or the LED is connected to the 5V rail instead of a digital pin

**One LED works but another doesn't:**
- Each LED needs its own resistor — make sure none are sharing
- Check that each LED's long leg row has a wire to the correct pin

**Breadboard connections seem random:**
- Remember: rows are connected, columns are not
- The trench breaks the connection — left side and right side are independent

---

## VOCABULARY

**Breadboard** — A reusable plastic board with internal metal connections for building circuits without soldering. Rows of holes are connected horizontally; the trench separates the two halves.

**LED (Light Emitting Diode)** — A component that emits light when current flows through it in the correct direction. Has polarity: long leg is positive (anode), short leg is negative (cathode).

**Resistor** — A component that limits the flow of electrical current. Measured in ohms (Ω). Protects LEDs and other components from receiving too much current.

**Ohm (Ω)** — The unit of electrical resistance. Higher ohms = more resistance = less current flow.

**Current** — The flow of electricity through a circuit, measured in amps (A) or milliamps (mA). LEDs typically need about 10-20mA.

**Voltage** — The electrical "pressure" that pushes current through a circuit, measured in volts (V). Arduino digital pins output 5V when HIGH, 0V when LOW.

**GND (Ground)** — The reference point for 0 volts in a circuit. All current returns to ground. Every circuit needs a connection back to GND to work.

**Anode** — The positive terminal of an LED (long leg). Connects toward the power source (Arduino pin).

**Cathode** — The negative terminal of an LED (short leg / flat edge). Connects toward ground.

**Polarity** — The property that a component has a specific positive and negative direction. LEDs have polarity; resistors do not.

**Short Circuit** — When current bypasses a component by finding an easier path. Usually caused by wires touching that shouldn't. Can damage components.

---

## ODE COMPETENCIES COVERED

**5.1.1** — Describe how computer programs and scripts can be used to solve problems
**5.2.1** — Data types and variables
**5.4.1** — Configure options, preferences, and tools
**5.4.2** — Write and edit code in the IDE
**5.4.3** — Compile or interpret a working program
**5.4.6** — Testing and debugging
**5.4.7** — Error identification
**5.5.5** — Use appropriate naming conventions and apply comments
