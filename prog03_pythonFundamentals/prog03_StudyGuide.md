# prog03 Study Guide: Python Fundamentals

**Medina County Career Center**
**Instructor: Ryan McMaster**

---

## Key Concepts & Terminology

### 1. **Interpreter**
A program that reads Python code line-by-line and executes it directly (no compilation needed).

### 2. **Dynamic Typing**
Variables can hold any type of value; the type is determined at runtime, not declared in advance.

### 3. **IDLE**
Python's Integrated Development and Learning Environment — a simple editor to write and run `.py` files.

### 4. **print()**
Function that outputs text to the console.

### 5. **input()**
Function that reads a line of text from the user; always returns a string.

### 6. **f-string (formatted string)**
A Python string literal with `f` prefix that allows embedding expressions in curly braces.
Example: `f"Hello, {name}! You are {age} years old."`

### 7. **int**
Data type for whole numbers: 5, -10, 0.

### 8. **float**
Data type for decimal numbers: 3.14, -2.5, 0.0.

### 9. **str (string)**
Data type for text: "hello", "Alice", "123" (as text, not a number).

### 10. **bool (boolean)**
Data type for True or False.

### 11. **type()**
Built-in function that returns the data type of a value.
Example: `type(5)` returns `<class 'int'>`.

### 12. **camelCase**
Naming convention where the first word is lowercase and subsequent words start with uppercase.
Example: `studentName`, `isStudent`, `gradeLevel`.

### 13. **Comment**
A line of code that starts with `#` and is ignored by Python; used to explain code.
Example: `# This is a comment`

### 14. **Variable**
A named storage location that holds a value.

### 15. **Assignment**
Using `=` to give a variable a value.
Example: `x = 10`

### 16. **Type Conversion**
Converting a value from one data type to another using functions like `int()`, `float()`, or `str()`.
Example: `userInput = input()` returns a string; `age = int(userInput)` converts it to int.

### 17. **Arithmetic Operators**
`+` (addition), `-` (subtraction), `*` (multiplication), `/` (division — returns float), `//` (integer division), `%` (modulo/remainder).

### 18. **String Concatenation**
Combining strings using `+`.
Example: `greeting = "Hello, " + name`

---

## Quick Reference: Python vs C

| Feature | C | Python |
|---------|---|--------|
| **Compilation** | Required | No — interpreted |
| **Syntax** | Braces `{}`, semicolons `;` | Indentation, no semicolons |
| **Types** | Must declare: `int x = 5;` | Dynamic: `x = 5` |
| **Output** | `printf("x = %d", x);` | `print(f"x = {x}")` |
| **Input** | `scanf()` — complex | `input()` — returns string |
| **Division** | `10 / 4 = 2` (integer) | `10 / 4 = 2.5` (float) |

---

## Common Python Syntax

```python
# Comments
# This is a comment

# Variables (no type declaration)
name = "Alice"
age = 16
gpa = 3.8
isStudent = True

# Type checking
print(type(name))     # <class 'str'>

# Input
userAge = input("How old are you? ")  # returns string "16"
userAge = int(userAge)                # convert to int 16

# Arithmetic
total = 10 + 5
result = 20 / 4           # 5.0 (float)
result = 20 // 4          # 5 (integer division)
remainder = 20 % 3        # 2

# String concatenation
fullMessage = "Hello, " + name

# F-strings (recommended)
message = f"Hello, {name}! You are {age}."

# Output
print(message)
```

---

## Alignment with Ohio Academic Standards

**ODE: 5.2.1** — Understand and use fundamental programming concepts.
**ODE: 5.2.3** — Implement programming solutions using standard data types and control structures.

---

## Practice Tips

1. **Run early, run often** — Python gives instant feedback. Don't be afraid to test code.
2. **Use f-strings** — They're cleaner than string concatenation.
3. **Remember: input() returns a string** — Always convert with int() or float() if needed.
4. **Indentation matters** — One space off breaks the code.
5. **Use camelCase for variable names** — Makes code readable.

