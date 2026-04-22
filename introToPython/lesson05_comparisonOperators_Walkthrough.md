# Lesson 05 — Comparison Operators (Teacher Walkthrough)

> **Teacher-only file.** ~20-minute script.

**Student deliverable:** `lesson05_comparisonOperators_Task.ipynb`
**ODE standards touched:** 5.3.1 (boolean logic), 5.3.4 (relational operators), 5.4.2.

---

## Learning Objectives

1. Use the six comparison operators: `==`, `!=`, `<`, `>`, `<=`, `>=`.
2. Explain that a comparison always evaluates to `True` or `False`.
3. Store a comparison result in a boolean variable.
4. Avoid the #1 beginner mistake: confusing `=` (assignment) with `==` (comparison).

---

## Section 1 — Comparisons always return a bool (5 minutes)

**Say to the class:**

> "Up until now, when we ran code, the answer was a number or a string. Today we introduce operators that always give you back a **bool** — one of the two values `True` or `False`."

> "A **comparison operator** takes two values, compares them, and answers the question 'is this comparison true?' with a `True` or `False`."

Run these live:

```python
print(5 == 5)
print(5 == 6)
print(7 > 3)
print(7 < 3)
print(10 >= 10)
print(10 <= 9)
```

**Say after each:**

> "Every one of those is answering a yes/no question. The answer is always `True` or `False`. That's it."

---

## Section 2 — The six operators (5 minutes)

Put this table on the board:

| Operator | Meaning | Example | Result |
|---|---|---|---|
| `==` | equal to | `5 == 5` | `True` |
| `!=` | not equal to | `5 != 6` | `True` |
| `<` | less than | `3 < 5` | `True` |
| `>` | greater than | `3 > 5` | `False` |
| `<=` | less than or equal | `5 <= 5` | `True` |
| `>=` | greater than or equal | `5 >= 6` | `False` |

### The BIG rule: `=` vs `==`

**Write this on the board in big letters:**

> `=` assigns. `==` compares.

```python
age = 17      # assignment — puts 17 into the variable age
age == 17     # comparison — asks "is age equal to 17?" — returns True
```

**Say:**

> "Single equals puts a value in a box. Double equals asks a question. Mixing these up is going to cause you pain, so stop and look at it every single time you type it. I am telling you right now, this will be the most common bug you produce."

### `!=` — the not-equal operator

```python
print("cat" != "dog")   # True
print(7 != 7)           # False
```

---

## Section 3 — Storing comparison results in variables (4 minutes)

**Say:**

> "You can save the result of a comparison in a variable, and then use it later. The variable will be a **bool**."

```python
age = 17
isAdult = age >= 18
print(isAdult)          # False
print(type(isAdult))    # <class 'bool'>
```

**Convention:**

> "When you name a boolean variable, start it with `is`, `has`, or `can`. It reads like a yes/no question. `isAdult`, `hasLicense`, `canDrive`. Super readable."

Examples:

```python
temperature = 72
isWarm = temperature >= 70          # True
isHot = temperature > 90            # False

hasPermission = True
passingGrade = 65 >= 60             # True

print(f"isWarm: {isWarm}")
print(f"isHot: {isHot}")
print(f"hasPermission: {hasPermission}")
print(f"passingGrade: {passingGrade}")
```

---

## Section 4 — Comparisons work on strings too (3 minutes)

**Say:**

> "These same operators work on strings, not just numbers. With strings, `==` asks 'are these exactly the same text?' Case matters."

```python
print("apple" == "apple")     # True
print("apple" == "Apple")     # False — capital A is different
print("apple" != "orange")    # True
```

> "The less-than and greater-than operators also work on strings — they compare them alphabetically. You won't use that much in this class, but don't be surprised if you see it."

```python
print("apple" < "banana")     # True — a comes before b
```

### Case matters — and it matters a lot

> "If you're comparing user input to an expected word, remember that the user might type in different capitalization. The normal fix is to convert both sides to lowercase with `.lower()`."

```python
answer = input("Do you want to continue? (yes/no) ")
print(answer == "yes")               # False if user typed YES or Yes
print(answer.lower() == "yes")       # True whether they type yes, YES, Yes
```

---

## Section 5 — Live build (3 minutes)

Do this on the projector:

```python
# Program: Temperature check
# Purpose: Ask user for temperature and store a few booleans describing it.

temp = float(input("What is the temperature in °F? "))

isFreezing = temp <= 32
isCold = temp < 50
isWarm = temp >= 70
isHot = temp >= 90

print(f"Temperature: {temp}°F")
print(f"  Freezing? {isFreezing}")
print(f"  Cold?     {isCold}")
print(f"  Warm?     {isWarm}")
print(f"  Hot?      {isHot}")
```

> "Notice: none of this is making a **decision** yet. We're just calculating true/false values. Next lesson we'll use these to branch the program with `if`."

---

## Section 6 — Common Mistakes (2 minutes)

**Mistake 1: `=` instead of `==`.**

```python
if age = 18:     # SyntaxError
if age == 18:    # Correct
```

**Mistake 2: Case mismatch on strings.**

```python
choice = input("Y or N? ")
print(choice == "y")           # Could be False even if they typed Y
print(choice.lower() == "y")   # Works regardless of case
```

**Mistake 3: Comparing with the wrong type.**

```python
age = input("Age? ")       # age is a string
print(age >= 18)           # CRASHES — comparing str and int
```

Fix:

```python
age = int(input("Age? "))
print(age >= 18)           # Works
```

**Mistake 4: Chained comparisons (Python does something special here — worth mentioning briefly).**

```python
age = 20
print(18 <= age <= 65)     # True — Python allows chained comparisons!
```

> "That's a Python bonus — you can chain comparisons to check a range. Useful, but don't overuse it."

---

## Section 7 — Quick Recap (1 minute)

Ask:

1. "What does a comparison always return?"
2. "What's the difference between `=` and `==`?"
3. "What are the six comparison operators?"
4. "How do you make a string comparison case-insensitive?"

Hand off:

> "Open `lesson05_comparisonOperators_Task.ipynb`."

---

## Vocabulary introduced today

- **Comparison operator** — `==`, `!=`, `<`, `>`, `<=`, `>=` — returns a `bool`.
- **Equality operator** `==` — asks "are these equal?"
- **Inequality operator** `!=` — asks "are these different?"
- **Boolean variable** — a variable that holds `True` or `False`. Conventionally named with `is`/`has`/`can` prefix.
- **.lower()** — a string method that returns an all-lowercase version of the string. Useful for case-insensitive compares.
