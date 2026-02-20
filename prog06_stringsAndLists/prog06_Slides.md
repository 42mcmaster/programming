---
marp: true
theme: default
class: invert
paginate: true
---

# Lesson 06: Strings & Lists
## Programming
### Medina County Career Center
#### Instructor: Ryan McMaster

---

## What We'll Learn

- **String Methods & Slicing** — powerful built-in tools
- **Lists** — mutable, dynamic collections
- **Data Processing** — splitting, joining, parsing text
- **Comparison to C** — how Python makes things easier

---

## Strings in Python (06a)

- **Indexing**: `s[0]`, `s[-1]`, `s[2:5]`
- **Slicing**: `s[::-1]` reverses, `s[1:]` from index 1
- **Key Methods**: `.upper()`, `.lower()`, `.strip()`, `.split()`, `.join()`
- **Search**: `.find()`, `.replace()`, `.count()`
- **Check**: `.startswith()`, `.endswith()`
- **Immutable** — can't modify in place (unlike C char arrays)

---

## Lists in Python (06b)

- **Create**: `myList = [1, 2, 3]` or `myList = []`
- **Access**: `myList[0]`, `myList[-1]`, slicing works the same
- **Modify**: `.append()`, `.insert()`, `.remove()`, `.pop()`
- **Sort & Reverse**: `.sort()`, `.reverse()`
- **Search**: `.index()`, `.count()`
- **Mutable** — change elements anytime
- **List Comprehension**: `[x*2 for x in myList]`

---

## C vs Python: Strings

C:
```c
char str[50];  // fixed size
int len = strlen(str);  // manual
```

Python:
```python
str = "hello"
len(str)  # just call len()
```

**Why Python wins**: No buffer overflows, no manual length tracking

---

## C vs Python: Arrays/Lists

C:
```c
int arr[100];  // fixed size forever
// realloc() if you need more
```

Python:
```python
myList = []
myList.append(5)  # grows automatically!
```

**Why Python wins**: Dynamic sizing, no malloc/free headaches

---

## Data Processing (06c)

- **Split strings into lists**: `"a,b,c".split(",")`
- **Join lists into strings**: `",".join(["a", "b", "c"])`
- **Nested lists**: 2D data (like C 2D arrays)
- **Real examples**: word count, CSV parsing, grade books
- **Sorting & searching**: instant with `.sort()`, `.index()`

---

## Key Takeaway

Python's string and list tools are **huge upgrades** from C:
- No manual memory management
- Rich built-in methods
- Clean syntax (slicing, comprehensions)
- Less code, fewer bugs
