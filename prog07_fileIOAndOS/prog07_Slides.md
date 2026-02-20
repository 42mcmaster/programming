---
marp: true
theme: default
class: invert
paginate: true
---

# Lesson 07: File I/O & OS Module
## Programming
### Medina County Career Center
### Instructor: Ryan McMaster

---

## Why File I/O Matters
- BPA contest requires reading data files and writing results
- Real-world programming: databases, config files, logs, reports
- Data persistence: saving user input between program runs
- Example: Processing student grades, game scores, sensor data

---

## Reading Files
```python
# Three ways to read a file
with open('data.txt', 'r') as file:
    content = file.read()        # Read entire file as string
    line = file.readline()       # Read one line
    lines = file.readlines()     # Read all lines as list
```
- Always use `with` statement (closes file automatically)
- Mode `'r'` = read (file must exist)
- `.strip()` removes newlines and whitespace

---

## Writing Files
```python
# Write mode: 'w' creates or overwrites
with open('output.txt', 'w') as file:
    file.write('Hello\n')
    file.writelines(['Line 1\n', 'Line 2\n'])

# Append mode: 'a' adds to end of file
with open('log.txt', 'a') as file:
    file.write('New entry\n')
```
- Mode `'w'` = write (overwrites existing file)
- Mode `'a'` = append (adds to end)

---

## OS Module: File Management
```python
import os

os.listdir('.')              # List all files in current directory
os.path.exists('file.txt')   # Check if file exists
os.path.join('folder', 'file.txt')  # Build file paths safely
os.rename('old.txt', 'new.txt')     # Rename file
os.mkdir('newfolder')       # Create directory
os.remove('file.txt')       # Delete file
```

---

## CSV Files and Data Processing
- CSV = Comma-Separated Values (spreadsheet format)
- Manual parsing: `line.split(',')`
- Python has built-in `csv` module for complex data
- Example: Reading student grades from CSV

---

## Context Managers: The `with` Statement
```python
# Why we use 'with':
with open('file.txt', 'r') as file:
    data = file.read()
# File automatically closes here (no need for file.close())

# Risky way (don't do this):
file = open('file.txt', 'r')
data = file.read()
file.close()  # Could be skipped if error occurs
```

---

## Hands-On Practice Today
1. **07a**: Read files, count lines/words, search for keywords
2. **07b**: Write user input, create logs, modify files
3. **07c**: List files, process CSV, rename files, create reports
4. **DIY**: Build a Grade Manager application (read, calculate, write)

---

## Key Takeaways
- Use `with open()` for safe file handling
- Read: `.read()`, `.readline()`, `.readlines()`
- Write: mode `'w'` (new) or `'a'` (append)
- OS module: navigate, rename, delete, create directories
- CSV: simple data format with `split(',')`
