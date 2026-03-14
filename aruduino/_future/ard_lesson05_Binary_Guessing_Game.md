## Follow-On Task: Binary Guessing Game

**What to do:**
Turn your 4-LED circuit into a guessing game. The Arduino picks a random number between 0 and 15, shows it on the LEDs in binary, and waits for you to type your guess in the Serial Monitor. It tells you if you're right or wrong, then picks a new number.

**No new wiring needed** — same four LEDs on pins 13, 12, 11, 10.

---

### Step 1: Understand the Serial Monitor

The Serial Monitor is a text window built into the Arduino IDE. Your sketch can send messages to it and read typed input from it. Open it with the magnifying glass icon in the top-right of the IDE. **Make sure the baud rate dropdown says 9600** — if it doesn't match your code, you'll see gibberish or nothing at all.

Two commands you'll use:

```cpp
Serial.begin(9600);      // Opens the connection — goes in setup(), must match monitor's baud rate
Serial.println("text");  // Sends a line of text to the monitor (like print in Python)
Serial.parseInt();       // Reads a number the user typed and returns it as an integer
```

And one for checking if the user has typed anything yet:

```cpp
Serial.available()  // Returns how many characters are waiting to be read
                    // If it's 0, the user hasn't typed anything yet
```

---

### Step 2: Understand the New Functions and Syntax

**`random()` — picking a random number**

```cpp
int num = random(0, 16);  // Picks a random integer from 0 up to (but NOT including) 16
                           // So the range is 0–15
```

`randomSeed(analogRead(A0))` goes in `setup()` before you use `random()`. It reads electrical noise from an unused pin to make sure the sequence is different every time the board starts up. Without it, you'd get the same "random" numbers every run.

---

**`showBinary()` — your first custom function**

Instead of writing 4 `digitalWrite` lines every time you want to show a number, you can define a function once and call it by name. Here's the structure:

```cpp
void showBinary(int num) {
    // code that runs when showBinary() is called
    // num is whatever value you pass in — like showBinary(7) makes num equal 7
}
```

Then anywhere in `loop()` you just write:

```cpp
showBinary(answer);  // Runs your function with answer as the input
```

This is the same concept as functions in JavaScript or `def` in Python — define once, use anywhere.

---

**The `&` operator — checking one bit at a time**

This is the trickiest new idea. The `&` (bitwise AND) operator lets you check whether a specific bit is ON in a number.

Think back to the binary table. The number 11 in binary is `1011`. To check if the 8s bit is on, you ask: does this number have a 1 in the 8s column?

```cpp
num & 8   // Is the 8s bit ON in num?  (8 in binary = 1000)
num & 4   // Is the 4s bit ON in num?  (4 in binary = 0100)
num & 2   // Is the 2s bit ON in num?  (2 in binary = 0010)
num & 1   // Is the 1s bit ON in num?  (1 in binary = 0001)
```

If the result is non-zero, that bit is ON. If it's zero, that bit is OFF. You can use this directly in an `if` statement or use it to decide between HIGH and LOW.

The shorthand `condition ? valueIfTrue : valueIfFalse` is a compact if/else:

```cpp
(num & 8) ? HIGH : LOW   // If the 8s bit is on → HIGH, otherwise → LOW
```

Is the same as writing:
```cpp
if (num & 8) {
    HIGH
} else {
    LOW
}
```

---

### Step 3: Pseudocode — Plan Before You Code

Read through this pseudocode and make sure you understand the flow before writing a single line:

```
SETUP:
  set pins 13, 12, 11, 10 as OUTPUT
  open Serial connection at 9600 baud
  seed the random number generator
  print a welcome message to Serial Monitor

LOOP (repeats forever):
  pick a random number between 0 and 15, store it
  show that number on the LEDs in binary
  print "What number am I showing?" to Serial Monitor

  wait until the user types something
    (keep checking Serial.available() until it's not zero)

  read the number they typed
  
  if their guess equals the stored number:
    print "Correct!" and the number
  else:
    print "Wrong!" and the number

  wait 3 seconds before the next round
```

---

### Step 4: Starter Code

This gives you the structure. Your job is to fill in the missing pieces marked with `// ???`.

```cpp
// Binary Guessing Game
// Uses 4 LEDs to display a random binary number.
// Player guesses the decimal value via Serial Monitor.

int answer = 0;

// --- Custom function: shows a number 0-15 on the LEDs ---
// Fill in the digitalWrite lines using the & operator
void showBinary(int num) {
  digitalWrite(13, ???);   // 8s place: is bit 8 on in num?
  digitalWrite(12, ???);   // 4s place: is bit 4 on in num?
  digitalWrite(11, ???);   // 2s place: is bit 2 on in num?
  digitalWrite(10, ???);   // 1s place: is bit 1 on in num?
}

void setup() {
  pinMode(13, OUTPUT);
  pinMode(12, OUTPUT);
  pinMode(11, OUTPUT);
  pinMode(10, OUTPUT);

  Serial.begin(???);                  // What baud rate should this be?
  randomSeed(analogRead(A0));
  Serial.println("Binary Guessing Game! Look at the LEDs and type the decimal number.");
}

void loop() {
  answer = random(???, ???);          // What range do you need?
  showBinary(answer);
  Serial.println("What number am I showing?");

  while (??? == 0) {                  // What condition keeps you waiting?
    // waiting for input...
  }

  int guess = Serial.parseInt();

  if (??? == ???) {                   // What are you comparing?
    Serial.print("Correct! The number was ");
    Serial.println(???);
  } else {
    Serial.print("Wrong! The number was ");
    Serial.println(???);
  }

  delay(3000);
}
```

---

### Troubleshooting This Task

| Problem | Likely Cause |
|---|---|
| Serial Monitor shows nothing | Check `Serial.begin(9600)` is in `setup()` and monitor is set to 9600 |
| Serial Monitor shows garbage text | Baud rate mismatch — both must be 9600 |
| LEDs don't change between rounds | `showBinary()` not being called, or `digitalWrite` lines missing |
| Every guess says "Wrong" | Check what `Serial.parseInt()` actually returns — add `Serial.println(guess)` to debug |
| Same numbers every time | Make sure `randomSeed(analogRead(A0))` is in `setup()` |

---

### Expected Output (once working)

```
Binary Guessing Game! Look at the LEDs and type the decimal number.
What number am I showing?
11
Correct! The number was 11
What number am I showing?
5
Wrong! The number was 9
```
