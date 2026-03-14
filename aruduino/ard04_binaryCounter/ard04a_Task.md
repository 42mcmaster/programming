# ard04a — Stoplight Challenge

**Programming — Medina County Career Center**
**Standards: ODE 5.2.1, 5.4.2, 5.4.3, 5.4.6, 5.5.5**

---

## Before You Start

You've built the 4-LED binary counter and watched it count from 0 to 15. Now you're going to rewire those LEDs into something from the real world — a traffic stoplight. Then you'll build a full intersection with two stoplights that work together.

**Swap your LED colors.** Pull out your red-only LEDs and replace them with the right colors from your kit. You'll need **red**, **yellow**, and **green** LEDs.

---

## Task 1: Single Stoplight

### Rewire Your Circuit

Remove one of your 4 LEDs. Wire the remaining 3 with these colors and pins:

| LED Color | Arduino Pin | Role |
|---|---|---|
| Red | Pin 13 | Stop |
| Yellow | Pin 12 | Caution |
| Green | Pin 11 | Go |

Same wiring pattern as before: pin → LED long leg → LED short leg → resistor → GND rail. Each LED keeps its own resistor.

### The Stoplight Sequence

A real stoplight follows this pattern:

| State | Red | Yellow | Green | Duration |
|---|---|---|---|---|
| **Go** | OFF | OFF | ON | 5 seconds |
| **Caution** | OFF | ON | OFF | 2 seconds |
| **Stop** | ON | OFF | OFF | 5 seconds |

Then it repeats: Go → Caution → Stop → Go → Caution → Stop → ...

### Write the Code

**Your starter code:**

```cpp
int redPin = 13;
int yellowPin = 12;
int greenPin = 11;

void setup() {
    pinMode(redPin, OUTPUT);
    pinMode(yellowPin, OUTPUT);
    pinMode(greenPin, OUTPUT);
    Serial.begin(9600);
    Serial.println("Stoplight running");
}

void loop() {
    // GREEN - Go
    // Turn on green, turn off red and yellow
    // Print "GREEN - Go" to Serial Monitor
    // Delay 5 seconds

    // YELLOW - Caution
    // Turn on yellow, turn off green and red
    // Print "YELLOW - Caution"
    // Delay 2 seconds

    // RED - Stop
    // Turn on red, turn off yellow and green
    // Print "RED - Stop"
    // Delay 5 seconds
}
```

Upload and verify. You should see the classic stoplight pattern: green for 5 seconds, yellow for 2, red for 5, repeat.

---

## Task 2: Intersection — Two Stoplights

Now here's the real challenge. At an intersection, when one direction has a green light, the other direction **must** have a red light. They have to work together.

### Add 3 More LEDs

Wire a second set of 3 LEDs for the cross street:

| LED Color | Arduino Pin | Role |
|---|---|---|
| Red (Street 2) | Pin 10 | Stop |
| Yellow (Street 2) | Pin 9 | Caution |
| Green (Street 2) | Pin 8 | Go |

That's 6 LEDs total, 6 resistors, all sharing the GND rail.

### The Intersection Sequence

Think about what happens at a real intersection:

| Phase | Street 1 | Street 2 | Duration |
|---|---|---|---|
| 1 | **GREEN** | **RED** | 5 seconds |
| 2 | **YELLOW** | **RED** | 2 seconds |
| 3 | **RED** | **RED** | 1 second |
| 4 | **RED** | **GREEN** | 5 seconds |
| 5 | **RED** | **YELLOW** | 2 seconds |
| 6 | **RED** | **RED** | 1 second |

Notice phase 3 and 6: **both directions are red** for 1 second. This is the safety pause that real intersections use so cars in the intersection can clear before the other direction gets a green.

### Write the Code

**Your starter code:**

```cpp
// Street 1
int red1 = 13;
int yellow1 = 12;
int green1 = 11;

// Street 2
int red2 = 10;
int yellow2 = 9;
int green2 = 8;

void setup() {
    for (int pin = 8; pin <= 13; pin++) {
        pinMode(pin, OUTPUT);
    }
    Serial.begin(9600);
    Serial.println("Intersection running");
}

// Helper function: set all 6 LEDs at once
void setLights(int r1, int y1, int g1, int r2, int y2, int g2) {
    digitalWrite(red1, r1);
    digitalWrite(yellow1, y1);
    digitalWrite(green1, g1);
    digitalWrite(red2, r2);
    digitalWrite(yellow2, y2);
    digitalWrite(green2, g2);
}

void loop() {
    // Phase 1: Street 1 green, Street 2 red
    setLights(LOW, LOW, HIGH, HIGH, LOW, LOW);
    Serial.println("St1: GREEN  |  St2: RED");
    delay(5000);

    // Phase 2: Street 1 yellow, Street 2 red

    // Phase 3: Both red (safety pause)

    // Phase 4: Street 1 red, Street 2 green

    // Phase 5: Street 1 red, Street 2 yellow

    // Phase 6: Both red (safety pause)

}
```

**Notice the `setLights()` helper function.** It takes 6 HIGH/LOW values (one for each LED) so you can set the entire intersection in one line. The order matches: red1, yellow1, green1, red2, yellow2, green2.

### Test It

Watch the full cycle. Verify:
- Both stoplights are never green at the same time
- Yellow always comes between green and red
- There's a brief all-red pause between direction changes
- The Serial Monitor shows the correct phase for each step

---

## Task 3: Add a Feature (Pick One)

Choose **one** of these to add to your intersection:

### Option A: Flashing Red
After 3 full cycles, switch to flashing red on both streets (like a late-night mode). Both red LEDs blink on and off every 1 second, everything else stays off.

### Option B: Turn Signal
Add a 7th LED (any color) on pin 7 that acts as a left-turn arrow. During phase 3 (the all-red safety pause), blink the turn LED 3 times quickly (200ms on, 200ms off) before the cross street gets green.

### Option C: Countdown Timer
Print a countdown to the Serial Monitor during each phase. For example during the 5-second green:
```
St1: GREEN  |  St2: RED  - 5
St1: GREEN  |  St2: RED  - 4
St1: GREEN  |  St2: RED  - 3
St1: GREEN  |  St2: RED  - 2
St1: GREEN  |  St2: RED  - 1
```
**Hint:** Replace each `delay(5000)` with a `for` loop that runs 5 times with `delay(1000)`.

---

## Submission Checklist

- [ ] Task 1: Single stoplight — green → yellow → red cycle works correctly
- [ ] Task 2: Intersection — 6 LEDs, correct phasing, both never green at the same time, all-red safety pause works
- [ ] Task 3: One additional feature implemented and working
- [ ] Serial Monitor shows the current phase for all tasks
- [ ] Code has comments explaining each phase
