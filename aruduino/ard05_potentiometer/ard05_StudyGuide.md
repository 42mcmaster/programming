# Lesson 05: Reading Analog Voltages — The Potentiometer
## Study Guide & Reference

**Programming — Medina County Career Center**

---

## 1. DIGITAL vs. ANALOG

### Digital
Digital signals have only two states: **HIGH** (5V) or **LOW** (0V). Everything you've done so far — `digitalWrite()`, LED on/off — has been digital.

### Analog
Analog signals have a **continuous range** of values. In the real world, most things are analog: temperature doesn't jump from "cold" to "hot" — it changes gradually. Light doesn't switch from dark to bright — it fades.

The Arduino can **read** analog voltages between 0V and 5V and convert them into a number.

---

## 2. ANALOG PINS

The Arduino Uno R4 has **6 analog input pins** labeled **A0 through A5**. These are separate from the digital pins (0–13).

Paul uses `pinMode(potPin, INPUT)` to set analog pins as input. Technically the Arduino sets them to input by default, but Paul's approach is good practice — it makes your code clear about what each pin does.

**Do not apply more than 5V to an analog pin — it can damage the Arduino.**

---

## 3. analogRead()

```cpp
int value = analogRead(A0);
```

Reads the voltage on the specified analog pin and returns a number from **0 to 1023**.

| Voltage on pin | analogRead returns |
|---|---|
| 0.0V | 0 |
| 0.5V | ~102 |
| 1.0V | ~205 |
| 2.5V | ~512 |
| 5.0V | 1023 |

### Resolution

The Arduino uses a **10-bit ADC** (Analog-to-Digital Converter). 10 bits = 2^10 = 1024 steps. That means it divides the 0–5V range into 1024 levels.

**Voltage per step:** 5V ÷ 1024 = approximately 0.00488V per step

### Converting to Voltage

```cpp
float voltage = (analogRead(A0) / 1023.0) * 5.0;
```

**Critical:** Use `1023.0` (float), not `1023` (integer). Integer division in C/Arduino truncates — `500 / 1023` gives `0`, not `0.489`.

---

## 4. THE POTENTIOMETER

A **potentiometer** (pot) is a variable resistor with a rotating knob.

### How It Works

Inside the potentiometer is a strip of resistive material with a slider (wiper) that moves when you turn the knob. The wiper divides the resistance into two parts.

When connected to 5V and GND, turning the knob moves the wiper between 5V and 0V, producing any voltage in between on the middle pin.

### Pin Layout

```
   [Left]     [Middle]    [Right]
     │           │           │
    5V        Signal       GND
              (wiper)
           → to Arduino A0
```

Swap left/right if the direction feels backwards — it just reverses the range.

### Wiring

| Pot Pin | Arduino Pin |
|---|---|
| Left | **5V** |
| Middle (wiper) | **A0** (or any analog pin) |
| Right | **GND** |

No resistor needed — the potentiometer IS the resistor.

---

## 5. PAUL'S CODING STYLE: NO MAGIC NUMBERS

In Paul McWhorter's lessons, every number gets a variable declared at the top of the sketch:

```cpp
int potPin = A0;    // Which pin the potentiometer is on
int potVal;         // Variable to store the reading (assigned later)
int br = 9600;      // Baud rate for Serial Monitor
int wt = 100;       // Wait time (delay) in milliseconds

void setup() {
    pinMode(potPin, INPUT);
    Serial.begin(br);
}

void loop() {
    potVal = analogRead(potPin);
    Serial.println(potVal);
    delay(wt);
}
```

**Why do this?** A raw number like `9600` buried in your code is called a "magic number" — someone reading the code has to guess what it means. By putting it in a variable called `br` (baud rate), the code explains itself. It also means if you want to change the delay from 100 to 200, you change `wt` once at the top instead of hunting through your code.

**Paul's variable naming style:** Short and descriptive — `potPin`, `potVal`, `br`, `wt`. Not single letters, but not long sentences either.

---

## 6. SERIAL MONITOR FOR DATA

The Serial Monitor is your window into what the Arduino is reading. For analog sensors, it's essential — you can't see a voltage, but you can see the number.

### Printing Values

```cpp
Serial.println(potVal);                    // Just the number
Serial.print("Value: "); Serial.println(potVal);   // Label + number
```

### Printing Multiple Values on One Line

```cpp
Serial.print("Raw: ");
Serial.print(potVal);
Serial.print("  Voltage: ");
Serial.print(voltage);
Serial.println("V");
// Output: Raw: 512  Voltage: 2.50V
```

`Serial.print()` stays on the same line. `Serial.println()` adds a newline at the end.

### Delay and Readability

Without a delay, `analogRead()` runs thousands of times per second and the Serial Monitor scrolls too fast to read. Use `delay(100)` or `delay(200)` for readable output.

---

## 7. COMMON PATTERNS

### Reading and printing every 200ms

```cpp
void loop() {
    int val = analogRead(A0);
    Serial.println(val);
    delay(200);
}
```

### Only printing when the value changes

```cpp
int lastVal = 0;

void loop() {
    int val = analogRead(A0);
    if (abs(val - lastVal) > 5) {
        Serial.println(val);
        lastVal = val;
    }
    delay(50);
}
```

### Mapping to a different range

```cpp
int brightness = map(analogRead(A0), 0, 1023, 0, 255);
// Converts 0-1023 range to 0-255 range (useful for analogWrite)
```

---

## 8. FLOAT vs. INT

| Type | What it stores | Example |
|---|---|---|
| `int` | Whole numbers only | `512`, `-3`, `1023` |
| `float` | Decimal numbers | `2.5`, `0.00488`, `3.14` |

`analogRead()` returns an `int`. But voltage calculations need `float` for decimals.

**Integer division trap:**
```cpp
int result = 500 / 1023;      // result = 0 (integer truncation!)
float result = 500 / 1023.0;  // result = 0.489 (correct)
```

Always use at least one decimal number in the division to get a `float` result.

---

## VOCABULARY

**Analog** — A signal that varies continuously over a range, as opposed to digital (only two states).

**ADC (Analog-to-Digital Converter)** — Hardware inside the Arduino that converts an analog voltage into a digital number. The Arduino has a 10-bit ADC.

**Potentiometer** — A variable resistor with a knob that produces a voltage between 0V and 5V on its middle pin.

**Wiper** — The moving contact inside a potentiometer that slides along the resistive strip when you turn the knob.

**Resolution** — How many distinct levels a measurement can distinguish. 10-bit = 1024 levels.

**Float** — A data type that stores decimal numbers (floating-point). Needed for voltage calculations.

**map()** — An Arduino function that converts a value from one range to another. `map(val, fromLow, fromHigh, toLow, toHigh)`.

---

## ODE COMPETENCIES COVERED

**5.1.1** — Describe how computer programs and scripts can be used to solve problems
**5.2.1** — Data types and variables (int vs. float, analog values)
**5.2.3** — Arithmetic operations (voltage calculation, type conversion)
**5.4.2** — Write and edit code in the IDE
**5.4.6** — Testing and debugging
