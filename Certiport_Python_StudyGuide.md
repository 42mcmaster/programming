# Certiport ITS Python — Student Study Guide

A self-paced review for the Certiport / GMetrix Information Technology Specialist (ITS) Python certification exam.

---

## How to Use This Guide

This guide is structured as **fourteen short modules**, building from Python syntax up through data structures, functions, file I/O, testing, and finishing with test-taking strategy. Work through them in order — each module assumes the ones before it.

Every module follows the same rhythm:

1. **Concept** — read the explanation.
2. **Anchor** — a small diagram, table, code snippet, or rule of thumb you should be able to redraw from memory.
3. **Self-check** — exam-style question(s) plus "explain the distractor" practice.

The single most powerful study habit for this exam is **explaining why the wrong answers are wrong**. If you can do that, the right answer takes care of itself.

### What This Exam Tests Most Heavily

Across the two practice exams (84 questions total), the heaviest weight is on:

- **Operators and order of operations** — arithmetic, comparison, logical, and especially `==` vs. `=` vs. `is`.
- **Control flow and loops** — `if`/`elif`/`else`, `for` with `range()`, `while`, plus `break` / `continue` / `pass`.
- **Data structures** — lists vs. tuples vs. sets vs. dicts, indexing (zero-based!), and slicing.
- **Functions** — `def`, parameters, default values, `return`, and storing the return value.
- **Built-in modules** — `math`, `random`, `datetime`, `os`, and `sys`.

Lighter but reliable: file I/O modes, exception handling, and the `unittest` framework.

---

## Table of Contents

1. [Python Syntax, Comments, and Documentation](#module-1--python-syntax-comments-and-documentation)
2. [Data Types and Type Conversion](#module-2--data-types-and-type-conversion)
3. [Operators and Order of Operations](#module-3--operators-and-order-of-operations)
4. [Control Flow: `if` / `elif` / `else`](#module-4--control-flow-if--elif--else)
5. [Loops: `for` and `while`](#module-5--loops-for-and-while)
6. [Strings, Formatting, and Slicing](#module-6--strings-formatting-and-slicing)
7. [Lists, Tuples, Sets, and Dictionaries](#module-7--lists-tuples-sets-and-dictionaries)
8. [Functions](#module-8--functions)
9. [Input / Output and File I/O](#module-9--input--output-and-file-io)
10. [Exception Handling](#module-10--exception-handling)
11. [Built-In Modules: `math`, `random`, `datetime`, `os`, `sys`](#module-11--built-in-modules-math-random-datetime-os-sys)
12. [Unit Testing with `unittest`](#module-12--unit-testing-with-unittest)
13. [Errors, Debugging, and Common Pitfalls](#module-13--errors-debugging-and-common-pitfalls)
14. [Test-Taking Strategy and Final Review](#module-14--test-taking-strategy-and-final-review)
15. [Exam-Day Cheat Card](#exam-day-cheat-card)
16. [Master Glossary](#master-glossary)

---

## Module 1 — Python Syntax, Comments, and Documentation

### Concept

A surprising number of exam points come from syntax mechanics — colons, indentation, comment characters, and case sensitivity. These are easy to lose if you skim, and easy to lock in if you drill them once.

### Anchor: The Mechanics

| Rule                            | Detail                                                                                            |
| ------------------------------- | ------------------------------------------------------------------------------------------------- |
| **Comment character**           | `#` for single-line. (`//` is C/JavaScript; `/* */` is HTML/C; `--` is SQL — none work in Python.) |
| **Colons end control headers**  | Every `if`, `elif`, `else`, `for`, `while`, `def`, `class`, `try`, `except`, `finally` ends with `:`. |
| **Indentation is required**     | The body of a control statement **must** be indented. No braces.                                  |
| **Case sensitivity**            | `True`, `False`, `None` are capitalized. `true` is **not** a Boolean.                             |
| **Line continuation**           | A trailing backslash `\` continues a code line. (Inside strings, `\n`, `\t`, etc. are escapes.)   |

### Anchor: Comments vs. Docstrings vs. `pydoc`

```python
# This is a single-line comment.

def calc_area(width, height):
    """Return the area of a rectangle.

    width  -- in feet
    height -- in feet
    """
    return width * height

print(calc_area.__doc__)        # prints the triple-quoted docstring
```

- **Triple-quoted strings** (`"""..."""` or `'''...'''`) placed *immediately after* a `def` or `class` are docstrings. They document the function and are accessible via `funcname.__doc__`.
- **`pydoc`** generates documentation from Python modules: `python -m pydoc module_name`.

### Self-Check

> Which line is a valid Python comment?
> A) `// this is a note`
> B) `/* this is a note */`
> C) `# this is a note`
> D) `-- this is a note`

**Answer:** C.
**Why the others are wrong:** A is JavaScript/C++, B is C/HTML, D is SQL.

> Which keyword/value is a valid Boolean in Python?
> A) `true`
> B) `TRUE`
> C) `"True"`
> D) `True`

**Answer:** D. Python is case-sensitive; only the capitalized form is the literal.

---

## Module 2 — Data Types and Type Conversion

### Concept

Python is **dynamically typed** — you don't declare variable types. But you do need to know the built-in types, when they're created, and how to convert between them. Several exam questions hinge on whether `int()` truncates, what `str()` does to a number, and which collection types are mutable.

### Anchor: The Eight Core Types

| Type    | Example                  | Notes                              |
| ------- | ------------------------ | ---------------------------------- |
| `int`   | `42`                     | Whole numbers                      |
| `float` | `3.14`, `44.0`           | Numbers with decimals              |
| `str`   | `"hello"`, `'hi'`        | Text in quotes                     |
| `bool`  | `True`, `False`          | Capitalized                        |
| `list`  | `[1, 2, 3]`              | Ordered, mutable                   |
| `tuple` | `(1, 2, 3)`              | Ordered, **immutable**             |
| `set`   | `{1, 2, 3}`              | Unordered, unique items            |
| `dict`  | `{"k": "v"}`             | Key-value pairs                    |

### Anchor: Conversion Functions

| Function   | Behavior                                                       |
| ---------- | -------------------------------------------------------------- |
| `int(x)`   | Drops the decimal portion (truncates **toward zero**)          |
| `float(x)` | Converts to a decimal — `float(44)` → `44.0`                   |
| `str(x)`   | Converts to a string — useful for IDs / serial numbers you don't want to do math on |
| `bool(x)`  | Converts to `True` / `False` (most non-empty values are `True`) |

A common trap: `int(3.9)` returns `3`, not `4` — it truncates rather than rounding.

### Anchor: Mutable vs. Immutable

```
MUTABLE (can be changed in place):    list, set, dict
IMMUTABLE (cannot be changed):        int, float, str, bool, tuple
```

Trying to assign into a tuple — `t[0] = 99` — raises `TypeError`.

### Self-Check

> What is the result of `int(7.8)`?
> A) `8`
> B) `7`
> C) `7.0`
> D) `7.8`

**Answer:** B. `int()` truncates toward zero.

> Which type is **immutable**?
> A) `list`
> B) `dict`
> C) `tuple`
> D) `set`

**Answer:** C.

---

## Module 3 — Operators and Order of Operations

### Concept

This is the highest-density module on the exam. You must be fluent in arithmetic, comparison, logical, identity, and membership operators — and you must know the precedence order cold.

### Anchor: Arithmetic Operators

| Operator | Meaning           | Example         | Result |
| -------- | ----------------- | --------------- | ------ |
| `+`      | Addition          | `2 + 3`         | `5`    |
| `-`      | Subtraction       | `5 - 3`         | `2`    |
| `*`      | Multiplication    | `4 * 3`         | `12`   |
| `/`      | True division     | `10 / 3`        | `3.333…` |
| `//`     | Floor division    | `10 // 3`       | `3`    |
| `%`      | Modulo (remainder)| `10 % 3`        | `1`    |
| `**`     | Exponent          | `2 ** 3`        | `8`    |

### Anchor: Comparison and Logical

```python
==   !=   >   <   >=   <=         # comparison; return Booleans
and  or  not                       # logical
```

**Precedence within logicals (highest → lowest): `not` → `and` → `or`.**

### Anchor: `==` vs. `is` vs. `=`

| Operator | Meaning                                                       |
| -------- | ------------------------------------------------------------- |
| `=`      | **Assignment** — gives a name a value                          |
| `==`     | **Equality** — are the values equal?                           |
| `is`     | **Identity** — are these the same object in memory?            |

```python
a = [1, 2, 3]
b = a               # b refers to the SAME list as a
c = [1, 2, 3]       # c is a NEW list with equal contents

a == b   # True — values match AND same object
a is b   # True — same object in memory
a == c   # True — values match
a is c   # False — different objects
```

### Anchor: Membership and Compound Assignment

```python
"nine" in quote                  # True if "nine" is a substring
5 in [1, 2, 3, 5]                # True
"name" in {"name": "Ana"}        # True — dict membership checks KEYS

a += b   # a = a + b
a -= b   # a = a - b
a *= b   # a = a * b
a /= b   # a = a / b
a //= b  # a = a // b
a %= b   # a = a % b
a **= b  # a = a ** b
```

### Anchor: Full Precedence Order (highest → lowest)

```
1. Parentheses                    ( )
2. Exponent                       **
3. Multiply / Divide / Floor / Mod  *  /  //  %
4. Add / Subtract                  +  -
5. Comparison / Membership / Identity   ==  !=  <  >  <=  >=  in  not in  is  is not
6. Logical                         not  →  and  →  or
7. Assignment                       =  +=  -=  ...
```

When in doubt, parenthesize.

### Anchor: A Classic "Logic Error" Trap

```python
# Goal: 7% interest on the full bill (car + license)
total = car_price + license_fee * interest_rate    # ❌ WRONG
total = (car_price + license_fee) * interest_rate  # ✅ correct
```

The first version multiplies only the license fee by the rate — a logic error, not a syntax error. Code runs but produces the wrong answer.

### Self-Check

> What does `10 // 3` evaluate to?
> A) `3.333`
> B) `3`
> C) `1`
> D) `30`

**Answer:** B. Floor division drops the decimal.

> Given `a = [1, 2]` and `b = a`, which is `True`?
> A) `a is b`
> B) `a is not b`
> C) `a == b` is False
> D) `a` and `b` are different objects

**Answer:** A. They refer to the same object.

> Which has the **highest** logical-operator precedence?
> A) `or`
> B) `and`
> C) `not`
> D) `==`

**Answer:** C. Order: `not` → `and` → `or`.

---

## Module 4 — Control Flow: `if` / `elif` / `else`

### Concept

Conditional logic is everywhere on the exam. The two recurring traps are **branch order** (an earlier `if` swallows later cases) and **operator choice** (`==` vs. `>=`).

### Anchor: The Pattern

```python
if score >= 90:
    grade = 'A'
elif score >= 80:
    grade = 'B'
elif score >= 70:
    grade = 'C'
else:
    grade = 'F'
```

- Every condition line ends with `:`.
- Each body is indented (typically 4 spaces).
- `elif` is short for "else if" and is checked only when the previous conditions were false.
- The `else` branch is optional and runs when nothing above matched.

### Anchor: Branch Order Matters

When ranges overlap, check the **most restrictive** range first. Otherwise an earlier branch silently captures every case.

```python
# ❌ This always assigns 'F' or 'C', never A or B
if score >= 60:
    grade = 'C'
elif score >= 90:
    grade = 'A'        # unreachable
```

Walking from the top down, scoring 95 still hits `score >= 60` first → `'C'`. The `>= 90` branch is dead code.

### Anchor: `pass` as a Placeholder

Empty bodies cause `IndentationError`. Use `pass` to write the structure first and fill in the action later:

```python
if user_logged_in:
    pass        # TODO: load dashboard
else:
    redirect_to_login()
```

### Self-Check

> What's wrong with this code?
>
> ```python
> if temp > 100
>     print("hot")
> ```
>
> A) Missing parentheses around the condition
> B) Missing colon at the end of the `if` line
> C) `print` should be capitalized
> D) Nothing — it works

**Answer:** B. Every control header ends with `:`.

> Which operator should be used for "exactly equal to 100"?
> A) `=`
> B) `==`
> C) `>=`
> D) `is`

**Answer:** B. `=` is assignment; `==` is equality.

---

## Module 5 — Loops: `for` and `while`

### Concept

Both loop types are tested. The most common confusion is **when to use which** and the off-by-one behavior of `range()`.

### Anchor: `for` Loops and `range()`

Use `for` when iterating a known collection or a known number of times.

```python
for i in range(1, 6):       # 1, 2, 3, 4, 5  (stop value EXCLUDED)
    print(i * 10)

for fruit in ["apple", "pear", "kiwi"]:
    print(fruit)
```

| Form                        | Produces                                  |
| --------------------------- | ----------------------------------------- |
| `range(n)`                  | `0, 1, 2, …, n-1`                         |
| `range(start, stop)`        | `start, start+1, …, stop-1`               |
| `range(start, stop, step)`  | every `step` value, stopping before `stop` |

Example: `range(3, 102, 3)` gives `3, 6, 9, …, 99` (multiples of 3 between 3 and 99).

### Anchor: `while` Loops

Use `while` when the number of iterations is unknown — keep going until a condition flips.

```python
guess = 0
while guess != answer:
    guess = int(input("Guess: "))
```

The condition is checked **before** each iteration. If the condition starts false, the body never runs.

### Anchor: `break`, `continue`, `pass`

| Keyword    | Effect                                                                                  |
| ---------- | --------------------------------------------------------------------------------------- |
| `break`    | Immediately exit the loop. Place **after** a `print` to include the current item; **before** to exclude it. |
| `continue` | Skip the rest of this iteration; jump back to the loop header.                          |
| `pass`     | Do nothing; placeholder so an empty body is syntactically valid.                        |

### Anchor: Nested Loops

Common for grids, matrices, and "every X for every Y" patterns:

```python
for day in range(7):
    for student in range(10):
        record_attendance(day, student)
```

The inner loop runs to completion for **every** iteration of the outer loop.

### Self-Check

> How many iterations does `for i in range(5):` perform?
> A) 4
> B) 5
> C) 6
> D) Infinite

**Answer:** B. `range(5)` produces `0, 1, 2, 3, 4` — five values.

> Which keyword skips the rest of the current iteration but stays in the loop?
> A) `break`
> B) `continue`
> C) `pass`
> D) `return`

**Answer:** B.

---

## Module 6 — Strings, Formatting, and Slicing

### Concept

Strings show up in two forms on the exam: as text being **formatted** for output, and as sequences being **sliced**. Both are mostly notation drills.

### Anchor: Three Ways to Format

```python
items = 5
price = 19.995

# 1. f-string (recommended)
print(f"You have {items} items at ${price:0.2f}")

# 2. .format()
print("You have {} items at ${:0.2f}".format(items, price))

# 3. % formatting (older)
print("Cost: %.2f" % price)
```

The `f` prefix marks an f-string; `{var}` slots in variables. `:0.2f` formats a float to two decimals.

### Anchor: Escape Sequences

| Sequence | Meaning                  |
| -------- | ------------------------ |
| `\n`     | Newline                  |
| `\t`     | Tab                      |
| `\\`     | Literal backslash        |
| `\'`     | Literal single quote     |
| `\"`     | Literal double quote     |

`\` at the **end of a code line** (outside a string) means "this line continues on the next line" — different from the inside-string escape sequences above.

### Anchor: Slicing — `[start:stop:step]`

```python
text = "PYTHON"

text[0]        # 'P'        — first character
text[-1]       # 'N'        — last character
text[1:]       # 'YTHON'    — drop first character
text[:3]       # 'PYT'      — first three
text[::2]      # 'PTO'      — every other character
text[::-1]     # 'NOHTYP'   — reversed
```

The `stop` index is **exclusive**: `text[1:3]` is `'YT'`, not `'YTH'`. `step` defaults to 1; a negative step walks backward.

### Self-Check

> What does `"DATABASE"[::-1]` return?
> A) `"DATABASE"`
> B) `"ESABATAD"`
> C) `"D"`
> D) An error

**Answer:** B. A step of -1 reverses the string.

> Which f-string formats `price = 19.995` to two decimals?
> A) `f"{price}"`
> B) `f"{price:0.2f}"`
> C) `f"{price%2}"`
> D) `f"{price.format(2)}"`

**Answer:** B.

---

## Module 7 — Lists, Tuples, Sets, and Dictionaries

### Concept

The exam expects fluency in all four collection types and the differences between them. Most data-structure questions test **mutability**, **ordering**, and **zero-based indexing**.

### Anchor: The Four Collections

| Type    | Syntax           | Ordered? | Mutable? | Allows duplicates? | Indexed? |
| ------- | ---------------- | -------- | -------- | ------------------ | -------- |
| `list`  | `[1, 2, 3]`      | ✅       | ✅       | ✅                 | ✅       |
| `tuple` | `(1, 2, 3)`      | ✅       | ❌       | ✅                 | ✅       |
| `set`   | `{1, 2, 3}`      | ❌       | ✅       | ❌                 | ❌       |
| `dict`  | `{"k": "v"}`     | (insertion-ordered) | ✅ | keys must be unique | by **key**, not position |

### Anchor: List Operations

```python
animals = ["dog", "cat"]

animals.append("Jaguars")    # add to end
animals.insert(0, "ant")     # insert at index
animals.remove("dog")        # remove by value (first match)
animals.sort()               # sort in place (alphabetical / numeric)
animals.reverse()            # reverse in place
len(animals)                 # length
animals[0]                   # first item (zero-based!)
animals[-1]                  # last item
list1 + list2                # concatenate
```

### Anchor: Zero-Based Indexing

A list with **6 items** is indexed `0, 1, 2, 3, 4, 5`. The "last item" is `list[5]` — equivalently `list[-1]`. Trying `list[6]` raises `IndexError: list index out of range`.

### Anchor: Tuple — Read-Only

```python
products = ("A1", "B2", "C3")
products[0]                    # "A1"  — indexing works
# products[0] = "X"            # ❌ TypeError — tuples are immutable
```

### Anchor: Set and Dict

```python
locations = {"HQ", "West", "Remote1"}      # unordered, unique
{1, 2, 2, 3}                                 # → {1, 2, 3} duplicates dropped

person = {"name": "Ana", "age": 30}          # key-value pairs
person["age"]                                # 30
person["age"] = 31                           # update
person["email"] = "a@x.com"                  # add new key
"name" in person                             # True — `in` checks KEYS
```

### Self-Check

> A list has six items. What is the index of the last item?
> A) `6`
> B) `7`
> C) `5`
> D) `1`

**Answer:** C. Indices run `0` through `5`.

> Which operation is **not** allowed?
> A) `[1, 2, 3].append(4)`
> B) `(1, 2, 3)[0] = 99`
> C) `{1, 2, 3}.add(4)`
> D) `{"a": 1}["a"] = 2`

**Answer:** B. Tuples are immutable.

---

## Module 8 — Functions

### Concept

Functions have a few syntax rules and a few "calling" rules. The most common exam trap: calling a function but not storing its return value.

### Anchor: Defining and Calling

```python
def calc_subtotal(amount, sales_tax):
    """Return amount with sales tax applied."""
    subtotal = amount * (1 + sales_tax)
    return subtotal

order_total = calc_subtotal(500, 0.07)   # capture the return
```

Rules:

- Use **`def`** to declare. (Not `function` — that's JavaScript.)
- Header ends with `:`. Body is indented.
- **`return`** sends a value back. Without `return`, the function returns `None`.
- **To keep the return value, assign it**: `total = calc_subtotal(...)`. Calling `calc_subtotal(...)` alone discards the result.

### Anchor: Default Parameter Values

```python
def area(width, height=2):
    return width * height

area(5)        # 10  (uses default height=2)
area(5, 10)    # 50  (overrides default)
```

**Required parameters must come before defaulted ones** in the signature. `def f(a=1, b)` is a syntax error.

### Anchor: Docstrings

Place a triple-quoted string immediately under the `def` to document the function. Access it with `func.__doc__`.

```python
def greet(name):
    """Print a friendly greeting."""
    print(f"Hello, {name}!")

print(greet.__doc__)   # "Print a friendly greeting."
```

### Self-Check

> Which keyword defines a function in Python?
> A) `function`
> B) `def`
> C) `define`
> D) `func`

**Answer:** B.

> What does this print?
>
> ```python
> def square(n):
>     return n * n
>
> square(4)
> print("done")
> ```
>
> A) `16` then `done`
> B) `done`
> C) `4`
> D) An error

**Answer:** B. `square(4)` is called but the return value is discarded — never printed. Only `print("done")` produces output.

---

## Module 9 — Input / Output and File I/O

### Concept

You should be fluent in reading from the user, printing to the console, and reading/writing files. The most-tested file detail is the **mode flag** — `"r"`, `"w"`, `"a"`, `"r+"`.

### Anchor: Console I/O

```python
guess = int(input("Enter a number from 1 to 10: "))
print("You guessed:", guess)
print()                           # blank line
```

`input()` **always returns a string**. To use it as a number, wrap it: `int(input(...))` or `float(input(...))`.

### Anchor: File Modes

| Mode  | Behavior                                                       |
| ----- | -------------------------------------------------------------- |
| `"r"` | **Read-only** — file must exist                                |
| `"w"` | **Write** — creates a new file or **overwrites** existing      |
| `"a"` | **Append** — creates if missing; writes to end if it exists    |
| `"r+"`| Read **and** write                                              |

A common bug: using `"w"` when you meant `"a"`. `"w"` wipes out the existing file's contents the moment you open it.

### Anchor: Reading and Writing

```python
# Read
with open("file.txt", "r") as file:
    content = file.read()

# Write (overwrite)
with open("log.txt", "w") as file:
    file.write("Daily message")

# Append (preserve existing content)
with open("log.txt", "a") as file:
    file.write("\nNew entry")
```

The `with` block automatically closes the file when finished — preferred over manually calling `file.close()`.

### Anchor: Existence Checks and Deletion

```python
import os

if os.path.isfile("config.txt"):
    print("found")

if os.path.exists("config.txt"):
    print("exists (file or directory)")

if os.path.isfile("temp.txt"):
    os.remove("temp.txt")
```

`os.path.isfile()` returns `True` only for actual files; `os.path.exists()` is `True` for files **or** directories. `import os` is the most reliable way to access these.

### Self-Check

> Which mode opens a file for writing **without** erasing existing content?
> A) `"r"`
> B) `"w"`
> C) `"a"`
> D) `"x"`

**Answer:** C. `"a"` appends; `"w"` overwrites.

> What is the type of value returned by `input()`?
> A) `int`
> B) `float`
> C) `str`
> D) Whatever the user types

**Answer:** C. Always a string — convert it if you need a number.

---

## Module 10 — Exception Handling

### Concept

Exception handling lets a program respond to runtime errors instead of crashing. The exam tests the four-block structure (`try` / `except` / `else` / `finally`) and a few specific exception names.

### Anchor: The Pattern

```python
try:
    result = a / b
except ZeroDivisionError:
    print("Can't divide by zero.")
else:
    print("Result:", result)        # runs only if NO exception
finally:
    print("Done.")                  # runs ALWAYS — error or not
```

| Block       | Runs When                                                    |
| ----------- | ------------------------------------------------------------ |
| `try`       | Always — wraps the risky code                                |
| `except`    | When a matching exception is raised                          |
| `else`      | Only when **no** exception was raised                        |
| `finally`   | **Always** — used for cleanup, "make sure this runs"         |

### Anchor: Raising and Catching

```python
def withdraw(amount):
    if amount < 0:
        raise ValueError("Amount must be positive.")
    ...
```

- **`raise`** is the keyword to throw an exception. (`throw` is Java — not Python.)
- A bare `except:` catches any exception — usually too broad. Catch specific exception types when you can.

### Anchor: Common Exceptions

| Exception            | When It's Raised                                         |
| -------------------- | -------------------------------------------------------- |
| `ZeroDivisionError`  | Dividing by zero                                         |
| `IndexError`         | List index out of range                                  |
| `KeyError`           | Dict key doesn't exist                                   |
| `ValueError`         | Right type, wrong value (e.g., `int("abc")`)             |
| `TypeError`          | Wrong type for the operation                             |
| `FileNotFoundError`  | Opening a missing file in read mode                      |

### Self-Check

> Which block runs **regardless** of whether an exception was raised?
> A) `try`
> B) `except`
> C) `else`
> D) `finally`

**Answer:** D.

> Which keyword manually triggers an exception in Python?
> A) `throw`
> B) `raise`
> C) `error`
> D) `panic`

**Answer:** B.

---

## Module 11 — Built-In Modules: `math`, `random`, `datetime`, `os`, `sys`

### Concept

The exam tests function names from a handful of standard-library modules. You must `import` the module before using it.

### Anchor: `math` — Math Operations

```python
import math

math.pi             # 3.14159…
math.ceil(4.2)      # 5      — round up
math.floor(4.8)     # 4      — round down
math.sqrt(16)       # 4.0    — square root (float)
math.isqrt(17)      # 4      — integer square root
math.pow(2, 3)      # 8.0    — power as a float
math.fabs(-14)      # 14.0   — absolute value as a float
math.fmod(21, -14)  # 7.0    — floating-point modulus
math.isnan(x)       # True if x is NaN
```

### Anchor: `random` — Random Values

```python
import random

random.choice(countries)         # pick one item from a list
random.shuffle(deck)             # shuffle in place (no return)
random.randint(1, 10)            # whole number, INCLUSIVE on both ends
random.randrange(3, 102, 3)      # 3, 6, …, 99 (stop EXCLUDED, like range)
random.random()                  # float in [0.0, 1.0)
```

A common trap: `randint(a, b)` is inclusive on both ends; `randrange(a, b)` excludes `b` (just like the built-in `range`).

### Anchor: `datetime` — Dates and Times

```python
import datetime

datetime.datetime.now()                              # current date+time
datetime.datetime.today()                            # current date+time
today = datetime.date.today()                        # just today's date

today.strftime("%Y-%m-%d")                            # date → string ("format")
datetime.datetime.strptime("2024-01-15", "%Y-%m-%d") # string → date  ("parse")
```

Memory aid: **`strftime` = format time (to string), `strptime` = parse time (from string).**

### Anchor: `os` and `os.path` — Filesystem

```python
import os

os.path.isfile(path)
os.path.exists(path)
os.remove(path)
```

### Anchor: `sys` — System and Command-Line Args

```python
import sys

sys.argv          # list: [scriptname, arg1, arg2, …]
sys.argv[0]       # the .py filename being run
sys.argv[1]       # first command-line argument
len(sys.argv)     # total count
```

Running `python testargs.py Hello World` makes `sys.argv` equal to `['testargs.py', 'Hello', 'World']`.

### Self-Check

> Which call returns `5` for `4.2`?
> A) `math.floor(4.2)`
> B) `math.ceil(4.2)`
> C) `int(4.2)`
> D) `round(4.2)`

**Answer:** B. `ceil` rounds up; `floor`, `int`, and `round` all return 4 here.

> Which converts a date object to a formatted string?
> A) `strptime`
> B) `strftime`
> C) `str()`
> D) `format()`

**Answer:** B. **f**ormat → `strftime`; **p**arse → `strptime`.

---

## Module 12 — Unit Testing with `unittest`

### Concept

The `unittest` module provides a framework for automatically checking that functions return what you expect. The exam tests the structure of a test class, the naming rule for test methods, and the most common assertion methods.

### Anchor: The Skeleton

```python
import unittest

class MyTests(unittest.TestCase):

    def test_territory(self):                # name MUST start with "test"
        self.assertEqual(a, b)
        self.assertTrue(condition)
        self.assertIn(item, collection)
        self.assertIs(a, b)                  # same object in memory

if __name__ == "__main__":
    unittest.main()
```

Rules to memorize:

- **The class inherits from `unittest.TestCase`.**
- **Every test method's name must start with `test`** (e.g., `test_area`, `test_login`). Names like `_test_area`, `area_test`, or `testcase_area` are **not** discovered as tests.
- The `if __name__ == "__main__":` block ensures `unittest.main()` runs only when the file is executed directly, not when imported.

### Anchor: Common Assertions

| Assertion                        | Passes When                                |
| -------------------------------- | ------------------------------------------ |
| `assertEqual(a, b)`              | `a == b`                                   |
| `assertNotEqual(a, b)`           | `a != b`                                   |
| `assertTrue(x)` / `assertFalse(x)` | `x` is truthy / falsy                    |
| `assertIn(x, collection)`        | `x` is in the collection                   |
| `assertIs(a, b)`                 | `a is b` (same object in memory)           |
| `assertIsNone(x)`                | `x is None`                                |

A bare `assert expression` (outside `unittest`) raises `AssertionError` only when the expression is false. When it's true, it produces no output.

### Self-Check

> Which method name will `unittest` actually run as a test?
> A) `def area_test(self):`
> B) `def _test_area(self):`
> C) `def test_area(self):`
> D) `def Test_area(self):`

**Answer:** C. The name must start with lowercase `test`.

> Which assertion checks that `a` and `b` refer to the **same object in memory**?
> A) `assertEqual(a, b)`
> B) `assertIs(a, b)`
> C) `assertIn(a, b)`
> D) `assertTrue(a == b)`

**Answer:** B. `assertIs` uses `is`, not `==`.

---

## Module 13 — Errors, Debugging, and Common Pitfalls

### Concept

The exam asks "what kind of error is this?" repeatedly. You must distinguish the three categories and recognize the small set of pitfalls that come up over and over.

### Anchor: The Three Error Categories

| Category          | When It Happens                                              | Examples                                            |
| ----------------- | ------------------------------------------------------------ | --------------------------------------------------- |
| **Syntax error**  | Python can't even parse the code; nothing runs                | Missing colon, unmatched paren, bad indentation     |
| **Runtime error** | Code parses but fails *during* execution                     | `ZeroDivisionError`, `IndexError`, `TypeError`      |
| **Logic error**   | Code runs without complaining but produces the wrong answer  | Wrong operator (`>` vs. `>=`), missing parentheses around an expression |

Logic errors are the most dangerous — there's nothing to read other than wrong output.

### Anchor: The Pitfall Drill List

These come up repeatedly across both practice exams:

1. Missing colon at the end of `if`/`for`/`while`/`def`/`class`.
2. Forgetting indentation under a control statement.
3. Using `=` (assignment) where `==` (comparison) is needed.
4. `True`/`False` written lowercase.
5. Using `int()` when decimals are needed (truncates).
6. Trying to modify a tuple (immutable).
7. Naming a unit-test method something other than `test_…`.
8. Forgetting to `import` a module before using it.
9. `randint(a, b)` (inclusive of `b`) confused with `randrange(a, b)` (exclusive of `b`).
10. Using `'w'` mode when you meant `'a'` — `'w'` overwrites.
11. Off-by-one with `range(n)` (stops at `n-1`).
12. Indexing past the end of a list (`IndexError`).
13. Forgetting parentheses around an expression so `*` wins over `+` when you needed the sum first.
14. Calling a function but not storing the return — `subtotal(500, .07)` discards the result.

### Self-Check

> Code runs and prints a number, but the number is wrong because parentheses were forgotten around an expression. What kind of error is this?
> A) Syntax error
> B) Runtime error
> C) Logic error
> D) Import error

**Answer:** C.

> Code crashes mid-run with `IndexError: list index out of range`. What kind of error is this?
> A) Syntax error
> B) Runtime error
> C) Logic error
> D) Compile error

**Answer:** B. Code parsed fine; the failure occurred during execution.

---

## Module 14 — Test-Taking Strategy and Final Review

### The Distractor-Autopsy Method

For every practice question, do this:

1. Pick your answer.
2. **For each *wrong* option, write one sentence explaining why it is wrong.**
3. Only then check the answer key.

If you can articulate why every distractor is wrong, you have actually mastered the concept. If you can't, that's where to study next.

### Reading Code Under Time Pressure

When a code block appears, before reading the answer choices:

1. **Find every colon and indent.** Spot syntax errors immediately.
2. **Identify each operator** — especially `=` vs. `==`, `is` vs. `==`, `/` vs. `//`.
3. **Trace the precedence** if there's arithmetic. Mentally insert parentheses.
4. **Walk the loop / conditional** by hand for the first one or two iterations.
5. **Then evaluate the answer choices.**

### One Sentence to Repeat During the Exam

Pick one of these and repeat it under your breath whenever you get stuck:

- *"`=` assigns; `==` compares; `is` identifies."*
- *"`range(n)` stops at n-1."*
- *"Lists are zero-indexed."*
- *"Tuples are immutable."*
- *"`w` overwrites; `a` appends."*
- *"Test methods must start with `test`."*

### Mock Quiz (12 Questions Across the Whole Exam)

Try these timed — about 75 seconds per question.

1. Which character starts a single-line comment?
2. What does `int(7.8)` evaluate to?
3. What does `10 // 3` evaluate to?
4. Given `a = [1,2]` and `b = a`, what is `a is b`?
5. How many iterations does `for i in range(5):` perform?
6. How is the last item of a 6-item list indexed?
7. What gets printed?
   ```python
   def square(n): return n * n
   square(4)
   print("done")
   ```
8. Which file mode appends without erasing?
9. Which block runs *regardless* of whether an exception was raised?
10. Which call rounds 4.2 up to 5 — `math.ceil` or `math.floor`?
11. Which test method name will `unittest` discover and run?
12. Forgetting parentheses around a sum so multiplication wins precedence — what kind of error?

#### Answer Key (cover until done)

1. **`#`** — Module 1.
2. **`7`** (truncates toward zero). — Module 2.
3. **`3`** (floor division). — Module 3.
4. **`True`** — same object. — Module 3.
5. **5** — values 0,1,2,3,4. — Module 5.
6. **`list[5]`** or `list[-1]`. — Module 7.
7. **`done`** — `square(4)` is called but its return is discarded. — Module 8.
8. **`"a"`** — Module 9.
9. **`finally`** — Module 10.
10. **`math.ceil`** — Module 11.
11. A name **starting with `test`**, e.g., `test_area`. — Module 12.
12. **Logic error** — code runs but returns the wrong value. — Module 13.

---

## Exam-Day Cheat Card

Read this on the morning of the exam. It's the whole guide compressed into a single paragraph:

> Python comments use `#`. Every `if`/`elif`/`else`/`for`/`while`/`def`/`class`/`try`/`except`/`finally` ends with `:` and uses indented bodies. `True`, `False`, `None` are capitalized. Variables are dynamically typed; conversion functions are `int()` (truncates toward zero), `float()`, `str()`, `bool()`. Lists, sets, and dicts are mutable; tuples and strings are immutable. Operators: `+ - * /` standard, `**` power, `//` floor division, `%` modulo. `=` assigns, `==` compares values, `is` compares identity (same object). Logical precedence: `not` → `and` → `or`. Membership uses `in` / `not in`; for dicts it tests keys. Compound assignment: `+=`, `-=`, `*=`, etc. Without parentheses, `*` and `/` happen before `+` and `-`. Conditional branches must be ordered most-restrictive-first when ranges overlap; use `pass` as a placeholder for empty bodies. `range(n)` produces `0…n-1`; `range(start, stop)` excludes `stop`; `range(start, stop, step)` strides. Use `for` for known iterations, `while` for unknown. `break` exits the loop; `continue` skips to the next iteration; `pass` does nothing. f-strings: `f"{var:0.2f}"`. Slicing is `[start:stop:step]` with `[::-1]` to reverse. Lists are zero-indexed; the last item is `[len-1]` or `[-1]`; `IndexError` if you go past the end. Tuples can't be modified. Sets dedupe and are unordered; dicts store key-value pairs and the `in` operator checks keys. Define functions with `def`, end the header in `:`, return with `return` (default is `None`); to keep the result, assign the call to a variable. Default parameters come last in the signature. Docstrings sit just below the `def` and are reachable via `func.__doc__`. `input()` always returns a string — wrap with `int()` or `float()` for numbers. File modes: `"r"` reads (must exist), `"w"` overwrites, `"a"` appends, `"r+"` does both; use `with open(...) as file:` to auto-close. `os.path.isfile`, `os.path.exists`, `os.remove`. `try`/`except`/`else`/`finally` — `finally` runs no matter what; `raise` (not `throw`) triggers an exception. Common exceptions: `ZeroDivisionError`, `IndexError`, `KeyError`, `ValueError`, `TypeError`, `FileNotFoundError`. `math.ceil`, `math.floor`, `math.sqrt`, `math.pow`, `math.fabs`, `math.pi`. `random.choice`, `random.shuffle`, `random.randint(a,b)` inclusive, `random.randrange(a,b,step)` exclusive of `b`, `random.random()` 0–1. `datetime.datetime.now()`, `strftime` formats to string, `strptime` parses from string. `sys.argv` lists command-line arguments with `argv[0]` as the script name. `unittest.TestCase` subclass; method names must start with `test`; `assertEqual`, `assertTrue`, `assertIn`, `assertIs`. Three error categories: syntax (won't parse), runtime (parses but crashes), logic (runs but wrong answer).

---

## Master Glossary

**`__doc__`** — attribute holding a function or class's docstring; access via `funcname.__doc__`.

**`assertEqual` / `assertTrue` / `assertIn` / `assertIs`** — `unittest.TestCase` methods that pass when their condition holds.

**Boolean** — the `bool` type. Only `True` and `False` (capitalized).

**`break`** — exits the enclosing loop immediately.

**Comment** — non-executed note starting with `#`.

**Compound Assignment** — operators like `+=`, `-=`, `*=` that update and reassign in one step.

**`continue`** — skips to the next iteration of the enclosing loop.

**`datetime`** — module for dates and times. `strftime` → string, `strptime` → datetime object.

**`def`** — keyword that defines a function.

**Default Parameter** — a parameter with a fall-back value used when the caller omits the argument.

**Dictionary (`dict`)** — collection of key-value pairs; `in` tests keys.

**Docstring** — triple-quoted string immediately under a `def` or `class`; documents the object.

**Dynamic Typing** — Python infers a variable's type from the assigned value; no type declarations needed.

**`else` (loop / try)** — runs only if no exception was raised (`try`) or the loop completed without `break`.

**`except`** — block that handles a specific raised exception.

**Exception** — a runtime error object; common ones include `ZeroDivisionError`, `IndexError`, `KeyError`, `ValueError`, `TypeError`, `FileNotFoundError`.

**f-string** — string prefixed with `f` allowing inline `{variable}` substitutions; e.g., `f"{x:0.2f}"`.

**`finally`** — block that runs whether or not an exception was raised; used for cleanup.

**Floor Division (`//`)** — division that drops the decimal portion.

**`for` loop** — iterates a known collection or range.

**Function** — a reusable block of code defined with `def` and called by name.

**Identity (`is`)** — checks whether two names refer to the same object in memory.

**Immutable** — value that cannot be modified after creation (`int`, `float`, `str`, `bool`, `tuple`).

**Indentation** — required whitespace defining a block in Python; typically 4 spaces.

**`IndexError`** — raised when accessing a list index that doesn't exist.

**`input()`** — reads a line from the user; **always returns a string**.

**`int()` / `float()` / `str()` / `bool()`** — type-conversion functions.

**Logic Error** — code runs without complaint but produces the wrong result.

**`math` module** — math functions: `math.pi`, `math.ceil`, `math.floor`, `math.sqrt`, `math.pow`, `math.fabs`.

**Membership Operator** — `in` / `not in`; tests presence in a collection (keys for dicts).

**Modulo (`%`)** — remainder of integer division.

**Mutable** — value that can be modified after creation (`list`, `set`, `dict`).

**`os` / `os.path`** — modules for filesystem operations: `isfile`, `exists`, `remove`.

**`pass`** — placeholder statement; does nothing but satisfies the requirement that a block be non-empty.

**`pydoc`** — tool that generates documentation from Python modules.

**`raise`** — keyword that manually triggers an exception.

**`random` module** — `choice`, `shuffle`, `randint(a,b)` (inclusive), `randrange(a,b,step)` (exclusive of `b`), `random()`.

**`range(start, stop, step)`** — produces a sequence of integers; `stop` is excluded.

**`return`** — sends a value back from a function; without it, the function returns `None`.

**Runtime Error** — error that occurs while the program is running (e.g., `ZeroDivisionError`).

**Set** — unordered collection of unique values; written with `{}`.

**Slicing** — `[start:stop:step]` notation for sequences. Negative steps walk backward.

**`strftime`** — formats a date/datetime as a string.

**`strptime`** — parses a string into a date/datetime.

**`sys.argv`** — list of command-line arguments passed to the script; `argv[0]` is the script name.

**Syntax Error** — code that Python cannot parse (missing colon, bad indentation).

**Tuple** — ordered, immutable collection; written with `()`.

**`unittest`** — built-in testing framework; tests are methods of a `TestCase` subclass whose names start with `test`.

**`while` loop** — repeats while a condition is true; checked before each iteration.

**`with open(...) as file:`** — context-managed file open that auto-closes the file at block end.

**Zero-Based Indexing** — Python collections start at index 0; the last item of a length-N list is at index N-1 (or -1).
