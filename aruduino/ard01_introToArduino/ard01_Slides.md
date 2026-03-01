---
marp: true
theme: default
class: invert
paginate: true
---

# Lesson 01: Introduction to Arduino
## Programming
### Medina County Career Center
**Guest Instructor: Matt Schmidt**

---

## About Matt Schmidt

- Matt's education and career path
- Working with industrial sensors, automation, and embedded systems
- Why physical computing matters in the real world
- Microcontrollers in everyday life: cars, appliances, medical devices, manufacturing

---

## What Is a Microcontroller?

A **microcontroller** is a small computer on a single chip.

- Has a processor, memory, and I/O pins
- Runs **one program** in a loop (not a full OS like your laptop)
- Used in embedded systems: things that aren't "computers" but have computers inside them

**Examples:**
- Thermostat reading temperature and controlling HVAC
- Car engine management system
- Traffic light controller
- Your coffee maker's timer

---

## The Arduino Uno R4 WiFi

Your board at a glance:

- **Microcontroller**: Renesas RA4M1 (32-bit ARM Cortex-M4)
- **Clock Speed**: 48 MHz
- **Digital I/O Pins**: 14 (6 can do PWM)
- **Analog Input Pins**: 6
- **Operating Voltage**: 5V
- **USB-C** connection to your computer
- **Built-in WiFi** and **LED matrix** on the board

Pin 13 has a built-in LED — no wiring needed to get started!

---

## Arduino vs C Programming

You've been writing C code compiled with `gcc`.
Arduino uses **C/C++** but with a different workflow:

| C (gcc) | Arduino |
|---------|---------|
| Write `.c` files | Write `.ino` files (sketches) |
| Compile with `gcc` in terminal | Compile with Arduino IDE |
| Runs on your computer | Uploads to the board via USB |
| `int main()` entry point | `setup()` and `loop()` entry points |
| `printf()` for output | `Serial.println()` for output |

The syntax is almost identical — you already know most of this!

---

## The Arduino IDE

The **Integrated Development Environment** where you write, compile, and upload code.

Key parts:
- **Editor**: Where you write your sketch
- **Verify button** (checkmark): Compiles your code and checks for errors
- **Upload button** (arrow): Compiles AND sends code to the board
- **Serial Monitor**: See text output from your board
- **Board selector**: Choose your board and USB port

We'll use **Arduino IDE 2.x** for this class.

---

## Program Structure: setup() and loop()

Every Arduino program has two functions:

```cpp
void setup() {
    // Runs ONCE when the board powers on
    // Use for: setting pin modes, initializing serial
}

void loop() {
    // Runs OVER AND OVER forever
    // Use for: reading sensors, blinking LEDs, main logic
}
```

Think of it like:
- `setup()` = getting dressed in the morning (do it once)
- `loop()` = breathing (do it forever)

---

## Digital Pins: OUTPUT and INPUT

Before using a pin, tell the Arduino what it does:

```cpp
pinMode(13, OUTPUT);  // I will SEND signals to pin 13
pinMode(7, INPUT);    // I will READ signals from pin 7
```

- **OUTPUT**: You're talking TO the pin (LEDs, motors, buzzers)
- **INPUT**: You're listening FROM the pin (buttons, sensors)

Pin mode is set in `setup()` — you only need to do it once.

---

## digitalWrite() — Turning Things On and Off

Send a HIGH (5V) or LOW (0V) signal to a pin:

```cpp
digitalWrite(13, HIGH);  // Turn pin 13 ON (5 volts)
digitalWrite(13, LOW);   // Turn pin 13 OFF (0 volts)
```

- **HIGH** = 5 volts = ON = 1
- **LOW** = 0 volts = OFF = 0

Pin 13 has a built-in LED, so `digitalWrite(13, HIGH)` lights it up!

---

## delay() — Pausing the Program

```cpp
delay(1000);  // Wait for 1000 milliseconds (1 second)
delay(500);   // Wait for 500 milliseconds (half a second)
delay(100);   // Wait for 100 milliseconds (1/10 of a second)
```

**Milliseconds**: 1000 ms = 1 second

| Seconds | Milliseconds |
|---------|-------------|
| 0.1 s | 100 ms |
| 0.25 s | 250 ms |
| 0.5 s | 500 ms |
| 1 s | 1000 ms |
| 2 s | 2000 ms |

---

## Your First Program: Blink

```cpp
void setup() {
    pinMode(13, OUTPUT);   // Pin 13 is an output
}

void loop() {
    digitalWrite(13, HIGH);  // LED on
    delay(1000);             // Wait 1 second
    digitalWrite(13, LOW);   // LED off
    delay(1000);             // Wait 1 second
}
```

This blinks the built-in LED: 1 second on, 1 second off, forever.

---

## What Happens Without delay()?

```cpp
void loop() {
    digitalWrite(13, HIGH);
    digitalWrite(13, LOW);
}
```

The LED turns on and off **millions of times per second**.

Your eyes can't see it blinking — it just looks dim.

**The delay gives your eyes time to see the change.**

---

## Uploading Your Code

1. Connect the Arduino via USB-C
2. Select your board: **Arduino Uno R4 WiFi**
3. Select the correct **COM port** (where Arduino shows up)
4. Click the **Upload** button (right arrow)
5. Watch for "Done uploading" in the console

If you get errors:
- Check the board selection (Tools → Board)
- Check the port selection (Tools → Port)
- Read the error message — it tells you the line number

---

## The Serial Monitor

Send text from the Arduino back to your computer:

```cpp
void setup() {
    Serial.begin(9600);          // Start serial at 9600 baud
    Serial.println("Hello!");    // Print a line of text
}

void loop() {
    Serial.println("Looping...");
    delay(1000);
}
```

Open with: **Tools → Serial Monitor** (or the magnifying glass icon)

Set baud rate to **9600** to match your code.

---

## Key Commands Summary

| Command | What It Does |
|---------|-------------|
| `pinMode(pin, mode)` | Set a pin as INPUT or OUTPUT |
| `digitalWrite(pin, value)` | Send HIGH or LOW to a pin |
| `delay(ms)` | Pause for milliseconds |
| `Serial.begin(9600)` | Start serial communication |
| `Serial.println(text)` | Print text to Serial Monitor |

---

## Key Takeaways

- Arduino runs **C/C++** — you already know the basics from our C unit
- Every sketch has `setup()` (runs once) and `loop()` (runs forever)
- `pinMode()` configures pins; `digitalWrite()` sends signals
- `delay()` pauses execution in milliseconds
- Pin 13 has a built-in LED — perfect for learning without circuits
- The Serial Monitor lets you see output from the board
