# ard06a — Car Door Ajar Alarm

**Programming — Medina County Career Center**
**Standards: ODE 5.1.1, 5.2.1, 5.2.3, 5.3.5, 5.4.2, 5.4.6**

---

## The Scenario

You will replicate that annoying chime your car makes when you leave the door open. 

Your photoresistor is the door sensor — when the "door" opens, light hits the sensor. Your system needs to:

1. **Detect** when the door opens (light level rises above a threshold)
2. **Show status** with LEDs — green for closed, red for open
3. **Sound an alarm** with a buzzer that gets more urgent the longer the door stays open

This is, of course, a simplified version of how real car door ajar systems work — a sensor detects the state, a dash indicator lights up, and the car chimes at you until you close it.

---

## What You Need

Keep everything from the photoresistor walkthrough (photoresistor, 10KΩ resistor, first LED). Add this from your kit:

- **1 green LED** + **220Ω resistor**
- **1 red LED** + **220Ω resistor**
- **Piezo buzzer** — small black cylinder that has two pins (one is usually marked + or is longer).
- 3–4 more jumper wires

You can remove the original LED from the walkthrough — you'll replace it with the green and red LEDs.

---

## Part 1 — Add the Green and Red LEDs

**Disconnect USB first.**

Keep your photoresistor and voltage divider wired exactly as before. Now add two LEDs:

### Green LED (door closed indicator)

- **Arduino pin 8** → 220Ω resistor → green LED long leg → short leg → GND rail

### Red LED (door open indicator)

- **Arduino pin 9** → 220Ω resistor → red LED long leg → short leg → GND rail

*(Pin 9 is PWM capable — we'll use that later to make the red LED pulse.)*

### Test the LEDs

Before adding the buzzer, write this code to verify both LEDs work:

```cpp
const int green_led = 8;
const int red_led = 9;

void setup() {
    pinMode(green_led, OUTPUT);
    pinMode(red_led, OUTPUT);
}

void loop() {
    digitalWrite(green_led, HIGH);
    digitalWrite(red_led, LOW);
    delay(1000);
    digitalWrite(green_led, LOW);
    digitalWrite(red_led, HIGH);
    delay(1000);
}
```

Both LEDs should alternate on/off every second. If one doesn't light up, check your wiring before moving on.

---

## Part 2 — Add the Piezo Buzzer

### What You Need to Know

A piezo buzzer makes sound when you send it a signal. Arduino has a built-in function for this:

- `tone(pin, frequency)` — starts playing a tone at the given frequency (in Hz)
- `tone(pin, frequency, duration)` — plays a tone for a specific number of milliseconds
- `noTone(pin)` — stops the tone

Some common frequencies to try:

| Sound | Frequency |
|---|---|
| Low beep | 500 Hz |
| Medium beep | 1000 Hz |
| High beep | 2000 Hz |
| Annoying car chime | 800 Hz |

### Wiring

The buzzer has two pins:

1. **Longer pin (or marked +)** → connect to **Arduino pin 10**
2. **Shorter pin (or unmarked)** → connect to **GND rail**

That's it — no resistor needed for a piezo buzzer.

### Test the Buzzer

```cpp
const int buzzer = 10;

void setup() {
    pinMode(buzzer, OUTPUT);
}

void loop() {
    tone(buzzer, 800, 200);      // 800Hz beep for 200ms
    delay(1000);                  // Wait 1 second between beeps
}
```

You should hear a short beep every second. If you don't hear anything, flip the buzzer around (swap the two pins) and try again.

---

## Part 3 — Basic Door Alarm

Now combine everything. Here's your starter code — **you need to fill in the missing parts:**

```cpp
const int green_led = 8;         // green LED — door closed
const int red_led = 9;           // red LED — door open
const int sensor_pin = A0;       // photoresistor
const int buzzer = 10;           // piezo buzzer
const int threshold = 500;       // adjust based on YOUR calibration!
int sensor;                       // sensor reading

void setup() {
    pinMode(green_led, OUTPUT);
    pinMode(red_led, OUTPUT);
    pinMode(buzzer, OUTPUT);
    Serial.begin(9600);
    Serial.println("Car door alarm ready");
}

void loop() {
    sensor = analogRead(sensor_pin);    // read sensor value

    Serial.print("Light: ");
    Serial.print(sensor);

    if (sensor > threshold) {
        // DOOR IS OPEN (light detected)
        // TODO: Turn red LED on, green LED off
        // TODO: Play a beep using tone()

        Serial.println("  DOOR OPEN");
    } else {
        // DOOR IS CLOSED (dark)
        // TODO: Turn green LED on, red LED off
        // TODO: Stop the buzzer using noTone()

        Serial.println("  Door closed");
    }

    delay(200);
}
```

### What to Do

1. Replace the `// TODO` comments with actual code
2. Upload and test — cover the sensor (door closed = green LED, silence) and uncover it (door open = red LED, beeping)
3. **Adjust your `threshold`** value based on the calibration you did in the walkthrough

### Expected Behavior

| Sensor State | Green LED | Red LED | Buzzer |
|---|---|---|---|
| Covered (door closed) | ON | OFF | Silent |
| Uncovered (door open) | OFF | ON | Beeping |

---

## Part 4 — Urgent Alarm (The Real Challenge)

A real car doesn't just beep once. The longer the door is open, the more annoying the chime gets. Make yours do the same.

### What You Need to Know: `millis()`

So far you've only used `delay()` for timing. The problem with `delay()` is that it freezes your entire program — you can't read sensors or do anything else while it's waiting.

`millis()` returns the number of milliseconds since the Arduino was turned on. You can use it to track time without freezing:

```cpp
unsigned long door_open_time = 0;    // when the door was opened
bool door_was_open = false;          // was it open last time we checked?
```

When the door first opens, save the current time:
```cpp
if (!door_was_open) {
    door_open_time = millis();
    door_was_open = true;
}
```

Then calculate how long it's been open:
```cpp
unsigned long elapsed = millis() - door_open_time;
```

### Your Task

Modify your alarm so the beeping changes over time:

| Time Door Open | Behavior |
|---|---|
| 0–3 seconds | Slow beep — one short beep per second (like a gentle reminder) |
| 3–8 seconds | Medium beep — two beeps per second, slightly higher pitch |
| 8+ seconds | Urgent — fast continuous beeping, high pitch, red LED pulses |

**Hints:**

- Use `millis()` to track how long the door has been open
- Use different `tone()` frequencies for each stage (try 600, 800, and 1200 Hz)
- For the urgent stage, use `analogWrite()` on the red LED (pin 9 is PWM) to pulse it
- When the door closes, **reset everything** — turn off the buzzer, reset the timer, go back to green LED

### Pseudocode to Get You Started

```
Read sensor

If door is open (light > threshold):
    If door just opened:
        Record the time with millis()

    Calculate elapsed time = millis() - door_open_time

    If elapsed < 3000ms:
        Slow beep (tone 600Hz, beep on/off every 1000ms)
        Red LED solid on

    Else if elapsed < 8000ms:
        Medium beep (tone 800Hz, beep on/off every 500ms)
        Red LED solid on

    Else:
        Urgent beep (tone 1200Hz, beep on/off every 150ms)
        Pulse red LED using analogWrite with a changing brightness

Else (door is closed):
    Green LED on, red LED off
    Stop the buzzer
    Reset the timer flag
```

**For the beep on/off pattern without using `delay()`**, think about `millis()` and the modulo operator `%`:

```cpp
// This creates a beep that's on for half the interval, off for the other half
if ((millis() % 1000) < 500) {
    tone(buzzer, 600);
} else {
    noTone(buzzer);
}
```

**For pulsing the red LED**, you can use a sine wave with `millis()`:

```cpp
int brightness = (sin(millis() / 100.0) + 1) * 127;
analogWrite(red_led, brightness);
```

---

## Part 5 — Show Off and Document

When your alarm is working with all three stages:

1. **Demonstrate** for Mr. McMaster:
   - Cover the sensor — green LED, silence
   - Uncover it — watch it escalate through all three alarm stages
   - Cover it again — everything resets


## Checklist

- [ ] Green LED lights when sensor is covered (door closed)
- [ ] Red LED lights when sensor is uncovered (door open)
- [ ] Buzzer beeps when door is open
- [ ] Alarm escalates through 3 stages based on time
- [ ] Red LED pulses during urgent stage
- [ ] Everything resets when door closes
