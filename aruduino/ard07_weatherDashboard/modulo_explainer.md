# Understanding Modulo (`%`)

A teacher/student reference for the rotation trick used in Lesson 07.

---

## The Short Version

Modulo is one of those things that clicks instantly once you see it, but the textbook definition ("remainder after division") makes it sound more abstract than it really is.

**The simplest way to think about it: modulo = the remainder.**

When you divide 7 by 3, you get 2 with a remainder of 1.

- `7 / 3 = 2` (regular division, ignoring the remainder)
- `7 % 3 = 1` (modulo — gives you JUST the remainder)

That's it. `%` is just "divide and tell me what's left over."

---

## Why This Is Useful

**The remainder never gets bigger than the divisor.**

Watch what happens when you take `% 3` on a counter that keeps growing:

| i  | i % 3 |
|----|-------|
| 0  | 0     |
| 1  | 1     |
| 2  | 2     |
| 3  | 0     |
| 4  | 1     |
| 5  | 2     |
| 6  | 0     |
| 7  | 1     |
| 8  | 2     |

See the pattern on the right? `0, 1, 2, 0, 1, 2, 0, 1, 2...` — it cycles forever. The left column grows without limit, but the right column **can never be 3 or bigger**, because if it were, you could divide out one more 3. The remainder is always smaller than what you're dividing by.

**That's the whole trick.** We want `currentCity` to stay in the range `0, 1, 2` so it keeps landing on a valid spot in our array — and `% 3` is a math operation that guarantees that.

---

## The Clock Analogy

*(This is the one that usually sticks.)*

A clock is modulo 12. It goes `1, 2, 3, ... 11, 12, 1, 2, 3...` — when you hit the top, you wrap around.

If it's 10 o'clock and someone says "meet me in 5 hours," you don't say "15 o'clock." You say **3 o'clock**. Because `15 % 12 = 3`.

Your brain already does modulo every time you read a clock. We're just making it explicit in code.

Days of the week work the same way — it's `% 7`. Months are `% 12`. Anything that cycles is modulo.

---

## Back to Our Code

```cpp
currentCity = (currentCity + 1) % numCities;
```

Read it out loud in plain English: **"Add one to the current city. Then, if that makes it too big, wrap it back to zero."**

Trace it with `numCities = 3`:

- `currentCity` starts at 0
- `(0 + 1) % 3` → `1 % 3` → **1** ✓ (KJFK is next)
- `(1 + 1) % 3` → `2 % 3` → **2** ✓ (KLAX is next)
- `(2 + 1) % 3` → `3 % 3` → **0** ✓ (wraps back — KCAK again!)

The magic happens on that third line. `3 % 3 = 0` because 3 divides into 3 exactly once with nothing left over. So the moment we'd go past the end of the array, modulo snaps us back to the beginning — automatically, no if-statement needed.

---

## Why the Parentheses Matter

```cpp
(currentCity + 1) % numCities   // ✓ correct
currentCity + 1 % numCities     // ✗ broken
```

Without parens, C computes `1 % numCities` first (which is just 1 if `numCities > 1`), then adds `currentCity`. So you end up with `currentCity + 1` forever, no wrap. Silent bug.

Say it like this: **"Add one FIRST, then modulo."** The parens enforce that order.

---

## The If-Statement Equivalent

```cpp
currentCity = currentCity + 1;
if (currentCity >= numCities) {
    currentCity = 0;
}
```

This does the exact same thing. Increment the counter, and if it went too far, slam it back to 0. The modulo version is just the one-line way to say the same thing. Both are fine — some students find the if-statement version easier to read at first, and that's totally valid.

---

## The One-Sentence Version

> Modulo (`%`) gives you the remainder after division, and the remainder always stays smaller than what you divided by — which is exactly what you want when you're cycling through a list.

---

## Bonus: Other Cycle Sizes

Same pattern, different wrap point:

### `% 4` (4-city rotation)

| i  | i % 4 |
|----|-------|
| 0  | 0     |
| 1  | 1     |
| 2  | 2     |
| 3  | 3     |
| 4  | 0     |
| 5  | 1     |
| 6  | 2     |
| 7  | 3     |

Cycle: `0, 1, 2, 3, 0, 1, 2, 3, ...`

### `% 7` (days of the week)

| i  | i % 7 |
|----|-------|
| 0  | 0     |
| 1  | 1     |
| 6  | 6     |
| 7  | 0     |
| 8  | 1     |
| 14 | 0     |

Cycle: `0, 1, 2, 3, 4, 5, 6, 0, 1, 2, ...`

### `% 2` (alternating — the on/off trick)

| i  | i % 2 |
|----|-------|
| 0  | 0     |
| 1  | 1     |
| 2  | 0     |
| 3  | 1     |
| 4  | 0     |

Cycle: `0, 1, 0, 1, ...` — useful for blinking LEDs, alternating colors, or anything that toggles.

---

## Other Places You'll See Modulo

- **Even or odd?** `n % 2 == 0` is true when `n` is even, false when it's odd.
- **Every Nth time?** `if (count % 10 == 0)` fires once every 10 iterations — good for "print a status update every 10 loops."
- **Pair up students?** `student[i % 2]` alternates between two groups.
- **Wrap a value to a range?** `degrees % 360` keeps an angle between 0 and 359.

Once you spot the pattern, you'll see it everywhere — anytime something needs to stay inside a fixed range while a counter grows, modulo is the tool.
