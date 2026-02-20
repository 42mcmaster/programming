---
marp: true
theme: default
class: invert
paginate: true
---

# Lesson 08: Data Structures
## Dictionaries, Tuples, and Sets
### Medina County Career Center
### Instructor: Ryan McMaster

---

## Dictionaries: Like C Structs

```python
# C: struct RGBTRIPLE { BYTE rgbtRed, rgbtGreen, rgbtBlue; }
# Python:
color = {
    'red': 255,
    'green': 128,
    'blue': 64
}
print(color['red'])  # 255
```

**Key insight:** A dict is a struct where you add fields on the fly using strings or numbers as keys.

---

## Dictionary Operations

```python
# Create
student = {'name': 'Alice', 'gpa': 3.8, 'grade': 10}

# Access
print(student['name'])  # Alice

# Modify
student['gpa'] = 3.9

# Add new field
student['email'] = 'alice@school.edu'

# Delete
del student['email']

# Safe access (no KeyError)
age = student.get('age', 18)  # Returns 18 if 'age' missing
```

---

## Looping Through Dictionaries

```python
student = {'name': 'Alice', 'gpa': 3.8, 'grade': 10}

# .keys(), .values(), .items()
for key in student.keys():
    print(key)

for value in student.values():
    print(value)

for key, value in student.items():
    print(f"{key}: {value}")
```

---

## Tuples: Immutable Sequences

```python
# Create
point = (10, 20)
rgb = (255, 128, 64)

# Access (like list)
print(point[0])  # 10

# Cannot modify (immutable)
# point[0] = 15  # ERROR!

# Packing and unpacking
x, y = point

# Multiple return values
def get_bounds():
    return (0, 100)
```

**Use tuples:** When data should not change, as dict keys, or for multiple returns.

---

## Sets: Unique Values

```python
# Create
colors = {'red', 'green', 'blue', 'red'}
print(colors)  # {'red', 'green', 'blue'} - duplicates removed

# Add and remove
colors.add('yellow')
colors.remove('red')

# Operations
set1 = {1, 2, 3}
set2 = {2, 3, 4}
print(set1 | set2)  # Union: {1, 2, 3, 4}
print(set1 & set2)  # Intersection: {2, 3}
print(set1 - set2)  # Difference: {1}
```

**Use sets:** Remove duplicates, check membership fast, mathematical operations.

---

## Choosing Data Structures

| Type | Ordered | Mutable | Duplicates | Use Case |
|------|---------|---------|-----------|----------|
| **list** | Yes | Yes | Yes | Sequences, ordered data |
| **tuple** | Yes | No | Yes | Immutable sequences, multiple returns |
| **dict** | (ordered in 3.7+) | Yes | No (keys) | Named fields, lookups |
| **set** | No | Yes | No | Unique values, fast membership |

---

## Nested Data Structures

```python
# List of dictionaries (like a database table)
students = [
    {'name': 'Alice', 'gpa': 3.8},
    {'name': 'Bob', 'gpa': 3.5},
    {'name': 'Charlie', 'gpa': 3.9}
]

# Access
print(students[0]['name'])  # Alice

# Loop and compute
total_gpa = sum(s['gpa'] for s in students)
average = total_gpa / len(students)

# Dictionary of lists
grades = {'Alice': [92, 88, 95], 'Bob': [78, 85, 81]}
```

---

## JSON Basics

```python
import json

# Python dict <-> JSON string
student = {'name': 'Alice', 'gpa': 3.8, 'grades': [92, 88, 95]}

json_str = json.dumps(student)  # to JSON string
parsed = json.loads(json_str)   # from JSON string

# File I/O
with open('students.json', 'w') as f:
    json.dump(students, f)
```

**JSON:** A universal format for data exchange. Looks like Python dicts!

---

## Summary

- **Dictionaries:** Named fields (like C structs), key-value pairs
- **Tuples:** Immutable sequences, multiple returns
- **Sets:** Unique values, mathematical operations
- **Nested:** List of dicts for structured data
- **JSON:** Store/exchange dict-like data as text

**Next:** Apply these in real projects!
