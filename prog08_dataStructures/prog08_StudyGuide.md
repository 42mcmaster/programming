# Lesson 08: Data Structures — Study Guide

**Course:** CTE Programming
**School:** Medina County Career Center
**Instructor:** Ryan McMaster
**Standards:** ODE 5.2.1, 5.3.5

---

## Key Terms

### 1. **Dictionary**
A collection of key-value pairs enclosed in curly braces `{}`. Each key maps to a value. Like a C struct with named fields you can add dynamically.
- **Example:** `student = {'name': 'Alice', 'gpa': 3.8}`

### 2. **Key**
The unique identifier in a key-value pair. Used to access the corresponding value.
- **Example:** In `student['name']`, the key is `'name'`.

### 3. **Value**
The data associated with a key in a dictionary. Can be any data type.
- **Example:** In `color['red'] = 255`, the value is `255`.

### 4. **Key-Value Pair**
A combination of a unique key and its associated value. The fundamental unit of a dictionary.
- **Example:** `'gpa': 3.8` is a key-value pair.

### 5. **Tuple**
An immutable sequence of elements enclosed in parentheses `()`. Cannot be changed after creation.
- **Example:** `point = (10, 20)` or `rgb = (255, 128, 64)`

### 6. **Set**
An unordered collection of unique values enclosed in curly braces `{}`. Automatically removes duplicates.
- **Example:** `colors = {'red', 'green', 'blue'}`

### 7. **Mutable**
Able to be changed after creation. Lists, dictionaries, and sets are mutable.
- **Example:** You can modify `student['gpa']` after the dict is created.

### 8. **Immutable**
Cannot be changed after creation. Tuples and strings are immutable.
- **Example:** `point = (10, 20)` cannot be modified; you must create a new tuple.

### 9. **.get()**
A safe dictionary method that retrieves a value by key. Returns a default value if the key doesn't exist (instead of raising an error).
- **Example:** `age = student.get('age', 18)` returns 18 if 'age' key is missing.

### 10. **.keys()**
A dictionary method that returns all keys in the dictionary.
- **Example:** `for key in student.keys(): print(key)`

### 11. **.values()**
A dictionary method that returns all values in the dictionary.
- **Example:** `for value in student.values(): print(value)`

### 12. **.items()**
A dictionary method that returns all key-value pairs as tuples.
- **Example:** `for key, value in student.items(): print(f"{key}: {value}")`

### 13. **Packing**
Combining multiple values into a single tuple.
- **Example:** `point = (10, 20)` packs two values into a tuple.

### 14. **Unpacking**
Extracting individual values from a tuple and assigning them to separate variables.
- **Example:** `x, y = point` unpacks the tuple into `x` and `y`.

### 15. **Union** (Set Operation)
The combination of all unique elements from two or more sets. Symbol: `|`
- **Example:** `{1, 2} | {2, 3}` results in `{1, 2, 3}`

### 16. **Intersection** (Set Operation)
The set of elements that appear in both (or all) sets. Symbol: `&`
- **Example:** `{1, 2, 3} & {2, 3, 4}` results in `{2, 3}`

### 17. **Difference** (Set Operation)
The set of elements in the first set but not in the second. Symbol: `-`
- **Example:** `{1, 2, 3} - {2, 3}` results in `{1}`

### 18. **JSON** (JavaScript Object Notation)
A lightweight, text-based format for storing and exchanging data. Python dicts closely resemble JSON objects.
- **Example:** `{"name": "Alice", "gpa": 3.8}` (note: JSON uses double quotes)

### 19. **Nested Data Structure**
A data structure that contains other data structures. For example, a list of dictionaries or a dictionary of lists.
- **Example:** `students = [{'name': 'Alice', 'gpa': 3.8}, {'name': 'Bob', 'gpa': 3.5}]`

### 20. **Hash** (Concept)
An internal mechanism used by Python to quickly locate a dictionary key or check set membership. Keys must be hashable (immutable) like strings, numbers, or tuples.

---

## Quick Reference: Dictionary Operations

```python
# Create a dictionary
student = {'name': 'Alice', 'gpa': 3.8, 'grade': 10}

# Access a value
print(student['name'])                    # Alice

# Add or modify
student['email'] = 'alice@school.edu'    # Add
student['gpa'] = 3.9                     # Modify

# Delete
del student['email']

# Check if key exists
if 'gpa' in student:
    print(student['gpa'])

# Safe access with default
age = student.get('age', 18)              # Returns 18 if missing

# Iterate
for key in student.keys():
    print(key)

for value in student.values():
    print(value)

for key, value in student.items():
    print(f"{key}: {value}")
```

## Quick Reference: Tuple Operations

```python
# Create a tuple
point = (10, 20)
rgb = (255, 128, 64)

# Access
print(point[0])                           # 10

# Unpack
x, y = point

# Iterate
for value in point:
    print(value)

# Cannot modify (immutable)
# point[0] = 15  # ERROR!

# Use as dictionary key (because immutable)
locations = {(0, 0): 'Origin', (10, 20): 'Point A'}
```

## Quick Reference: Set Operations

```python
# Create a set
colors = {'red', 'green', 'blue', 'red'}  # Duplicates removed

# Add and remove
colors.add('yellow')
colors.remove('red')

# Check membership (fast)
if 'green' in colors:
    print('Green is in the set')

# Set operations
set1 = {1, 2, 3}
set2 = {2, 3, 4}

union = set1 | set2                       # {1, 2, 3, 4}
intersection = set1 & set2                # {2, 3}
difference = set1 - set2                  # {1}
```

## Quick Reference: Data Structure Comparison

| Feature | List | Tuple | Dict | Set |
|---------|------|-------|------|-----|
| Ordered | Yes | Yes | Yes* | No |
| Mutable | Yes | No | Yes | Yes |
| Duplicates | Yes | Yes | No (keys) | No |
| Lookup | O(n) | O(n) | O(1)** | O(1)** |
| Use Case | Sequences, changing data | Immutable data, returns | Named fields, lookups | Unique values |

*Dicts are ordered as of Python 3.7+
**Average case

---

## Study Tips

1. **Visualize a dictionary:** Think of it like a phone book where the name is the key and the phone number is the value.
2. **Relate to C structs:** A dictionary is like a struct, but with more flexibility—you can add fields dynamically.
3. **Remember tuple immutability:** Once created, a tuple cannot change. This makes it safe and fast.
4. **Sets for uniqueness:** When you need only unique values, use a set instead of checking a list manually.
5. **Nested structures:** Practice accessing nested data by working from the outside in: `students[0]['name']` means "the 'name' field of the first student in the list."

---

## Standards Alignment

- **ODE 5.2.1:** Students understand how to work with built-in data structures and their operations.
- **ODE 5.3.5:** Students design and implement programs using appropriate data structures and algorithms.

