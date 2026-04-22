# Lesson 04 — Arithmetic and f-strings (Teacher Walkthrough)

> **Teacher-only file.** ~20-minute script.

**Student deliverable:** `lesson04_arithmeticAndFstrings_Task.ipynb`
**ODE standards touched:** 5.2.1, 5.2.4, 5.4.2, 5.5.5, 5.5.7.

---

## Learning Objectives

1. Use the seven arithmetic operators: `+`, `-`, `*`, `/`, `//`, `%`, `**`.
2. Understand the difference between `/` (float division) and `//` (integer division).
3. Explain what `%` (modulo / remainder) returns.
4. Use **f-strings** to cleanly combine text and variables in `print()`.

---

## Section 1 — The seven arithmetic operators (8 minutes)

Put this table on the board:

| Operator | Name | Example | Result |
|---|---|---|---|
| `+` | Addition | `3 + 2` | `5` |
| `-` | Subtraction | `10 - 4` | `6` |
| `*` | Multiplication | `4 * 5` | `20` |
| `/` | Division (float) | `10 / 4` | `2.5` |
| `//` | Integer division | `10 // 4` | `2` |
| `%` | Modulo (remainder) | `10 % 4` | `2` |
| `**` | Exponent (power) | `2 ** 3` | `8` |

**Walk through each one live** in a cell. Students need to see the output.

```python
print(3 + 2)
print(10 - 4)
print(4 * 5)
print(10 / 4)
print(10 // 4)
print(10 % 4)
print(2 ** 3)
```

### The two tricky ones: `/` vs `//`

**Say:**

> "Notice what happened with `10 / 4`. It gave you `2.5` — a float. Even when you divide two whole numbers in Python, the `/` operator **always** gives you a float. If you want plain integer division — just the whole-number part, no decimal — use **two** slashes: `//`."

```python
print(10 / 4)    # 2.5   (float division)
print(10 // 4)   # 2     (integer division, drops the decimal)
print(10 // 3)   # 3
print(17 // 5)   # 3
```

### The modulo operator `%`

**Say:**

> "The `%` operator is called **modulo** or the **remainder** operator. It gives you what's left over after integer division. Think back to 3rd-grade long division."

```python
print(10 % 3)    # 1   (10 ÷ 3 is 3 remainder 1)
print(17 % 5)    # 2   (17 ÷ 5 is 3 remainder 2)
print(20 % 4)    # 0   (20 is exactly divisible by 4)
print(7 % 2)     # 1   (odd)
print(8 % 2)     # 0   (even)
```

**Flag this classic use:**

> "`n % 2` is how you check if a number is even or odd. Even numbers give you 0, odd numbers give you 1. You'll see this come back over and over."

### Exponent `**`

```python
print(2 ** 3)    # 8  (2 cubed)
print(5 ** 2)    # 25 (5 squared)
print(9 ** 0.5)  # 3.0 (square root — power of 0.5)
```

### Order of operations

**Say:**

> "Python follows PEMDAS — parentheses first, then exponents, then multiplication and division, then addition and subtraction. When in doubt, add parentheses. They're free."

```python
print(2 + 3 * 4)        # 14  — multiplication first
print((2 + 3) * 4)      # 20  — parentheses force addition first
```

---

## Section 2 — Assignment operators (2 minutes)

**Say:**

> "You'll often want to update a variable based on its current value. Python has shortcuts for this."

| Shortcut | Long form | Meaning |
|---|---|---|
| `x += 1` | `x = x + 1` | Add 1 to x |
| `x -= 1` | `x = x - 1` | Subtract 1 from x |
| `x *= 2` | `x = x * 2` | Double x |
| `x /= 2` | `x = x / 2` | Halve x |

Demo:

```python
score = 10
score += 5       # score is now 15
print(score)
score -= 2       # score is now 13
print(score)
score *= 2       # score is now 26
print(score)
```

---

## Section 3 — f-strings (7 minutes)

**This is the big one. Clear a cell on the projector.**

> "Up until now, when you wanted to mix text and variables in a print, you had to do ugly stuff like this:"

```python
name = "Ryan"
age = 17
print("My name is " + name + " and I am " + str(age) + " years old.")
```

> "Notice all that: you had to wrap `age` in `str()`, you had to manage every single space, and there's a string-plus-string-plus-string mess. There's a way cleaner way — it's called an **f-string**."

Rewrite the same line:

```python
name = "Ryan"
age = 17
print(f"My name is {name} and I am {age} years old.")
```

**Say:**

> "Three things changed:"

1. There's an `f` right before the opening quote: `f"..."`. That `f` stands for **formatted**.
2. The variables are written inside **curly braces** `{}` directly in the string.
3. No more `+` signs. No more `str()`. Python fills in the values for you.

Show more examples:

```python
firstName = "Alex"
grade = 94.5

print(f"Hi, {firstName}!")
print(f"Your grade is {grade}.")
print(f"Next year, {firstName} will be a senior.")
```

### You can put expressions inside the braces, not just variable names

```python
price = 20
tax = 0.075
print(f"Total: ${price + (price * tax)}")
```

```python
num = 7
print(f"{num} squared is {num ** 2}")
```

### Formatting numbers inside an f-string (optional but nice)

> "You can tell Python how to format a number with a colon and a format code. The most useful one: round to a specific number of decimals."

```python
price = 19.99
tax = price * 0.075
total = price + tax

print(f"Subtotal: ${price:.2f}")   # 2 decimal places
print(f"Tax:      ${tax:.2f}")
print(f"Total:    ${total:.2f}")
```

> "The `:.2f` means 'show this as a float with 2 decimals.' Super useful for money."

---

## Section 4 — Putting it all together (live build, 2 minutes)

Build this together with the class:

```python
# Program: Receipt calculator
# Author: Ryan
# Purpose: Compute total, tax, tip, and grand total for a meal.

priceText = input("Meal price: $")
price = float(priceText)

taxRate = 0.075
tipRate = 0.18

tax = price * taxRate
tip = price * tipRate
grandTotal = price + tax + tip

print("-----------------------")
print(f"Subtotal:     ${price:.2f}")
print(f"Tax (7.5%):   ${tax:.2f}")
print(f"Tip (18%):    ${tip:.2f}")
print(f"Grand Total:  ${grandTotal:.2f}")
print("-----------------------")
```

> "Clean. Everything lined up. Two decimal places. That's production-quality output."

---

## Section 5 — Common Mistakes (1 minute)

**Mistake 1: Forgetting the `f`.**

```python
name = "Alex"
print("Hi, {name}!")      # prints literally: Hi, {name}!
print(f"Hi, {name}!")     # prints: Hi, Alex!
```

**Mistake 2: Using `/` when you wanted `//`.**

```python
slices = 7
people = 3
print(f"Each person gets {slices / people} slices")   # 2.333...
print(f"Each person gets {slices // people} whole slices, {slices % people} left over")
```

**Mistake 3: `^` instead of `**` for power.**

```python
print(2 ^ 3)     # 1 — this is NOT exponent in Python, it's bitwise XOR
print(2 ** 3)    # 8 — this is exponent
```

---

## Section 6 — Quick Recap (1 minute)

Ask:

1. "What's the difference between `/` and `//`?"
2. "What does `17 % 5` give us, and why?"
3. "What character goes before the opening quote of an f-string?"
4. "What does `:.2f` do inside an f-string?"

Hand off:

> "Open `lesson04_arithmeticAndFstrings_Task.ipynb`."

---

## Vocabulary introduced today

- **Arithmetic operator** — a symbol that does math: `+`, `-`, `*`, `/`, `//`, `%`, `**`.
- **Float division** `/` — always returns a decimal number.
- **Integer division** `//` — drops the decimal, returns a whole number.
- **Modulo** `%` — returns the remainder of a division.
- **Exponent** `**` — raises a number to a power.
- **Assignment shortcut** — `+=`, `-=`, `*=`, `/=` update a variable based on its current value.
- **f-string** — a string prefixed with `f` that lets you embed variables and expressions inside `{}`.
