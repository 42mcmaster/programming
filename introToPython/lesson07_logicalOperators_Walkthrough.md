# Lesson 07 — Logical Operators: `and`, `or`, `not` (Teacher Walkthrough)

> **Teacher-only file.** ~20-minute script.

**Student deliverable:** `lesson07_logicalOperators_Task.ipynb`
**ODE standards touched:** 5.3.1 (boolean logic), 5.3.4 (compound conditions), 5.3.5.

---

## Learning Objectives

1. Combine two or more comparisons using `and` / `or`.
2. Flip a boolean using `not`.
3. Understand that Python uses the **words** `and`, `or`, `not` — not symbols.
4. Read a compound condition left to right and predict its result.

---

## Section 1 — Why we need this (3 minutes)

**Say:**

> "Last lesson you did an exercise where someone was old enough to drive AND had a license. You had to write a nested `if` inside another `if`. That works, but it's clunky. Today we learn a cleaner way: **combine** two conditions into one using a logical operator."

Show the before/after:

```python
# Before — nested
if age >= 16:
    if hasLicense:
        print("Can drive")
```

```python
# After — combined
if age >= 16 and hasLicense:
    print("Can drive")
```

> "Cleaner, reads like English, one level of indentation instead of two."

---

## Section 2 — The three operators (8 minutes)

Put this table on the board:

| Operator | Meaning | True when... |
|---|---|---|
| `and` | BOTH conditions are True | both sides are True |
| `or` | AT LEAST ONE condition is True | either side (or both) is True |
| `not` | flips True to False and vice versa | the thing it's in front of is False |

**Key syntax note:**

> "These are **words**, not symbols. Python uses the actual English words: `and`, `or`, `not`. Lowercase."

### 2a. `and` — both must be True

```python
age = 17
hasLicense = True

print(age >= 16 and hasLicense)            # True — both are True
print(age >= 18 and hasLicense)            # False — age >= 18 is False
print(age >= 16 and not hasLicense)        # False — hasLicense side flipped
```

**Say:**

> "Read `and` as 'both.' Both sides have to be True for the whole thing to be True. If either side is False, the whole thing is False."

### 2b. `or` — either (or both) can be True

```python
isWeekend = False
isHoliday = True

print(isWeekend or isHoliday)              # True — isHoliday is True
print(False or False)                      # False — neither
print(True or True)                        # True — both (still fine)
```

**Say:**

> "Read `or` as 'either.' As long as at least one side is True, the whole thing is True. The only way `or` is False is when BOTH sides are False."

### 2c. `not` — flips

```python
isRaining = False

print(not isRaining)                       # True
print(not True)                            # False
print(not (age >= 18))                     # True for a 17-year-old
```

**Say:**

> "`not` reverses a boolean. True becomes False; False becomes True. Put it in front of a comparison or a bool variable."

---

## Section 3 — Truth tables (quick reference, 2 minutes)

Put these on the board for students to copy:

### `and`

| A | B | A and B |
|---|---|---|
| T | T | **T** |
| T | F | F |
| F | T | F |
| F | F | F |

### `or`

| A | B | A or B |
|---|---|---|
| T | T | **T** |
| T | F | **T** |
| F | T | **T** |
| F | F | F |

### `not`

| A | not A |
|---|---|
| T | F |
| F | T |

> "Memorize `and`: only true when both are true. `or`: only false when both are false. The middle cases are the ones people mess up."

---

## Section 4 — Combining more than two (3 minutes)

You can chain any number of `and`s, `or`s, and `not`s together.

```python
age = 17
hasLicense = True
hasCar = True
hasInsurance = False

canDrive = age >= 16 and hasLicense and hasCar and hasInsurance
print(canDrive)                    # False — missing insurance
```

### Mixing `and` and `or`

> "When you mix `and` and `or`, **use parentheses** to make the order explicit. Don't rely on operator precedence — it's clearer, and you won't guess wrong."

```python
# A weekend OR a holiday AND you're off
isWeekend = False
isHoliday = True
isOffSchool = True

# Clear with parens
canSleepIn = (isWeekend or isHoliday) and isOffSchool
print(canSleepIn)
```

---

## Section 5 — Using in `if` statements (3 minutes)

Now we weave it into what we learned in Lesson 06.

```python
temp = int(input("Temperature in °F? "))
isRaining = input("Is it raining (yes/no)? ").lower() == "yes"

if temp >= 70 and not isRaining:
    print("Perfect — go outside!")
elif temp >= 70 and isRaining:
    print("Warm but wet. Bring a jacket.")
elif temp < 70 and isRaining:
    print("Cold and rainy. Stay in.")
else:
    print("Cold but dry. Bundle up and go.")
```

Run it with a few combinations so students can see each branch fire.

### Range checks with `and`

Very common pattern — checking that a number is in a range:

```python
score = int(input("Test score: "))

if score >= 0 and score <= 100:
    print(f"Your score of {score} is a valid test score.")
else:
    print("That score is outside the valid 0-100 range.")
```

> "Python also lets you write `0 <= score <= 100` as a shortcut for that. Both work."

---

## Section 6 — Common Mistakes (1 minute)

**Mistake 1: Using symbols instead of words.**

```python
if age >= 16 && hasLicense:        # SyntaxError — && is not Python
if age >= 16 and hasLicense:       # Correct
```

> "Python uses the English words. Not `&&`, not `||`, not `!`. Just `and`, `or`, `not`."

**Mistake 2: Ambiguous English that doesn't translate to code.**

```python
# Wrong — what it looks like in English
if color == "red" or "blue":
    ...

# What you actually mean
if color == "red" or color == "blue":
    ...
```

> "`\"blue\"` by itself isn't a comparison — it's just the string `\"blue\"`. You have to write out the full comparison on both sides of `or`."

**Mistake 3: `and` when you meant `or`.**

```python
# Check if day is Sat or Sun:
if day == "Saturday" and day == "Sunday":    # Impossible — never True
    print("Weekend!")

if day == "Saturday" or day == "Sunday":     # Correct
    print("Weekend!")
```

---

## Section 7 — Quick Recap (1 minute)

Ask:

1. "In Python, what do you type for `and`, `or`, `not`?"
2. "`True and False` — what's the result?"
3. "`True or False` — what's the result?"
4. "When you mix `and` and `or`, what should you always add to make it clear?" (parentheses)

Hand off:

> "Open `lesson07_logicalOperators_Task.ipynb`."

---

## Vocabulary introduced today

- **Logical operator** — `and`, `or`, `not` — combines or flips booleans.
- **Compound condition** — a condition made of two or more comparisons joined by `and`/`or`.
- **Truth table** — a small chart showing every possible input combination and its result.
- **Short-circuit evaluation** (bonus) — Python stops checking as soon as the answer is determined. (`True or anything` is True without checking `anything`.) Nice to mention but not required.
