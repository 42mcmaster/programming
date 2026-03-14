# ard_lesson05 — TEACHER SOLUTIONS

**Medina County Career Center — For Instructor Use**

---

## Solution 1: 4-LED Binary Counter (0–15)

Complete working sketch. Students were given numbers 0–4 and asked to complete 5–15 on their own.

```cpp
// ============================================================
// ard_lesson05 — Binary Counter (0 to 15)
// Pins 13, 12, 11, 10 represent the 8s, 4s, 2s, 1s place
// Each LED: long leg → pin, short leg → 1KΩ resistor → GND
// ============================================================

void setup() {
  pinMode(13, OUTPUT);  // 8s place (leftmost LED)
  pinMode(12, OUTPUT);  // 4s place
  pinMode(11, OUTPUT);  // 2s place
  pinMode(10, OUTPUT);  // 1s place (rightmost LED)
}

void loop() {

  // 0 — 0000
  digitalWrite(13, LOW);  digitalWrite(12, LOW);  digitalWrite(11, LOW);  digitalWrite(10, LOW);
  delay(500);

  // 1 — 0001
  digitalWrite(13, LOW);  digitalWrite(12, LOW);  digitalWrite(11, LOW);  digitalWrite(10, HIGH);
  delay(500);

  // 2 — 0010
  digitalWrite(13, LOW);  digitalWrite(12, LOW);  digitalWrite(11, HIGH); digitalWrite(10, LOW);
  delay(500);

  // 3 — 0011
  digitalWrite(13, LOW);  digitalWrite(12, LOW);  digitalWrite(11, HIGH); digitalWrite(10, HIGH);
  delay(500);

  // 4 — 0100
  digitalWrite(13, LOW);  digitalWrite(12, HIGH); digitalWrite(11, LOW);  digitalWrite(10, LOW);
  delay(500);

  // 5 — 0101
  digitalWrite(13, LOW);  digitalWrite(12, HIGH); digitalWrite(11, LOW);  digitalWrite(10, HIGH);
  delay(500);

  // 6 — 0110
  digitalWrite(13, LOW);  digitalWrite(12, HIGH); digitalWrite(11, HIGH); digitalWrite(10, LOW);
  delay(500);

  // 7 — 0111
  digitalWrite(13, LOW);  digitalWrite(12, HIGH); digitalWrite(11, HIGH); digitalWrite(10, HIGH);
  delay(500);

  // 8 — 1000
  digitalWrite(13, HIGH); digitalWrite(12, LOW);  digitalWrite(11, LOW);  digitalWrite(10, LOW);
  delay(500);

  // 9 — 1001
  digitalWrite(13, HIGH); digitalWrite(12, LOW);  digitalWrite(11, LOW);  digitalWrite(10, HIGH);
  delay(500);

  // 10 — 1010
  digitalWrite(13, HIGH); digitalWrite(12, LOW);  digitalWrite(11, HIGH); digitalWrite(10, LOW);
  delay(500);

  // 11 — 1011
  digitalWrite(13, HIGH); digitalWrite(12, LOW);  digitalWrite(11, HIGH); digitalWrite(10, HIGH);
  delay(500);

  // 12 — 1100
  digitalWrite(13, HIGH); digitalWrite(12, HIGH); digitalWrite(11, LOW);  digitalWrite(10, LOW);
  delay(500);

  // 13 — 1101
  digitalWrite(13, HIGH); digitalWrite(12, HIGH); digitalWrite(11, LOW);  digitalWrite(10, HIGH);
  delay(500);

  // 14 — 1110
  digitalWrite(13, HIGH); digitalWrite(12, HIGH); digitalWrite(11, HIGH); digitalWrite(10, LOW);
  delay(500);

  // 15 — 1111
  digitalWrite(13, HIGH); digitalWrite(12, HIGH); digitalWrite(11, HIGH); digitalWrite(10, HIGH);
  delay(500);

  // Pause before restarting at 0
  delay(2000);
}
```

---

### Grading Notes — Binary Counter

**Full credit:** All 16 states (0–15) display correctly, 500ms per step, 2-second pause at end before repeating.

**Common student errors to watch for:**
- Missing the `delay(2000)` at the end — counter restarts immediately and the 15→0 transition is invisible
- Swapped HIGH/LOW on a row — usually shows up as one number in the middle of the count looking wrong; have them compare that row against the binary table
- Pin 13 and Pin 10 swapped — the entire counter will look mirrored (counts right-to-left instead of left-to-right). Not wrong per se, but worth flagging
- Missing semicolons causing compile errors — remind them the error message includes a line number

---
---

## Solution 2: Binary Guessing Game

Complete working sketch with additional comments explaining the new concepts introduced (custom functions, bitwise AND, Serial input).

```cpp
// ============================================================
// ard_lesson05 — Binary Guessing Game
// Arduino picks a random number 0-15, shows it in binary on
// the LEDs, and waits for the player to guess via Serial Monitor.
//
// New concepts in this sketch:
//   - Custom functions (showBinary)
//   - Bitwise AND operator (&) to check individual bits
//   - Serial.begin / Serial.println / Serial.parseInt
//   - random() and randomSeed()
// ============================================================

int answer = 0;  // Stores the randomly chosen number each round

// ------------------------------------------------------------
// showBinary(num) — custom function
// Takes an integer 0-15 and lights up the LEDs to match its
// binary representation. Called from loop() each round.
//
// The & (bitwise AND) operator checks whether a specific bit
// is set in the number:
//   num & 8  → is the 8s bit ON?  (e.g. 11 & 8 = 8, truthy)
//   num & 4  → is the 4s bit ON?
//   num & 2  → is the 2s bit ON?
//   num & 1  → is the 1s bit ON?
// The ? HIGH : LOW is a shorthand if/else — if true, HIGH, else LOW.
// ------------------------------------------------------------
void showBinary(int num) {
  digitalWrite(13, (num & 8) ? HIGH : LOW);   // 8s place
  digitalWrite(12, (num & 4) ? HIGH : LOW);   // 4s place
  digitalWrite(11, (num & 2) ? HIGH : LOW);   // 2s place
  digitalWrite(10, (num & 1) ? HIGH : LOW);   // 1s place
}

void setup() {
  pinMode(13, OUTPUT);
  pinMode(12, OUTPUT);
  pinMode(11, OUTPUT);
  pinMode(10, OUTPUT);

  Serial.begin(9600);  // Open serial communication at 9600 baud
                       // Must match the baud rate in Serial Monitor

  // randomSeed() makes random() produce different sequences each run.
  // analogRead(A0) reads electrical noise on an unconnected pin —
  // it's different every time, which makes a good random seed.
  randomSeed(analogRead(A0));

  Serial.println("Binary Guessing Game!");
  Serial.println("Look at the LEDs, convert binary to decimal, and type your answer.");
  Serial.println("----------------------------------------------");
}

void loop() {
  // Pick a new random number between 0 and 15 (16 is excluded)
  answer = random(0, 16);

  // Show it on the LEDs
  showBinary(answer);

  Serial.println("What number am I showing?");

  // Wait here until the player types something in Serial Monitor
  while (Serial.available() == 0) {
    // Serial.available() returns how many bytes are waiting to be read.
    // When it's 0, nothing has been typed yet — keep waiting.
  }

  // Read the number the player typed
  int guess = Serial.parseInt();

  // Check the guess and respond
  if (guess == answer) {
    Serial.print("Correct! The number was ");
    Serial.println(answer);
  } else {
    Serial.print("Wrong! The number was ");
    Serial.println(answer);
  }

  Serial.println();  // Blank line between rounds for readability

  // Pause before next round so the player can read the result
  delay(3000);
}
```

---

### Grading Notes — Guessing Game

**Full credit:** Sketch compiles and runs, LEDs update each round, Serial Monitor shows correct/wrong feedback with the actual answer, game loops continuously.

**Common student errors to watch for:**
- `Serial.begin()` missing or wrong baud — Serial Monitor shows garbage characters or nothing. Fix: confirm `Serial.begin(9600)` is in `setup()` and the monitor is set to 9600.
- Student removes `showBinary()` and writes out 4 `digitalWrite` lines in loop instead — technically works, give credit, but use it as a teaching moment about why functions exist
- `while (Serial.available() == 0)` loop removed — sketch won't wait for input and will just rapidly cycle through random numbers. Common if students try to "simplify" the code without understanding what that line does
- `Serial.parseInt()` replaced with `Serial.read()` — `read()` returns the ASCII character code, not the number. Typing "7" sends the byte value 55, so every guess appears wrong. Worth explaining the difference between a character and an integer.

---

### Key Concepts to Reinforce in Discussion

**Custom functions:** `showBinary()` is defined above `setup()` and called inside `loop()`. Ask students: what would the code look like if we didn't have this function? (4 lines × 16 numbers = 64 lines just for the counter portion.) Functions aren't just convenient — they make code readable and maintainable.

**Bitwise AND:** The `&` operator is doing binary math directly. `11 & 8` in binary is `1011 & 1000 = 1000`, which is 8 — nonzero, so truthy. This is exactly the binary concepts from lesson 5 showing up in real code. Good opportunity to walk through one example on the board.

**The ternary operator:** `(condition) ? valueIfTrue : valueIfFalse` is shorthand for a simple if/else. Not required knowledge at this level, but Track B students who ask about it are ready for it.
