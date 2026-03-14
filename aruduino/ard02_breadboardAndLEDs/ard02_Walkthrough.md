# Arduino Walkthrough: Breadboards, Resistors, and External LEDs

**Programming — Medina County Career Center**

---

## What We're Doing

In Lesson 01, you blinked the built-in LED on pin 13 — no wiring needed. Today you're going to build your first **real circuit** on a breadboard: connecting an external LED with a resistor and controlling it with your Arduino. By the end, you'll have an LED blinking on the breadboard that you wired up yourself.

---

## Part 1 — Gather Your Components

Open your kit and find:

- **1 LED** (any color — red, green, yellow, or blue)
- **1 resistor** — use a 220Ω (red-red-brown-gold) or 1KΩ (brown-black-red-gold)
- **2 jumper wires** (one for the signal pin, one for GND)
- **Your breadboard**
- **Your Arduino Uno R4 WiFi** (with USB cable)

**Don't plug in the USB cable yet.** Always build the circuit first, then power it up.

---

## Part 2 — Understand the Breadboard

Before wiring anything, take a look at your breadboard:

### The Connection Rules

Pick up the breadboard and look at the holes. Here's how they're connected underneath:

**Component area (middle section):**
- Each short row of 5 holes (a-b-c-d-e) is connected together
- The other side (f-g-h-i-j) is also connected in rows of 5
- The **trench** down the middle separates the two sides — they are NOT connected across it

**Power rails (long strips on the edges):**
- The `+` rail runs vertically down the whole board — use for 5V power
- The `−` rail runs vertically down the whole board — use for GND (ground)

### Test Your Understanding

If you push a wire into hole **b5** and another wire into hole **d5**, are they connected? **Yes** — same row (5), same side of the trench.

If you push a wire into hole **e5** and another into hole **f5**? **No** — the trench separates them.

---

## Part 3 — Understand the LED

Pick up an LED from your kit and look at it closely.

**Two legs, two lengths:**
- **Long leg** = positive = anode — this side gets the signal from the Arduino pin
- **Short leg** = negative = cathode — this side connects toward GND

**Another way to tell:** Look at the flat edge on the round plastic body of the LED. The flat side is always the **negative (cathode)** side.

**Why does this matter?** LEDs only work in one direction. If you wire it backwards, it won't light up. It won't break — it just won't work. If your LED doesn't turn on, the first thing to try is flipping it around.

---

## Part 4 — Wire the Circuit

Here's what we're building: a single LED on **pin 8**, with a resistor to GND.

### Step-by-Step Wiring

**Step 1: Place the LED**

Push the LED into the breadboard so the two legs are in **different rows**:
- Long leg (+) in **row 10** (for example, hole **e10**)
- Short leg (−) in **row 11** (for example, hole **e11**)

The LED straddles two rows. Each leg is now accessible through the other holes in its row.

**Step 2: Place the resistor**

Push one leg of the resistor into the **same row as the LED's short leg** — for example, hole **a11**.

Push the other leg of the resistor into a hole on the **GND rail** (the `−` strip on the edge of the board).

The resistor now connects the LED's negative side to ground.

**Step 3: Connect the signal wire**

Use a jumper wire to connect **Arduino pin 8** to the **same row as the LED's long leg** — for example, hole **a10**.

**Step 4: Connect the ground wire**

Use a jumper wire to connect **Arduino GND** to the **GND rail** (the `−` strip) on the breadboard.

### Wiring Checklist

Before plugging in USB, verify:

- [ ] LED long leg (+) is in the row connected to the Arduino pin wire
- [ ] LED short leg (−) is in a different row
- [ ] Resistor connects the short leg's row to the GND rail
- [ ] Jumper wire from Arduino pin 8 to the long leg's row
- [ ] Jumper wire from Arduino GND to the GND rail
- [ ] Nothing is loose — push components in firmly

---

## Part 5 — Write the Code

Now plug in your Arduino via USB. Open the Arduino IDE.

Create a new sketch (**File → New Sketch**) and type this:

```cpp
void setup() {
    pinMode(8, OUTPUT);
    Serial.begin(9600);
    Serial.println("External LED ready!");
}

void loop() {
    digitalWrite(8, HIGH);
    delay(1000);
    digitalWrite(8, LOW);
    delay(1000);
}
```

### Upload It

1. Make sure your board and port are selected (Tools → Board, Tools → Port)
2. Click the **Upload** button (right arrow)
3. Wait for "Done uploading"
4. Look at your breadboard — the external LED should be blinking!

If the LED doesn't blink:
- Check that the LED isn't backwards (flip it)
- Check that the resistor connects to the GND rail
- Check that the GND wire goes from Arduino GND to the GND rail
- Check that your code says pin 8, and your wire is in pin 8

---

## Part 6 — Add a Second LED

Now let's add a second LED on **pin 9**.

### Wire the Second LED

Repeat the same wiring pattern:
1. New LED: long leg in **row 15**, short leg in **row 16** (or any unused rows)
2. Resistor from **row 16** to the **GND rail**
3. Jumper wire from **Arduino pin 9** to **row 15**

Both LEDs share the same GND rail — that's fine. They each need their own resistor.

### Update the Code

```cpp
void setup() {
    pinMode(8, OUTPUT);
    pinMode(9, OUTPUT);
    Serial.begin(9600);
    Serial.println("Two LEDs ready!");
}

void loop() {
    // Alternating pattern
    digitalWrite(8, HIGH);
    digitalWrite(9, LOW);
    delay(500);

    digitalWrite(8, LOW);
    digitalWrite(9, HIGH);
    delay(500);
}
```

Upload and observe. The two LEDs should alternate — when one is on, the other is off.

---

## Part 7 — Experiment

Try these modifications:

**Both on, both off:**
```cpp
void loop() {
    digitalWrite(8, HIGH);
    digitalWrite(9, HIGH);
    delay(1000);

    digitalWrite(8, LOW);
    digitalWrite(9, LOW);
    delay(1000);
}
```

**Chase pattern (if you add a third LED on pin 10):**
```cpp
void loop() {
    digitalWrite(8, HIGH); delay(200);
    digitalWrite(8, LOW);

    digitalWrite(9, HIGH); delay(200);
    digitalWrite(9, LOW);

    digitalWrite(10, HIGH); delay(200);
    digitalWrite(10, LOW);
}
```

---

## Completion Checklist

- [ ] Single LED on breadboard wired correctly with resistor
- [ ] LED blinks using code with `pinMode(8, OUTPUT)` and `digitalWrite(8, HIGH/LOW)`
- [ ] Second LED added on a different pin
- [ ] Alternating blink pattern working with two LEDs
- [ ] Can explain: why we need a resistor, what happens if the LED is backwards

**When all boxes are checked, show your circuit and screen to your instructor. You're done!**
