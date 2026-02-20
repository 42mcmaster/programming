---
marp: true
theme: default
class: invert
paginate: true
---

# Lesson 03: Python Fundamentals
## Programming
### Medina County Career Center
**Instructor: Ryan McMaster**

---

## Sub-Lesson 03a — Python vs C: A New World

**Key Differences:**
- **Interpreted** — no compilation step, just run it
- **No braces, no semicolons** — indentation defines code blocks
- **Dynamic typing** — no need to declare types
- **print()** — outputs text to console
- **f-strings** — modern, readable way to format output

```python
# C required: int x = 5; cout << "x = " << x;
# Python is simple:
x = 5
print(f"x = {x}")
```

---

## Running Python

**IDLE (built-in)**
- Click Python icon, choose "New File"
- Write code, save as `.py`
- Run: press F5 or Tools → Run Module

**VS Code**
- Install Python extension
- Write `.py` file, click "Run" button

**Jupyter Notebook** (we'll use this)
- Cell-based: write, run, see output immediately

---

## Sub-Lesson 03b — Variables, Types, and I/O

**Variables** (no declaration needed)
```python
name = "Alice"       # str
age = 16             # int
gpa = 3.8            # float
isStudent = True     # bool
```

**Type Checking**
```python
print(type(name))    # <class 'str'>
print(type(age))     # <class 'int'>
```

**Input & Conversion**
```python
userAge = input("What is your age? ")  # returns string
userAge = int(userAge)                 # convert to int
```

---

## Arithmetic & Operators

```python
# Same as C:
a = 10 + 5       # 15
b = 10 - 3       # 7
c = 4 * 5        # 20
d = 20 / 4       # 5.0 (always float!)
e = 20 // 4      # 5 (integer division)
f = 20 % 3       # 2 (modulo)

# String concatenation:
greeting = "Hello, " + name
```

---

## Sub-Lesson 03c — Writing Real Programs

**Program Structure**
```python
# 1. Comments & imports
# 2. Constants (if needed)
# 3. Get input
# 4. Process (calculate)
# 5. Output (f-strings)
```

**Why Python is Easier Than C**
- No type declarations → fewer syntax errors
- No memory management → no pointers, malloc, free
- No compilation → instant feedback
- Focus on the **logic**, not the mechanics

---

## Temperature Converter Example

```python
# Get input
celsius = float(input("Enter temperature in Celsius: "))

# Calculate
fahrenheit = (celsius * 9/5) + 32

# Output
print(f"{celsius}°C = {fahrenheit}°F")
```

In C, you needed type declarations, header files, printf syntax. Here? Just logic.

---

## Key Takeaways

1. Python is **interpreted** — write and run
2. **Indentation** replaces braces
3. **Dynamic typing** — variables hold any type
4. **input()** returns a string — convert with int(), float()
5. **f-strings** make output clean and readable
6. Focus on **logic**, not syntax

**Next: Let's write some Python!**

