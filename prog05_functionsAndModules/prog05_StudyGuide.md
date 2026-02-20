# Prog05: Functions & Modules — Study Guide

**Course**: Programming (CTE) | **School**: Medina County Career Center
**Instructor**: Ryan McMaster | **Standards**: ODE 5.2.1, 5.2.2, 5.2.3

---

## Key Concepts

### 1. **Function**
A reusable block of code that performs a specific task. Functions take input (parameters), process it, and return output.
```python
def add(a, b):
    return a + b
```

### 2. **def**
Python keyword used to define a function. Required at the start of every function definition.
```python
def myFunction():
    print("Hello")
```

### 3. **Parameter**
A variable in a function definition that represents input the function will receive.
```python
def add(a, b):  # a and b are parameters
    return a + b
```

### 4. **Argument**
The actual value passed to a function when it is called.
```python
add(3, 5)  # 3 and 5 are arguments
```

### 5. **Return**
The value a function sends back to the code that called it. Use `return` keyword.
```python
def multiply(x, y):
    return x * y
result = multiply(4, 5)  # result = 20
```

### 6. **Default Parameter**
A parameter with a preset value. Used if no argument is provided.
```python
def greet(name="Friend"):
    print(f"Hello, {name}!")
greet()  # prints "Hello, Friend!"
greet("Alice")  # prints "Hello, Alice!"
```

### 7. **Keyword Argument**
An argument passed to a function using the parameter name.
```python
def describe(name, age):
    print(f"{name} is {age} years old")
describe(age=25, name="Bob")  # keyword arguments
```

### 8. **Docstring**
A string that documents what a function does. Goes immediately after `def` line.
```python
def calculateArea(radius):
    """Calculate the area of a circle given its radius."""
    import math
    return math.pi * radius ** 2
```

### 9. **Scope**
The region of code where a variable can be accessed. Two main types: local and global.

### 10. **Local Variable**
A variable defined inside a function. Only accessible within that function.
```python
def myFunc():
    localVar = 10  # only exists inside myFunc
    print(localVar)
```

### 11. **Global Variable**
A variable defined outside all functions. Accessible anywhere in the program (use sparingly).
```python
globalVar = 100  # accessible everywhere
def myFunc():
    print(globalVar)  # can read it
```

### 12. **Module**
A Python file containing reusable code (functions, variables, classes). Can be imported into other programs.
```python
# Save in mathHelpers.py
def add(a, b):
    return a + b

# In another file:
import mathHelpers
mathHelpers.add(3, 5)  # returns 8
```

### 13. **import**
Statement to load a module into your program.
```python
import math
import random
```

### 14. **from...import**
Import specific items from a module to avoid typing the module name repeatedly.
```python
from math import sqrt, pi
from random import randint
sqrt(25)  # instead of math.sqrt(25)
```

### 15. **math module**
Built-in Python module with mathematical functions and constants.
```python
import math
math.sqrt(16)  # 4.0
math.pi  # 3.14159...
math.ceil(3.2)  # 4
math.floor(3.7)  # 3
```

### 16. **random module**
Built-in Python module for generating random numbers and making random selections.
```python
from random import randint, choice, shuffle
randint(1, 6)  # random integer between 1 and 6
choice([1, 2, 3, 4])  # randomly pick from list
```

### 17. **randint**
Function from random module. Returns random integer in given range (inclusive).
```python
from random import randint
dice = randint(1, 6)
```

### 18. **Type Hint**
Optional notation showing what type a parameter or return value should be. Not enforced by Python.
```python
def add(a: int, b: int) -> int:
    return a + b
```

---

## Quick Reference

| Task | Code |
|------|------|
| Define function | `def myFunc(param1, param2):` |
| Return value | `return result` |
| Default parameter | `def greet(name="Friend"):` |
| Call with keyword | `greet(name="Alice")` |
| Access global variable | `global myVar` (inside function, if modifying) |
| Import module | `import math` or `from math import sqrt` |
| Generate random int | `from random import randint; randint(1, 10)` |
| Use docstring | `"""Explain function here."""` (first line of function) |

---

## Comparison: C vs Python

| Feature | C | Python |
|---------|---|--------|
| Function signature | `int add(int a, int b)` | `def add(a, b):` |
| Type declarations | Required | Optional (type hints) |
| Return statement | `return x;` | `return x` |
| Default parameters | Not available | `def greet(name="World"):` |
| Documentation | Comments `//` or `/* */` | Docstrings `"""..."""` |

---

## Study Tips

1. **Practice writing functions** — Start with simple ones (add, subtract), then build complexity.
2. **Use docstrings** — Always document what your function does.
3. **Understand scope** — Test by printing variables inside and outside functions.
4. **Explore modules** — Try `help(math)` or `help(random)` in Python interpreter.
5. **Think in components** — Break large programs into smaller functions.

---
