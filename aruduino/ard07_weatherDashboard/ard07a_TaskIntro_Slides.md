---
marp: true
theme: default
paginate: true
---

# Task: Multi-City Weather Tour

**Programming — Medina County Career Center**

Lesson 07a

---

## The Goal

Your weather dashboard currently shows **one city** (KCAK — Akron-Canton).

Today you're going to make it **cycle through multiple cities**, showing each one's weather in turn before moving to the next.

```
KCAK 47F Cloudy  →  KJFK 52F Sunny  →  KLAX 68F Clear  →  (back to KCAK)
```

The good news: you only need to edit **one file** — `WeatherAPI.ino`.

---

## The Setup

To hold a list of cities, we use an **array**:

```cpp
String cities[] = {"KCAK", "KJFK", "KLAX"};
int numCities = 3;
int currentCity = 0;   // which city we're on
```

To pick the current city: `cities[currentCity]`

That part's easy. The tricky part is: **how do we advance `currentCity` so it cycles back to 0 after the last city?**

---

## The Naive Approach

The obvious idea:

```cpp
currentCity = currentCity + 1;
```

**What happens after three fetches?**

| Fetch | currentCity | cities[currentCity] |
|-------|-------------|---------------------|
| 1st   | 0           | KCAK ✓              |
| 2nd   | 1           | KJFK ✓              |
| 3rd   | 2           | KLAX ✓              |
| 4th   | **3**       | 💥 out of bounds    |

`cities[3]` doesn't exist. The Arduino reads random memory. Program crashes or shows garbage.

---

## What We Need

A way to make the counter **wrap around** back to 0 when it hits the end.

Before: `0, 1, 2, 3, 4, 5, 6, 7, ...` (keeps growing forever)

After: `0, 1, 2, 0, 1, 2, 0, 1, 2, ...` (cycles within range)

There's a math operator built exactly for this job.

---

## Meet the Modulo Operator: `%`

`%` means: **divide and give me the remainder.**

- `7 / 3 = 2` (regular division)
- `7 % 3 = 1` (modulo — just the leftover)

**The key insight:** the remainder can never be bigger than what you're dividing by.

If you do `% 3`, the answer is always `0`, `1`, or `2`. It's **mathematically impossible** to get 3 or bigger.

That's exactly the range we want for a 3-city array.

---

## Modulo in Action: `i % 3`

| i  | i % 3 |
|----|-------|
| 0  | **0** |
| 1  | **1** |
| 2  | **2** |
| 3  | **0** ← wrap!  |
| 4  | **1** |
| 5  | **2** |
| 6  | **0** ← wrap!  |
| 7  | **1** |

See the cycle `0, 1, 2, 0, 1, 2, ...`? That's the pattern we need.

---

## Clock Analogy

A clock is modulo 12. It counts `1, 2, 3, ... 11, 12, 1, 2, ...` — when it hits the top, it wraps.

If it's 10 o'clock and someone says "meet me in 5 hours," you say **3 o'clock**, not "15 o'clock."

`15 % 12 = 3` ✓

Your brain already does modulo every time you read a clock. We're just making it explicit in code.

---

## Worked Example: Traffic Light 🚦

Imagine a traffic light that cycles red → yellow → green → red:

```cpp
int state = 0;        // 0 = red, 1 = yellow, 2 = green

void nextLight() {
    state = (state + 1) % 3;   // advance, wrap at 3
    if (state == 0) setRed();
    if (state == 1) setYellow();
    if (state == 2) setGreen();
}
```

Trace `state` over 6 calls: `1 → 2 → 0 → 1 → 2 → 0` ✓

Cycles forever. No `if (state > 2)` check needed.

---

## Why the Parentheses Matter

```cpp
state = (state + 1) % 3;   // ✓ correct
state = state + 1 % 3;     // ✗ silent bug
```

Without parens, C computes `1 % 3` first (= 1), then adds `state`. You end up with `state + 1` forever — never wraps.

**Say it out loud: "Add one FIRST, then modulo."**

---

## The Alternative: If-Statement

Modulo is elegant, but you can also do it the long way:

```cpp
state = state + 1;
if (state >= 3) {
    state = 0;
}
```

Same result. Both work. Use whichever makes sense to you.

Modulo is just the **one-line version** of this pattern.

---

## Your Turn

You now know:

- How to advance a counter through a fixed range (`% N`)
- Why it works (remainder can never hit N)
- Two ways to write it (modulo OR if-statement)

Your task: apply this pattern to cycle `currentCity` through your cities array.

**Hints in the task doc. Modulo explainer in the folder if you want more examples.**

Go build a world-tour weather dashboard. 🌎

