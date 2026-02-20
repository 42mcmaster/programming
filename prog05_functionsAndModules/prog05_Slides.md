---
marp: true
theme: default
class: invert
paginate: true
---

# Lesson 05: Functions & Modules
## Programming
### Medina County Career Center
**Instructor: Ryan McMaster**

---

## Sub-Lesson 05a: Defining Functions
- Recall C: `int add(int a, int b) { ... }`
- Python: `def add(a, b): ...` (no type declarations required)
- Parameters vs Arguments
- Return values
- Default parameter values
- Keyword arguments
- Docstrings for documentation

---

## Function Basics
```python
# Function definition
def greet(name="World"):
    """This is a docstring. It explains what the function does."""
    message = f"Hello, {name}!"
    return message

# Function calls
result = greet()
result = greet("Alice")
result = greet(name="Bob")
```
- `def`: keyword to define a function
- `name="World"`: default parameter
- `name="Bob"`: keyword argument

---

## Sub-Lesson 05b: Scope and Modules
**Scope**: Where a variable can be used
- Local variables: defined inside functions
- Global variables: defined outside functions
- The `global` keyword (use sparingly)

**Modules**: Python files with reusable code
- `import math` — use as `math.sqrt(16)`
- `from math import sqrt` — use as `sqrt(16)`
- `from random import randint, choice`

---

## Working with Modules
```python
import math
from random import randint, choice

# Math module
area = math.pi * 5 ** 2
sqrt_value = math.sqrt(25)

# Random module
dice_roll = randint(1, 6)
choice_result = choice([1, 2, 3, 4, 5, 6])
```
**Note**: You can write your own modules by saving functions in a `.py` file!

---

## Sub-Lesson 05c: Putting It Together
- Functions calling other functions
- Building multi-function programs
- Code organization
- Testing with print statements

Example: Calculator program with separate add, subtract, multiply, divide functions

---

## Key Takeaways
1. Functions make code reusable and readable
2. Python syntax is simpler than C (no type declarations)
3. Scope matters — understand local vs global
4. Modules provide pre-built functionality
5. Good organization = maintainable code

---

## Learning Objectives (ODE 5.2.1, 5.2.2, 5.2.3)
✓ Define and call functions with parameters and return values
✓ Use default and keyword arguments
✓ Understand variable scope
✓ Import and use modules
✓ Write and import custom modules

---
