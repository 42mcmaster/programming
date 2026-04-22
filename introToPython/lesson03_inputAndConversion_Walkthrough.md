# Lesson 03 — Input and Type Conversion (Teacher Walkthrough)

> **Teacher-only file.** Your ~20-minute script.

**Student deliverable:** `lesson03_inputAndConversion_Task.ipynb`
**ODE standards touched:** 5.2.1, 5.2.4, 5.4.2, 5.5.7 (read user input).

---

## Learning Objectives

1. Use `input()` to read a value typed by the user.
2. Understand that `input()` **always returns a string**.
3. Convert a string to a number using `int()` or `float()`.
4. Convert a number to a string with `str()` when needed.

---

## Section 1 — The `input()` function (5 minutes)

**Say to the class:**

> "So far every value we've put in a variable, we wrote into the program ourselves. That's not very useful — a real program gets information from the **user**. The way we read something from the user is with the `input()` function."

Demo:

```python
userName = input("What is your name? ")
print("Hello,", userName)
```

**Say:**

> "Three things are happening on that first line:"

1. The message **"What is your name? "** gets displayed — that's called the **prompt**.
2. The program **pauses** and waits for the user to type something and press Enter.
3. Whatever they type gets stored in the variable `userName`.

**Run it on the projector a couple of times with different input.**

Show the prompt with and without a trailing space:

```python
# No trailing space — cursor sticks right next to the question mark. Ugly.
name = input("Name?")

# Trailing space — cleaner, cursor is separated.
name = input("Name? ")
```

> "Always put a space at the end of your prompt string. It makes the input look clean."

---

## Section 2 — The CRITICAL rule: `input()` always returns a string (5 minutes)

**Put this on the board in big letters:**

> `input()` **ALWAYS RETURNS A STRING.**

**Say:**

> "I want you to tattoo this on your brain. Even if the user types a number, Python stores it as text — as a string. Watch what happens."

Demo the problem:

```python
age = input("How old are you? ")
print(age)
print(type(age))
print(age + 5)          # CRASH
```

**Say:**

> "The `type()` confirms it's a `str`, even though the user typed 17. So when we try to add 5 to it, Python says 'wait, you can't add a number to a string' and crashes with a **TypeError**."

Show the exact error:

```
TypeError: can only concatenate str (not "int") to str
```

---

## Section 3 — Type conversion (7 minutes)

**Say:**

> "Luckily, Python gives us functions to **convert** between types. We call these **type conversion** or **casting**."

| Function | What it does |
|---|---|
| `int(x)` | Converts `x` to an integer |
| `float(x)` | Converts `x` to a decimal number |
| `str(x)` | Converts `x` to a string |

Show each one in action:

```python
# Convert string to int
ageText = "17"
ageNumber = int(ageText)
print(ageNumber + 5)          # 22 ✓
```

```python
# Convert string to float
priceText = "9.99"
priceNumber = float(priceText)
print(priceNumber * 2)        # 19.98 ✓
```

```python
# Convert number to string
score = 100
scoreText = str(score)
print("Your score is " + scoreText)   # "Your score is 100"
```

### The normal pattern with input()

**Write this on the board and have them copy it:**

```python
age = int(input("How old are you? "))
```

**Say:**

> "Read that from the inside out. First, `input()` asks the question and gives us a string. Then, `int()` wraps around that string and converts it to a whole number. The final value stored in `age` is an int. One line does both jobs."

Same idea with float:

```python
price = float(input("How much does it cost? $"))
tax = price * 0.075
print("Tax is:", tax)
```

### Common pattern — converting numbers back to strings

Show this, which will become very relevant once we start combining strings and numbers:

```python
age = 17
# print("I am " + age + " years old")   # CRASHES — can't concatenate string + int
print("I am " + str(age) + " years old")   # Works
```

> "You can't join a string and a number with `+`. You have to convert one or the other. We'll learn a cleaner way in Lesson 04 called **f-strings**, but `str()` is the classic way."

---

## Section 4 — What breaks? (3 minutes)

**Mistake 1: Converting text that isn't a number.**

```python
age = int("seventeen")
# ValueError: invalid literal for int() with base 10: 'seventeen'
```

> "`int()` only works on text that actually looks like a number. `'17'` works; `'seventeen'` does not."

**Mistake 2: Forgetting to convert.**

```python
birthYear = input("Year you were born? ")
age = 2026 - birthYear      # CRASHES — mixing int and str
```

Fix:

```python
birthYear = int(input("Year you were born? "))
age = 2026 - birthYear      # Works
```

**Mistake 3: Using int() on a float-looking string.**

```python
price = int("9.99")
# ValueError
```

> "`int()` wants **whole numbers only**. For anything with a decimal, use `float()`."

Fix:

```python
price = float("9.99")
# Or: int(float("9.99"))   gives 9
```

---

## Section 5 — Putting it all together (demo) (3 minutes)

Build this on the projector, talking through each line:

```python
# Program: Age calculator
# Author: Ryan
# Purpose: Ask the user their birth year and tell them their age this year.

currentYear = 2026

birthYear = int(input("What year were you born? "))
age = currentYear - birthYear

print("If your birthday has already passed, you are " + str(age) + " years old this year.")
```

> "Notice we converted `input()` to `int()` so subtraction works, and we converted `age` to `str()` to concatenate it into the print line. We're juggling types — that's a skill."

---

## Section 6 — Quick Recap (1 minute)

Ask:

1. "What type does `input()` always return?"
2. "What function converts a string like `"42"` to the number 42?"
3. "What function converts the number 100 back into a string?"
4. "What's the one-line pattern to read an integer from the user?"

Then hand off:

> "Open `lesson03_inputAndConversion_Task.ipynb`."

---

## Vocabulary introduced today

- **input()** — function that reads text typed by the user.
- **Prompt** — the message displayed to the user by `input()`.
- **Type conversion (casting)** — changing a value from one type to another using `int()`, `float()`, or `str()`.
- **TypeError** — Python's complaint that you're using the wrong type for an operation.
- **ValueError** — Python's complaint that a value can't be converted (like `int("abc")`).
