---
marp: true
theme: default
class: invert
paginate: true
---

# Lesson 02: Breadboards, Resistors, and External LEDs
## Programming
### Medina County Career Center
**Guest Instructor: Matt Schmidt**

---

## Recap: What We Did Last Time

- Installed the Arduino IDE and connected the board
- Learned about `setup()` and `loop()`
- Used `pinMode()`, `digitalWrite()`, and `delay()`
- Blinked the **built-in LED** on pin 13 — no wiring needed

Today we move beyond the board and into **real circuits**.

---

## Why External Components?

The built-in LED on pin 13 is great for learning, but real projects need:

- Multiple LEDs (status indicators, displays)
- Different colors and brightness levels
- Components placed away from the Arduino board
- Sensors, motors, and other parts that connect through wires

To do any of this, you need a way to connect components — that's the **breadboard**.

---

## The Breadboard

A breadboard lets you build circuits **without soldering**. Components push into the holes and connect through metal strips hidden underneath.

**How it's organized:**

- **Rows (a–e and f–j)**: Holes in the same row are connected horizontally
- **The trench** down the middle: Separates left side from right side — they are NOT connected across the trench
- **Power rails** (+ and −): The long strips on the edges run vertically — used for power (5V) and ground (GND)

---

## Breadboard Connection Rules

```
       Power Rails          Component Area          Power Rails
      (+)    (-)     a  b  c  d  e | f  g  h  i  j    (+)    (-)
       |      |      ─────────────|─────────────      |      |
       |      |      ● ● ● ● ● | ● ● ● ● ●          |      |
       |      |      ● ● ● ● ● | ● ● ● ● ●          |      |
       |      |      ● ● ● ● ● | ● ● ● ● ●          |      |
       ▼      ▼      (connected) | (connected)         ▼      ▼
    vertical  vertical  horizontally  horizontally    vertical  vertical
```

**Key rules:**
- Same row, same side of trench = **connected**
- Across the trench = **NOT connected**
- Power rails run the full length of the board

---

## LEDs: Light Emitting Diodes

An LED only works in **one direction** — polarity matters!

- **Long leg** = positive (anode) — connects toward the Arduino pin
- **Short leg** = negative (cathode) — connects toward GND
- **Flat edge** on the plastic body is also on the cathode (negative) side

If you put an LED in backwards, it just won't light up. It won't break — it just won't work.

---

## Why Do We Need a Resistor?

An LED will try to pull as much current as it can. Without a resistor:

- Too much current flows through the LED
- The LED burns out (sometimes immediately)
- You could also damage the Arduino pin

A **resistor limits the current** to a safe level.

**We use 220Ω or 1KΩ resistors** — either works fine for standard LEDs.

---

## Resistor Color Bands

Resistors are marked with colored bands that tell you their value:

| Resistor | Band 1 | Band 2 | Band 3 (multiplier) | Band 4 (tolerance) |
|---|---|---|---|---|
| **220Ω** | Red (2) | Red (2) | Brown (×10) | Gold (±5%) |
| **1KΩ** | Brown (1) | Black (0) | Red (×100) | Gold (±5%) |

You don't need to memorize the colors — just know which resistors are in your kit and what they look like.

**Tip:** Resistors work in either direction. Unlike LEDs, they have no polarity.

---

## The Circuit: Arduino Pin → LED → Resistor → GND

Every external LED circuit follows this path:

```
Arduino Pin  →  LED (long leg to short leg)  →  Resistor  →  GND
```

The current flows from the Arduino pin, through the LED (lighting it up), through the resistor (limiting the current), and back to ground.

**Important:** The resistor can go on either side of the LED — before or after. We put it after the LED for this class.

---

## Wiring One External LED

**Components needed:**
- 1 LED (any color)
- 1 resistor (220Ω or 1KΩ)
- 2 jumper wires
- Breadboard

**Wiring steps:**
1. Push the LED into the breadboard — long leg in one row, short leg in the next row
2. Connect one end of the resistor to the same row as the LED's **short leg**
3. Connect the other end of the resistor to the **GND rail** (− rail)
4. Use a jumper wire from **Arduino pin 8** to the row with the LED's **long leg**
5. Use a jumper wire from **Arduino GND** to the **GND rail**

---

## Wiring Diagram

```
Arduino                          Breadboard
─────────                        ──────────────────────────────
Pin 8  ──[jumper wire]────────►  row 10, col a  (LED long leg +)
                                 row 10, col b ── row 11, col b  (LED short leg −)
                                 row 11, col c ──[resistor]──► row 11, col d
                                 row 11, col d (other resistor leg) ──► GND rail
GND    ──[jumper wire]────────►  GND rail (− rail)
```

**Double-check before plugging in USB:**
- LED long leg faces the Arduino pin wire
- Resistor connects LED's short leg row to GND rail
- GND wire from Arduino to the (−) rail

---

## The Code: Blinking an External LED

```cpp
void setup() {
    pinMode(8, OUTPUT);    // Pin 8 controls our external LED
}

void loop() {
    digitalWrite(8, HIGH);   // LED on
    delay(1000);             // Wait 1 second
    digitalWrite(8, LOW);    // LED off
    delay(1000);             // Wait 1 second
}
```

This is the same blink code from Lesson 01 — just using **pin 8** instead of pin 13.

The built-in LED on pin 13 might still be doing whatever your last program told it to do.

---

## Using Multiple Pins

You can control multiple LEDs by using different pins:

```cpp
void setup() {
    pinMode(8, OUTPUT);   // LED 1
    pinMode(9, OUTPUT);   // LED 2
}

void loop() {
    digitalWrite(8, HIGH);   // LED 1 on
    digitalWrite(9, LOW);    // LED 2 off
    delay(500);

    digitalWrite(8, LOW);    // LED 1 off
    digitalWrite(9, HIGH);   // LED 2 on
    delay(500);
}
```

Each LED needs its own resistor and its own pin — but they can share the GND rail.

---

## Common Mistakes

| Problem | Likely Cause |
|---|---|
| LED doesn't light up | LED is backwards — flip it around |
| LED is very dim | Missing or wrong resistor value |
| LED flickers or acts weird | Loose connection on breadboard |
| Nothing works at all | GND wire not connected, or wrong pin in code |
| One LED works, other doesn't | Check each LED has its own resistor to GND |

**Debugging tip:** If an LED doesn't work, swap it with one that does. If the new one works in that spot, the original LED might be dead.

---

## Key Takeaways

- Breadboards connect components without soldering — rows are connected, the trench separates sides
- LEDs have polarity: long leg (+) toward the pin, short leg (−) toward GND
- **Always use a resistor** with an LED to limit current
- Every external LED circuit: Arduino Pin → LED → Resistor → GND
- The code is the same as Lesson 01 — just use different pin numbers
- Multiple LEDs need multiple pins and resistors, but can share GND
