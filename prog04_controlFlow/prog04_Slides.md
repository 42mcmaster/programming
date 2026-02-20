---
marp: true
theme: default
class: invert
paginate: true
---

# Lesson 04: Control Flow
## Programming
### Medina County Career Center
---

# Conditionals in Python
## Boolean Values: True and False

- Python uses **True** and **False** (capitalized, unlike C)
- Comparison operators (same as C):
  - `==` (equal), `!=` (not equal)
  - `<` (less than), `>` (greater than)
  - `<=` (less than or equal), `>=` (greater than or equal)

```python
age = 16
isAdult = age >= 18  # isAdult is False
```

---

# if / elif / else

Python uses **indentation** instead of braces:

```python
score = 85

if score >= 90:
    print("Grade: A")
elif score >= 80:
    print("Grade: B")
elif score >= 70:
    print("Grade: C")
else:
    print("Grade: F")
```

**Remember:** Indent with 4 spaces (not tabs)

---

# Logical Operators

Python uses words instead of C symbols:

| Python | C |
|--------|---|
| `and` | `&&` |
| `or` | `\|\|` |
| `not` | `!` |

```python
age = 16
hasLicense = True

if age >= 16 and hasLicense:
    print("You can drive!")

if not hasLicense:
    print("Get your license first")
```

---

# Loops: for loop

Compare C and Python:

**C:**
```c
for (int i = 0; i < 5; i++) {
    printf("%d\n", i);
}
```

**Python:**
```python
for i in range(5):
    print(i)
```

`range(5)` creates 0, 1, 2, 3, 4

---

# Loops: for with Lists and Strings

```python
# Loop over a list
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)

# Loop over a string
word = "Python"
for letter in word:
    print(letter)

# range with start, stop, step
for i in range(1, 10, 2):  # 1, 3, 5, 7, 9
    print(i)
```

---

# while Loop

Same concept as C, but simpler syntax:

```python
count = 0
while count < 5:
    print(count)
    count = count + 1
```

**Sentinel-controlled loop:**
```python
while True:
    userInput = input("Enter 'quit' to exit: ")
    if userInput == "quit":
        break  # Exit the loop
    print("You entered:", userInput)
```

---

# Loop Patterns: Accumulator & Counting

**Accumulator (running total):**
```python
total = 0
for i in range(1, 6):
    total = total + i  # Add to running total
print("Sum:", total)  # 15
```

**Counting:**
```python
count = 0
for num in [2, 4, 6, 8]:
    if num > 4:
        count = count + 1
print("Numbers > 4:", count)  # 2
```

---

# break and continue

```python
# break: exit loop immediately
for i in range(10):
    if i == 5:
        break  # Stop the loop
    print(i)  # Prints 0, 1, 2, 3, 4

# continue: skip to next iteration
for i in range(5):
    if i == 2:
        continue  # Skip this iteration
    print(i)  # Prints 0, 1, 3, 4
```

---

# Summary: Key Differences from C

| Concept | C | Python |
|---------|---|--------|
| Boolean | true/false (lowercase) | True/False (capitalized) |
| Blocks | `{ }` braces | **indentation** |
| if/else | `if (x) { }` | `if x:` (no parens) |
| and/or | `&&` / `\|\|` | `and` / `or` |
| for loop | `for(i=0; i<n; i++)` | `for i in range(n):` |
| while | `while (x) { }` | `while x:` |

**Practice:** Convert your C code to Python!
