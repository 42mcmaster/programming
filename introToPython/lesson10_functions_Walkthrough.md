# Lesson 10 — Functions and Docstrings (Teacher Walkthrough)

> **Teacher-only file.** ~20-minute script.

**Student deliverable:** `lesson10_functions_Task.ipynb`
**ODE standards touched:** 5.3.9 (create and call functions), 5.4.2, 5.5.5 (naming, comments, docstrings), 5.5.6 (algorithmic thinking).

---

## Learning Objectives

1. Define a function using `def`.
2. Pass values to a function through parameters.
3. Return a value with `return`.
4. Write a docstring explaining what the function does.
5. Call a function and use its return value.

---

## Section 1 — Why functions? (3 minutes)

**Say to the class:**

> "Everything we've built so far has been one long script, top to bottom. That's fine for short programs, but real programs get long — and repetitive. When you find yourself doing the same thing over and over, you should **wrap it up** and give it a name. That's what a function does."

> "You've already been **calling** functions all along. `print()` is a function. `input()` is a function. `int()` and `float()` are functions. Today you learn how to **write your own**."

Show the motivation:

```python
# Without a function — repeated code
print("Hello, Alex!")
print("Welcome to Python class.")

print("Hello, Jordan!")
print("Welcome to Python class.")

print("Hello, Sam!")
print("Welcome to Python class.")
```

```python
# With a function — no repetition
def greet(name):
    print(f"Hello, {name}!")
    print("Welcome to Python class.")

greet("Alex")
greet("Jordan")
greet("Sam")
```

> "Same output. But the greeting is written once. If I want to change it, I change it in one place, not three."

---

## Section 2 — The anatomy of a function (5 minutes)

Put this on the board:

```python
def FUNCTION_NAME(PARAMETERS):
    """Docstring — what does this function do?"""
    <body — indented>
    return VALUE
```

**Each piece:**

1. `def` — Python keyword. "I'm defining a function."
2. `FUNCTION_NAME` — what you call this function. Same naming rules as variables: letters, digits, underscores, no spaces, no leading digit.
3. Parentheses `()` — always required, even if there are no parameters.
4. `PARAMETERS` — names for the inputs the function will accept (can be empty, one, or many).
5. Colon `:` at the end.
6. The body is indented 4 spaces.
7. `return` sends a value back to the caller.

### Simple function with no parameters

```python
def sayHello():
    print("Hello!")

sayHello()      # Call it
sayHello()      # Can call as many times as we want
```

### Function with one parameter

```python
def greet(name):
    print(f"Hello, {name}!")

greet("Alex")
greet("Jordan")
```

**Say:**

> "`name` is the **parameter** — the placeholder in the function definition. When we **call** `greet(\"Alex\")`, the value `\"Alex\"` is the **argument** that gets plugged into `name`. The function only knows about `name`."

### Function with multiple parameters

```python
def greetWithAge(name, age):
    print(f"Hello, {name}! You are {age} years old.")

greetWithAge("Alex", 17)
greetWithAge("Jordan", 18)
```

---

## Section 3 — `return` vs just `print` (5 minutes)

**This is a really important distinction. Pause and cover slowly.**

> "There are TWO very different things a function can do:"
>
> 1. **Print** something (display output to the user).
> 2. **Return** something (hand a value back to the code that called it).
>
> "These are not the same."

### A function that prints

```python
def addAndPrint(a, b):
    total = a + b
    print(total)          # Shows on screen

addAndPrint(3, 5)         # Prints 8 to screen
```

### A function that returns

```python
def add(a, b):
    return a + b          # Hands the value back

result = add(3, 5)        # result = 8
print(result * 2)         # 16
```

**Say:**

> "The difference is huge. `addAndPrint` displays a number on the screen but gives nothing back — you can't use the answer in a calculation. `add` does the calculation and hands the result back as a value. You can save it, print it, multiply it, pass it to another function."

> "As a rule of thumb: **prefer `return` over `print`** inside your functions. Let the caller decide what to do with the result."

### What happens when a function doesn't return anything

```python
def shout(word):
    print(word.upper())

result = shout("hello")
print(result)          # None
```

> "If a function doesn't have a `return` statement, Python returns the special value `None` by default. `None` means 'nothing.' That's Python telling you 'this function didn't hand you back anything.'"

### `return` ends the function

```python
def test(x):
    if x > 0:
        return "positive"
    return "not positive"    # Only reached if x <= 0
    print("this never prints")   # Dead code
```

> "As soon as `return` fires, the function is done. Any code after it is skipped."

---

## Section 4 — Docstrings (3 minutes)

**Say:**

> "Every function you write should have a **docstring** — a short string, in triple quotes, that says what the function does. It goes on the line right after the `def`."

```python
def calculateArea(length, width):
    """Return the area of a rectangle given its length and width."""
    return length * width
```

**Why docstrings matter:**

1. Future-you will thank you when you come back in a week and don't remember what the function does.
2. `help()` will show them. Try `help(print)` in a cell — that's what a good docstring looks like in Python's built-ins.
3. I will grade on them. Every function in your task today needs one.

### Style

- One-line docstrings are fine for simple functions.
- Use complete sentences. Start with a verb in present tense: "Return the…", "Print the…", "Compute the…".

```python
def celsiusToFahrenheit(celsius):
    """Convert a Celsius temperature to Fahrenheit and return it."""
    return celsius * 9/5 + 32
```

---

## Section 5 — Default parameters (2 minutes)

**Say:**

> "You can give a parameter a **default value**. That way the caller doesn't have to supply it if they don't want to."

```python
def greet(name="Friend"):
    """Greet the given name, or 'Friend' if no name is provided."""
    print(f"Hello, {name}!")

greet()              # Hello, Friend!
greet("Alex")        # Hello, Alex!
```

> "Rule: default parameters go at the **end** of the parameter list, after any non-default parameters."

```python
# OK
def order(item, quantity=1):
    ...

# NOT OK — SyntaxError
# def order(quantity=1, item):
#     ...
```

---

## Section 6 — Live build (2 minutes)

Build this with the class:

```python
def calculateBMI(weightLbs, heightInches):
    """Return the Body Mass Index given weight in pounds and height in inches."""
    return (weightLbs / (heightInches ** 2)) * 703

def bmiCategory(bmi):
    """Return the BMI category for a BMI value (underweight/normal/overweight/obese)."""
    if bmi < 18.5:
        return "Underweight"
    elif bmi < 25:
        return "Normal"
    elif bmi < 30:
        return "Overweight"
    else:
        return "Obese"

# Use them together
weight = float(input("Weight (lbs): "))
height = float(input("Height (inches): "))

bmi = calculateBMI(weight, height)
category = bmiCategory(bmi)

print(f"Your BMI is {bmi:.1f} ({category}).")
```

**Point out:**

> "Two small, single-purpose functions. One returns a number. One returns a string. The main code ties them together. That's the normal way to build programs: small functions that do one thing, composed together."

---

## Section 7 — Common Mistakes (1 minute)

**Mistake 1: Forgot the colon.**

```python
def greet(name)        # SyntaxError — missing colon
def greet(name):       # Correct
```

**Mistake 2: Didn't indent the body.**

```python
def greet(name):
print(f"Hello, {name}")   # IndentationError
```

**Mistake 3: Using a parameter name outside the function.**

```python
def greet(name):
    print(name)

print(name)    # NameError — name only exists inside greet()
```

> "Parameters are **local** to the function. They don't exist outside it."

**Mistake 4: Forgetting `return`.**

```python
def add(a, b):
    a + b        # Calculated but not returned

result = add(3, 5)
print(result)    # None — the function didn't hand anything back
```

Fix:

```python
def add(a, b):
    return a + b
```

**Mistake 5: Calling without parentheses.**

```python
def sayHi():
    print("Hi")

sayHi        # Does nothing — this just refers to the function, doesn't call it
sayHi()      # Calls it
```

---

## Section 8 — Quick Recap (1 minute)

Ask:

1. "What keyword defines a function?"
2. "What's the difference between a parameter and an argument?"
3. "What's the difference between `return` and `print`?"
4. "What's a docstring? Where does it go?"

Hand off:

> "Open `lesson10_functions_Task.ipynb`. Every function you write today needs a docstring."

---

## Vocabulary introduced today

- **Function** — a reusable block of code with a name.
- **def** — keyword that starts a function definition.
- **Parameter** — a variable name in the function's parentheses, holds an input.
- **Argument** — the actual value passed when calling the function.
- **return** — sends a value back to the caller and ends the function.
- **Docstring** — a triple-quoted string right after `def` that documents the function.
- **Default parameter** — a parameter with a preset value used if the caller omits it.
- **Local variable** — a variable that only exists inside the function it's defined in.
- **None** — Python's special value meaning 'nothing'; returned by default.
