# Lesson 02 — Variables and Data Types (Teacher Walkthrough)

> **Teacher-only file.** This is your script for the ~20-minute whole-class opener.

**Student deliverable for today:** `lesson02_variablesAndTypes_Task.ipynb`
**ODE standards touched:** 5.2.1 (data types), 5.2.3 (variables), 5.4.2 (write/edit in IDE), 5.5.5 (naming & comments).

---

## Learning Objectives

1. Create a variable and give it a value.
2. Name the four most common data types: **int**, **float**, **str**, **bool**.
3. Use `type()` to check what type a value is.
4. Follow Python naming conventions (lowercase, snake_case or camelCase, descriptive names).

---

## Section 1 — What is a variable? (3 minutes)

**Say to the class:**

> "A **variable** is a labeled container. Think of it like a box with your name written on the side. You put something in the box, and later when you need it, you just say the name on the box and Python hands you what's inside."

Type this on the projector:

```python
age = 17
print(age)
```

**Say:**

> "Read that out loud: 'age equals 17.' The `=` sign is called the **assignment operator**. It does NOT mean 'is equal to' like in math — it means 'take the thing on the right and put it in the box named on the left.' The value goes right-to-left into the variable."

Now show that you can change what's inside the box:

```python
age = 17
print(age)
age = 18      # Birthday!
print(age)
```

**Say:**

> "We reassigned `age` to a new value. The old 17 is gone. Variables hold one value at a time — the newest one wins."

---

## Section 2 — The four basic data types (7 minutes)

Put these four words on the board:

> **int, float, str, bool**

**Say:**

> "Every value in Python has a **type**. The type tells Python what kind of thing it is and what you can do with it. Today we care about four types."

### 2a. int (integer)

> "An `int` is a **whole number** — positive, negative, or zero. No decimal point."

```python
age = 17
studentCount = 28
temperature = -5
print(age, studentCount, temperature)
```

### 2b. float (floating-point number)

> "A `float` is a **decimal number**. The name comes from the decimal point being able to 'float' anywhere in the number."

```python
price = 9.99
pi = 3.14159
negativeDecimal = -0.5
print(price, pi, negativeDecimal)
```

**Show that even `5.0` is a float, not an int:**

```python
print(5)      # int
print(5.0)    # float — the decimal makes it a float
```

### 2c. str (string)

> "A `str` is **text** — anything in quotes. It can be a single character, a word, a sentence, or even a whole paragraph."

```python
firstName = "Ryan"
favoriteColor = "green"
message = "Welcome to Python!"
print(firstName, favoriteColor, message)
```

**Show that numbers in quotes are strings, not numbers:**

```python
realAge = 17       # int — a number
fakeAge = "17"     # str — the characters 1 and 7
print(realAge)
print(fakeAge)
```

### 2d. bool (boolean)

> "A `bool` has only **two possible values**: `True` or `False`. That's it. You use booleans to represent yes/no, on/off, correct/incorrect."

```python
isStudent = True
hasDriverLicense = False
print(isStudent, hasDriverLicense)
```

**Flag this carefully:**

> "Notice the capital T and capital F. `True` and `False` must be capitalized. Lowercase `true` will crash."

```python
isStudent = true       # NameError — crashes
isStudent = True       # Works
```

---

## Section 3 — Checking a type with type() (2 minutes)

```python
age = 17
price = 9.99
name = "Ryan"
isStudent = True

print(type(age))
print(type(price))
print(type(name))
print(type(isStudent))
```

**Say:**

> "`type()` is a function that tells you what type a value is. Super useful when you're debugging and you're not sure what something is. You'll see output like `<class 'int'>` — just focus on the word in the quotes."

---

## Section 4 — Naming Rules and Conventions (5 minutes)

**Put these two lists on the board side-by-side:**

| Valid names | Invalid names |
|---|---|
| `age`, `firstName`, `total_count`, `x`, `score2` | `2score` (can't start with a number), `first name` (no spaces), `first-name` (no dashes), `if` (reserved word) |

**Hard rules (Python will crash if you break these):**

- Must start with a letter or underscore.
- Can only contain letters, digits, and underscores. **No spaces. No dashes.**
- Cannot be a **reserved word** like `if`, `for`, `while`, `print`, `True`, `False`.

**Style rules (Python won't crash but I'll dock points):**

- Use **descriptive** names. `studentAge` is better than `x`.
- Use **camelCase** for variables (first word lowercase, each later word capitalized): `firstName`, `finalScore`, `isStudent`.
  - You will also see `snake_case` (`first_name`) — that's fine too, but pick one and stay consistent.
- Keep variable names **short-ish** but meaningful.

Demo bad-to-better names:

```python
x = 17                   # bad — what is x?
a = 17                   # still bad
age = 17                 # good
studentAge = 17          # even better if there could be other ages
```

---

## Section 5 — Common Mistakes (2 minutes)

**Mistake 1: Treating a string like a number.**

```python
priceText = "9.99"
# priceText + 1    ← This would crash because priceText is a string, not a number
```

> "We'll fix this in Lesson 03 with type conversion."

**Mistake 2: Using a variable before creating it.**

```python
print(score)      # NameError — score doesn't exist yet
score = 100       # Too late; the print already crashed
```

**Mistake 3: Assignment backwards.**

```python
17 = age          # SyntaxError — variable must be on the LEFT
age = 17          # Correct
```

**Mistake 4: Lowercase true/false.**

```python
isHungry = true   # NameError
isHungry = True   # Correct
```

---

## Section 6 — Quick Recap (1 minute)

Ask out loud:

1. "What's the difference between `int` and `float`?"
2. "What's the difference between `17` and `"17"`?"
3. "What are the only two values a `bool` can have?"
4. "Why is `firstName` a better variable name than `x`?"

Then hand off:

> "Open `lesson02_variablesAndTypes_Task.ipynb` and get started."

---

## Vocabulary introduced today

- **Variable** — a named container that holds a value.
- **Assignment operator** `=` — puts the value on the right into the variable on the left.
- **Type** — what kind of value something is.
- **int** — whole number.
- **float** — decimal number.
- **str** — text in quotes.
- **bool** — True or False.
- **camelCase** — naming style where the first word is lowercase and later words are Capitalized.
- **Reserved word** — a word Python already uses (like `if`, `for`, `print`) that you can't use as a variable name.
