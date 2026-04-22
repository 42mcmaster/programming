# Lesson 08 — `for` Loops and `range()` (Teacher Walkthrough)

> **Teacher-only file.** ~20-minute script.

**Student deliverable:** `lesson08_forLoopsAndRange_Task.ipynb`
**ODE standards touched:** 5.3.6 (repetition/iteration), 5.4.2, 5.5.6 (algorithm patterns).

---

## Learning Objectives

1. Write a `for` loop that repeats a block of code a fixed number of times.
2. Use the three forms of `range()`: `range(n)`, `range(start, stop)`, `range(start, stop, step)`.
3. Loop through each character of a string.
4. Use the **accumulator pattern** to compute a running total.

---

## Section 1 — Why loops? (2 minutes)

**Say:**

> "Imagine I want you to print `Hello` ten times. You could write ten `print` statements. Or you could use a **loop**."

Show the repetitive version:

```python
print("Hello")
print("Hello")
print("Hello")
print("Hello")
print("Hello")
```

Then the loop version:

```python
for i in range(5):
    print("Hello")
```

> "Same result. Five lines of typing turned into two. More importantly, if I ask you to do it 500 times, the loop is unchanged — just change the 5 to a 500."

---

## Section 2 — Basic `for` with `range()` (5 minutes)

### The anatomy

Put this on the board:

```python
for VARIABLE in range(COUNT):
    <body — indented code that repeats>
```

- `for` — the keyword.
- `VARIABLE` — a name you pick. It holds the current loop value each time around. Conventionally `i` (short for index) for counting loops.
- `in range(COUNT)` — how many times to loop.
- The colon `:` at the end.
- The body is **indented 4 spaces**.

Demo:

```python
for i in range(5):
    print("i =", i)
```

**Expected output:**

```
i = 0
i = 1
i = 2
i = 3
i = 4
```

**Point out:**

> "Notice the numbers: 0, 1, 2, 3, 4. Python starts counting at **zero**. `range(5)` gives you five numbers — 0 through 4. It does NOT include 5. That's called **exclusive upper bound** — the stop value is where the range stops, but doesn't include."

---

## Section 3 — Three forms of `range()` (5 minutes)

### Form 1 — `range(stop)`

> "Numbers from 0 up to (but not including) stop."

```python
for i in range(5):
    print(i)
# Prints 0, 1, 2, 3, 4
```

### Form 2 — `range(start, stop)`

> "Numbers from start up to (but not including) stop."

```python
for i in range(1, 6):
    print(i)
# Prints 1, 2, 3, 4, 5
```

> "Notice — to count 1 through 5, you write `range(1, 6)`. The 6 is exclusive."

### Form 3 — `range(start, stop, step)`

> "Start, stop, and how much to jump each time."

```python
for i in range(0, 20, 2):
    print(i)
# Prints 0, 2, 4, 6, 8, 10, 12, 14, 16, 18
```

**Countdown — negative step:**

```python
for i in range(10, 0, -1):
    print(i)
# Prints 10, 9, 8, 7, 6, 5, 4, 3, 2, 1
```

> "Negative step counts down. Handy for countdowns."

---

## Section 4 — Looping over a string (2 minutes)

**Say:**

> "`for` loops aren't limited to `range()`. You can loop over any **sequence** — and strings are sequences. Each iteration, the variable gets the next character."

```python
word = "Python"
for letter in word:
    print(letter)
```

**Expected output:**

```
P
y
t
h
o
n
```

> "Six iterations, one per character. We'll come back to strings and lists in future lessons."

---

## Section 5 — The accumulator pattern (4 minutes)

**This is the big idea of the lesson. Write it in big letters on the board.**

> **Accumulator pattern:** start with a variable at 0, then add to it inside a loop.

```python
total = 0                    # Start fresh
for i in range(1, 6):        # 1, 2, 3, 4, 5
    total = total + i        # Add to total each time
print(total)                 # 15
```

Walk through the trace on the board:

| Iteration | i | total before | total after |
|---|---|---|---|
| 1 | 1 | 0 | 1 |
| 2 | 2 | 1 | 3 |
| 3 | 3 | 3 | 6 |
| 4 | 4 | 6 | 10 |
| 5 | 5 | 10 | 15 |

**Say:**

> "The word **accumulator** means 'the thing that keeps accumulating values.' The pattern is: (1) set a starting value **before** the loop, (2) update it **inside** the loop."

Same thing with the shortcut operator:

```python
total = 0
for i in range(1, 6):
    total += i
print(total)    # 15
```

### Common uses of the accumulator pattern

**Sum of N numbers from the user:**

```python
total = 0
for i in range(3):
    num = float(input("Enter a number: "))
    total += num
print(f"Sum: {total}")
```

**Counting things:**

```python
count = 0
for letter in "Mississippi":
    if letter == "s":
        count += 1
print(f"There are {count} s's.")
```

**Product (running multiplication — start at 1, not 0):**

```python
product = 1
for i in range(1, 6):
    product *= i
print(product)     # 120 (which is 5!)
```

> "Heads up: if you're multiplying, start at 1, not 0. Starting at 0 would always give 0."

---

## Section 6 — Live build (2 minutes)

Build together:

```python
# Program: Average of N numbers
# Purpose: Get 5 numbers and print their average.

total = 0
count = 5

for i in range(count):
    num = float(input(f"Enter number #{i + 1}: "))
    total += num

average = total / count
print(f"The average of those {count} numbers is {average:.2f}")
```

> "Look at `f\"#{i + 1}\"` — I'm shifting from 0-based to 1-based just for display. Users prefer to see #1, #2, #3..."

---

## Section 7 — Common Mistakes (2 minutes)

**Mistake 1: Forgetting the range is exclusive on the right.**

```python
for i in range(1, 5):      # 1, 2, 3, 4 — does NOT include 5!
    print(i)
```

> "If you want to include the last number, add 1 to the stop value. `range(1, 6)` if you want 1 through 5."

**Mistake 2: Resetting the accumulator inside the loop.**

```python
for i in range(5):
    total = 0          # BUG — this resets every iteration!
    total += i
print(total)           # 4, not 10
```

> "The accumulator must be set **before** the loop. Not inside."

**Mistake 3: Off-by-one errors.**

```python
# Print 1 through 10
for i in range(1, 10):     # Only goes 1–9! Bug.
    print(i)

for i in range(1, 11):     # Correct: 1–10
    print(i)
```

**Mistake 4: Modifying the loop variable by hand.**

> "Don't manually change `i` inside the loop — Python controls it. If you want to skip, use `continue` (next lesson)."

---

## Section 8 — Quick Recap (1 minute)

Ask:

1. "What does `range(5)` give you?" (0, 1, 2, 3, 4)
2. "What does `range(1, 6)` give you?" (1, 2, 3, 4, 5)
3. "How do you count down from 10 to 1?" (`range(10, 0, -1)`)
4. "What are the two steps of the accumulator pattern?" (start the variable before the loop, update it inside)

Hand off:

> "Open `lesson08_forLoopsAndRange_Task.ipynb`."

---

## Vocabulary introduced today

- **Loop** — code that repeats.
- **for loop** — repeats a set number of times, once per item in a sequence.
- **range()** — a function that generates a sequence of integers.
- **Iteration** — one run through a loop body.
- **Accumulator** — a variable that builds up a value (total, count, product) across iterations.
- **Exclusive upper bound** — `range(stop)` does NOT include `stop` itself.
- **Off-by-one error** — getting the endpoint wrong by one; very common in loop code.
