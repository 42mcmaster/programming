# Lesson 06 — if / elif / else (Teacher Walkthrough)

> **Teacher-only file.** ~20-minute script.

**Student deliverable:** `lesson06_ifElifElse_Task.ipynb`
**ODE standards touched:** 5.3.1 (boolean logic), 5.3.5 (conditional control), 5.4.2.

---

## Learning Objectives

1. Write a simple `if` statement that runs code only when a condition is True.
2. Add an `else` branch for the false case.
3. Write an `if` / `elif` / `elif` / `else` **ladder** for multiple cases.
4. Use correct Python **indentation** (4 spaces) — the most important rule today.

---

## Section 1 — The `if` statement (4 minutes)

**Say to the class:**

> "Up to now, every line of code we wrote ran, no questions asked. Top to bottom, every single one. Today we're going to give the program a brain. We're going to let it **decide** whether to run certain lines, based on a condition."

Write this on the board:

```python
if <condition>:
    <code to run if the condition is True>
```

**Three pieces of syntax I need you to lock in:**

1. The word `if`
2. A condition that evaluates to `True` or `False`
3. A **colon** `:` at the end of the `if` line
4. The code that runs is **indented** — Python uses indentation (4 spaces) to show which lines are "inside" the if.

Demo:

```python
age = 20

if age >= 18:
    print("You are an adult.")
    print("You can vote.")

print("This line always runs.")
```

**Say:**

> "Look at the indentation. The two `print` lines underneath `if` are indented 4 spaces. That's what tells Python 'these lines only run if the condition is True.' The last `print` line is NOT indented, so it runs no matter what."

Change `age` to 15 and re-run to show the two indented lines get skipped.

### The colon is NOT optional

```python
if age >= 18      # SyntaxError — missing colon
if age >= 18:     # Correct
```

> "Forgetting the colon at the end of the `if` line is the #1 typo. Develop the habit of always typing the colon."

---

## Section 2 — Adding `else` (3 minutes)

**Say:**

> "What if we want to do something different when the condition is False? That's what `else` is for."

```python
age = 15

if age >= 18:
    print("You are an adult.")
else:
    print("You are a minor.")
```

**Rules:**

- `else` has no condition — it catches everything the `if` didn't.
- `else` also needs a colon.
- The code inside `else` is also indented.

### Common use

```python
number = int(input("Enter a number: "))

if number % 2 == 0:
    print(f"{number} is even.")
else:
    print(f"{number} is odd.")
```

> "Using `% 2 == 0` to check for even/odd — remember modulo from Lesson 04. Add this pattern to your mental toolkit."

---

## Section 3 — `elif` — checking multiple cases (6 minutes)

**Say:**

> "Sometimes you have more than two possibilities. For that we use `elif`, which is short for 'else if.' You can chain as many `elif`s as you need."

```python
score = 85

if score >= 90:
    print("A")
elif score >= 80:
    print("B")
elif score >= 70:
    print("C")
elif score >= 60:
    print("D")
else:
    print("F")
```

**Say:**

> "Read that top to bottom. Python checks each condition in order. As soon as it finds one that's True, it runs that block and skips the rest. If nothing matches, the `else` at the bottom catches it."

### Order matters — watch this

```python
score = 95

# Wrong order
if score >= 60:
    print("D")         # THIS WILL PRINT — because 95 >= 60 is True
elif score >= 90:
    print("A")         # Never reached!
```

> "Start with the most specific (or highest/lowest) condition. A common pattern is top-down from highest to lowest when using thresholds."

### Only one branch ever runs

> "Important: in an if/elif/else ladder, **exactly one** branch runs. Python picks the first match and ignores the rest, even if later conditions would also be True. Understanding this saves you from writing redundant code."

---

## Section 4 — Nesting (an if inside an if) (3 minutes)

**Say:**

> "You can put an `if` inside another `if`. We call that **nesting**. Each level of nesting means another level of indentation."

```python
age = 17
hasLicense = True

if age >= 16:
    print("Old enough to drive.")
    if hasLicense:
        print("And you have a license!")
    else:
        print("But you don't have a license yet.")
else:
    print("Too young to drive.")
```

**Cue:**

> "Notice the inner `if` is indented **8 spaces** — two levels. Every `:` opens a new indent block."

Warn gently:

> "Don't go crazy with nesting. Two levels deep is usually enough. If you're four levels in, there's probably a cleaner way, usually with `and`/`or`, which we learn in the next lesson."

---

## Section 5 — Indentation details (2 minutes)

**Say:**

> "Python uses **indentation** to show which lines are 'inside' an if/elif/else. This is not optional and it's not a style choice. Python will crash without it."

| Rule | Why it matters |
|---|---|
| Use **4 spaces** per level (or one Tab, but be consistent) | Pick one and never mix |
| Every line in the same block must be indented the **same amount** | Mismatched indent = IndentationError |
| You can't just stop indenting in the middle of a block | Every line inside the `if` must be indented |

Demo an IndentationError:

```python
if True:
    print("Line 1")
     print("Line 2")    # Extra space — IndentationError
```

> "If you see `IndentationError` or `unexpected indent`, look at your spaces."

---

## Section 6 — Live build (2 minutes)

Build this with the class:

```python
# Program: Letter grade calculator
# Purpose: Ask for a score and print the letter grade.

score = int(input("Enter your test score (0-100): "))

if score >= 90:
    print("Grade: A")
elif score >= 80:
    print("Grade: B")
elif score >= 70:
    print("Grade: C")
elif score >= 60:
    print("Grade: D")
else:
    print("Grade: F")

print("End of grader.")
```

Run it 3 or 4 times with different scores (95, 73, 55, 0, 100).

---

## Section 7 — Common Mistakes (2 minutes)

**Mistake 1: Forgot the colon.**

```python
if score >= 90
    print("A")
```

**Mistake 2: Forgot to indent.**

```python
if score >= 90:
print("A")
```

**Mistake 3: Used `=` instead of `==`.**

```python
if score = 100:         # SyntaxError
if score == 100:        # Correct
```

**Mistake 4: `elif` without a preceding `if`.**

```python
elif score >= 80:       # SyntaxError — elif must follow an if
```

**Mistake 5: Overlapping ladder in wrong order.**

```python
if score >= 60:          # too broad — this catches 95 too
    print("D")
elif score >= 90:
    print("A")           # unreachable
```

---

## Section 8 — Quick Recap (1 minute)

Ask:

1. "What three things must appear on an `if` line?" (the word `if`, a condition, a colon)
2. "What does `elif` stand for?"
3. "How much do you indent each level?" (4 spaces)
4. "In a big if/elif/else ladder, how many branches run?" (exactly one)

Hand off:

> "Open `lesson06_ifElifElse_Task.ipynb`."

---

## Vocabulary introduced today

- **if** — runs code only if a condition is True.
- **else** — catches the case where the `if` condition was False.
- **elif** — short for "else if"; lets you check more conditions in order.
- **Indentation** — the spaces at the start of a line that tell Python which block a line belongs to.
- **Nesting** — putting one `if` inside another.
- **IndentationError** — Python's complaint that your spaces don't match up.
