# Lesson 01: Introduction to Arduino
## Study Guide & Reference

**Programming — Medina County Career Center**

---

This guide is your reference for everything in Arduino Lesson 01. Use it while you work through the task files — it has syntax examples, worked problems, and vocabulary you'll need.

---

## 1. WHAT IS AN ARDUINO?

An Arduino is a **microcontroller board** — a small computer designed to interact with the physical world. Unlike your laptop, which runs a full operating system and many programs at once, an Arduino runs **one program** in an infinite loop.

**What makes Arduino special:**
- It has **pins** that connect to LEDs, sensors, motors, buttons, and more
- You write code on your computer, then **upload** it to the board via USB
- The code runs on the board — even after you unplug it from your computer (it runs on any power source)
- It uses **C/C++** — so everything you learned about C applies here

**Your board: Arduino Uno R4 WiFi**
- 14 digital input/output pins (numbered 0–13)
- 6 analog input pins (A0–A5)
- USB-C connection
- Built-in WiFi and Bluetooth
- Built-in LED connected to **pin 13**
- Built-in 12x8 LED matrix on the front

---

## 2. PROGRAM STRUCTURE: setup() AND loop()

Every Arduino sketch (program) has exactly two required functions:

```cpp
void setup() {
    // Runs ONE TIME when the board powers on or resets
}

void loop() {
    // Runs OVER AND OVER forever after setup() finishes
}
```

### How it compares to C:

| Concept | C (gcc) | Arduino |
|---|---|---|
| Entry point | `int main()` | `void setup()` + `void loop()` |
| Runs once | Everything in `main()` | Code in `setup()` |
| Runs repeatedly | Only with a `while` loop | Code in `loop()` automatically |
| Return value | `return 0;` | Not needed |

### What goes where:

**Put in `setup()`:**
- `pinMode()` calls — setting up your pins
- `Serial.begin()` — starting serial communication
- Any one-time initialization

**Put in `loop()`:**
- Reading sensors
- Turning LEDs on/off
- Main program logic
- Anything you want to repeat

### Worked Example: The Simplest Sketch

```cpp
void setup() {
    pinMode(13, OUTPUT);       // Configure pin 13 as output
    Serial.begin(9600);        // Start serial communication
    Serial.println("Ready!");  // Print once
}

void loop() {
    // This runs forever but does nothing
}
```

**Output (Serial Monitor):**
```
Ready!
```

The message prints once because `Serial.println` is in `setup()`. The `loop()` runs forever but has nothing in it.

---

## 3. PINMODE — CONFIGURING PINS

Before you use a pin, you must tell the Arduino whether it's an **input** or an **output**:

```cpp
pinMode(pinNumber, mode);
```

### Modes

| Mode | Use | Example |
|---|---|---|
| `OUTPUT` | Sending signals (LEDs, buzzers, motors) | `pinMode(13, OUTPUT);` |
| `INPUT` | Receiving signals (buttons, sensors) | `pinMode(7, INPUT);` |

### Worked Example

```cpp
void setup() {
    pinMode(13, OUTPUT);  // I will send signals TO pin 13 (LED)
    pinMode(7, INPUT);    // I will read signals FROM pin 7 (button)
}
```

**Important:**
- Pin mode is set in `setup()` — you only do it once
- Case matters: `OUTPUT` not `output`, `INPUT` not `input`
- You must set the pin mode before using `digitalWrite()` or `digitalRead()`

---

## 4. DIGITALWRITE — SENDING SIGNALS

Send a **HIGH** (5V, on) or **LOW** (0V, off) signal to a pin:

```cpp
digitalWrite(pinNumber, value);
```

| Value | Voltage | Effect on LED |
|---|---|---|
| `HIGH` | 5 volts | LED turns **on** |
| `LOW` | 0 volts | LED turns **off** |

### Worked Example: Turn LED On Then Off

```cpp
void setup() {
    pinMode(13, OUTPUT);
}

void loop() {
    digitalWrite(13, HIGH);   // LED on
    delay(1000);              // Wait 1 second
    digitalWrite(13, LOW);    // LED off
    delay(1000);              // Wait 1 second
}
```

**What happens:** The LED on pin 13 blinks — 1 second on, 1 second off, forever.

---

## 5. DELAY — PAUSING THE PROGRAM

```cpp
delay(milliseconds);
```

Pauses the program for the given number of **milliseconds**. The Arduino does nothing during a `delay()` — it just waits.

### Milliseconds Conversion

```
1 second     = 1000 milliseconds
0.5 seconds  = 500 milliseconds
0.25 seconds = 250 milliseconds
0.1 seconds  = 100 milliseconds
2 seconds    = 2000 milliseconds
5 seconds    = 5000 milliseconds
```

**Formula:** `milliseconds = seconds × 1000`

### Worked Example: Different Blink Speeds

```cpp
void loop() {
    // Fast blink (5 blinks per second)
    digitalWrite(13, HIGH);
    delay(100);
    digitalWrite(13, LOW);
    delay(100);
}
```

```cpp
void loop() {
    // Slow blink (1 blink every 4 seconds)
    digitalWrite(13, HIGH);
    delay(2000);
    digitalWrite(13, LOW);
    delay(2000);
}
```

```cpp
void loop() {
    // Asymmetric: long on, short off
    digitalWrite(13, HIGH);
    delay(1500);
    digitalWrite(13, LOW);
    delay(300);
}
```

---

## 6. SERIAL COMMUNICATION

The **Serial Monitor** lets the Arduino send text back to your computer over USB. This is your `printf()` for Arduino.

### Setting Up Serial

In `setup()`:
```cpp
Serial.begin(9600);  // Start serial at 9600 baud (bits per second)
```

### Printing Text

```cpp
Serial.println("Hello!");       // Prints text with a newline at the end
Serial.print("No newline");     // Prints text WITHOUT a newline
Serial.println(42);             // Prints a number
Serial.println(3.14);           // Prints a float
```

### print() vs println()

| Function | Output | Newline? |
|---|---|---|
| `Serial.print("A");` | `A` | No |
| `Serial.println("A");` | `A` + newline | Yes |

### Worked Example: Printing a Counter

```cpp
int count = 0;

void setup() {
    Serial.begin(9600);
    Serial.println("Counter starting!");
}

void loop() {
    count = count + 1;
    Serial.print("Count: ");
    Serial.println(count);
    delay(1000);
}
```

**Output (Serial Monitor):**
```
Counter starting!
Count: 1
Count: 2
Count: 3
Count: 4
...
```

### How it compares to C:

| C (printf) | Arduino (Serial) |
|---|---|
| `printf("Hello\n");` | `Serial.println("Hello");` |
| `printf("x = %d\n", x);` | `Serial.print("x = "); Serial.println(x);` |
| `printf("%.2f", 3.14);` | `Serial.println(3.14);` |

**Key difference:** Arduino's `Serial.println()` doesn't use format specifiers like `%d`. Instead, you chain `print()` and `println()` calls together.

---

## 7. VARIABLES IN ARDUINO

Variables work the same as in C — you must declare the type:

```cpp
int ledPin = 13;         // Whole number
int delayTime = 500;     // Milliseconds to wait
float voltage = 3.3;     // Decimal number
char letter = 'A';       // Single character
bool isOn = true;        // Boolean: true or false
```

### Worked Example: Using Variables for Timing

```cpp
int ledPin = 13;
int onTime = 1000;
int offTime = 250;

void setup() {
    pinMode(ledPin, OUTPUT);
}

void loop() {
    digitalWrite(ledPin, HIGH);
    delay(onTime);
    digitalWrite(ledPin, LOW);
    delay(offTime);
}
```

**Why use variables?** If you want to change the timing, you change it in **one place** at the top instead of hunting through your code for every `delay(1000)`.

---

## 8. LOOPS IN ARDUINO

Loops work exactly like C:

### For Loop

```cpp
for (int i = 0; i < 5; i++) {
    digitalWrite(13, HIGH);
    delay(200);
    digitalWrite(13, LOW);
    delay(200);
}
```

This blinks the LED 5 times, then the `loop()` function restarts and does it again.

### While Loop

```cpp
int count = 0;
while (count < 3) {
    digitalWrite(13, HIGH);
    delay(500);
    digitalWrite(13, LOW);
    delay(500);
    count++;
}
```

---

## 9. COMMON MISTAKES AND FIXES

**Missing semicolon:**
```
error: expected ';' before '}' token
```
You forgot a `;` at the end of a line. Check the line the error points to, and also the line above it.

**Wrong case:**
```cpp
pinmode(13, output);    // WRONG — won't compile
pinMode(13, OUTPUT);    // CORRECT
```
Arduino commands are case-sensitive. `pinMode`, `digitalWrite`, `HIGH`, `LOW`, `OUTPUT`, `INPUT` must be exact.

**Wrong board or port:**
```
avrdude: ser_open(): can't open device
```
Go to Tools → Board and Tools → Port and make sure both are set correctly.

**Serial Monitor shows garbage:**
Make sure the baud rate in the Serial Monitor matches what's in your code. If your code says `Serial.begin(9600)`, set the monitor to `9600`.

**LED doesn't blink (looks dim instead):**
You probably forgot `delay()`. Without delays, the LED switches on and off millions of times per second — too fast for your eyes.

---

## VOCABULARY

**Arduino** — An open-source microcontroller platform used for building electronics projects. The board runs one program at a time and can interact with physical components through its pins.

**Sketch** — The Arduino term for a program. Saved as `.ino` files.

**IDE (Integrated Development Environment)** — The software where you write, compile, and upload your code. Arduino IDE 2.x is what we use.

**Microcontroller** — A small computer on a single chip with a processor, memory, and input/output capabilities. Runs embedded programs.

**Pin** — A physical connection point on the Arduino board. Digital pins send or receive HIGH/LOW signals. Analog pins can read a range of values.

**Digital Signal** — A signal that is either HIGH (5V, on) or LOW (0V, off). Only two states — like a light switch.

**setup()** — The Arduino function that runs once when the board powers on. Used for initialization.

**loop()** — The Arduino function that runs repeatedly forever after `setup()` finishes. Contains the main program logic.

**pinMode()** — Configures a pin as INPUT or OUTPUT. Must be called before using the pin.

**digitalWrite()** — Sends a HIGH or LOW signal to a digital pin. Used to turn things on and off.

**delay()** — Pauses the program for a specified number of milliseconds. 1000 ms = 1 second.

**Serial Monitor** — A tool in the Arduino IDE that displays text sent from the board to your computer over USB. Used for debugging.

**Baud Rate** — The speed of serial communication in bits per second. We use 9600 baud.

**Upload** — The process of compiling your sketch and sending it to the Arduino board via USB.

**Compile** — Converting your human-readable code into machine instructions the microcontroller can execute.

**LED (Light Emitting Diode)** — A small light component. Pin 13 on the Arduino has a built-in LED that requires no wiring.

---

## ODE COMPETENCIES COVERED

**5.1.1** — Describe how computer programs and scripts can be used to solve problems
**5.2.1** — Data types and variables
**5.2.3** — Arithmetic operations
**5.3.6** — Repetition control structures (while, for)
**5.4.1** — Configure options, preferences, and tools
**5.4.2** — Write and edit code in the IDE
**5.4.3** — Compile or interpret a working program
**5.4.6** — Testing and debugging
**5.4.7** — Error identification
**5.5.5** — Use appropriate naming conventions and apply comments
