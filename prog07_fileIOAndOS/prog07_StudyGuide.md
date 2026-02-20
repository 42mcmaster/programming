# Lesson 07: File I/O & OS Module — Study Guide
## Medina County Career Center | Instructor: Ryan McMaster

---

## Essential Terms & Concepts

### 1. **File**
A collection of data stored on disk (hard drive). In Python, files are read sequentially from beginning to end, one line or character at a time. Files can contain text, binary data, or structured information like CSV data.

### 2. **open() Function**
Built-in Python function that opens a file and returns a file object. Syntax: `open(filename, mode)`
- Returns a file object that allows reading/writing
- Must specify the mode: `'r'`, `'w'`, or `'a'`

### 3. **File Object**
The result of calling `open()`. It's an object with methods like `.read()`, `.write()`, `.readline()`, and `.close()`.

### 4. **Read Mode ('r')**
Opens a file for reading only. File must exist. Does not allow writing.

### 5. **Write Mode ('w')**
Opens a file for writing. Creates a new file or overwrites existing file completely. All previous content is lost.

### 6. **Append Mode ('a')**
Opens a file for writing at the end without overwriting existing content. If file doesn't exist, creates it.

### 7. **Context Manager**
A programming pattern that ensures resources (like files) are properly cleaned up. Implemented using the `with` statement.

### 8. **with Statement**
Syntax: `with open(filename, mode) as variable:`. Automatically closes the file when the block ends, even if an error occurs. Preferred way to open files in modern Python.

### 9. **read() Method**
Reads and returns the entire file contents as a single string, including all newline characters.

### 10. **readline() Method**
Reads and returns a single line from the file (including the newline character at the end). Each call reads the next line.

### 11. **readlines() Method**
Reads and returns all lines as a list of strings. Each string in the list includes the newline character.

### 12. **write() Method**
Writes a string to the file. Does NOT add a newline automatically; you must include '\n' if needed.

### 13. **writelines() Method**
Writes a list of strings to the file. Does NOT automatically add newlines between items.

### 14. **Newline Character ('\n')**
Special character that marks the end of a line. When reading, included in the string. When writing, must be added manually.

### 15. **strip() Method**
Removes whitespace (including newlines and spaces) from both ends of a string. Useful for cleaning up lines read from files.

### 16. **os Module**
Python standard library for operating system interactions: listing files, creating/deleting directories, renaming files, checking file existence.

### 17. **os.listdir()**
Returns a list of all files and folders in a directory. Syntax: `os.listdir('.')`  or `os.listdir('/path/to/directory')`

### 18. **os.path.exists()**
Checks if a file or directory exists. Returns True or False. Useful before attempting to read a file.

### 19. **os.path.join()**
Safely builds file paths across different operating systems. Handles forward/backward slashes automatically. Syntax: `os.path.join('folder', 'subfolder', 'file.txt')`

### 20. **os.rename()**
Renames a file. Syntax: `os.rename('oldname.txt', 'newname.txt')`

### 21. **os.mkdir()**
Creates a new directory. Syntax: `os.mkdir('newfolder')`

### 22. **os.remove()**
Permanently deletes a file. Use with caution; cannot be undone.

### 23. **CSV (Comma-Separated Values)**
Text format for storing tabular data. Each line is a row; commas separate columns. Simple alternative to Excel or databases.

### 24. **split() Method**
String method that divides a string by a delimiter. Syntax: `line.split(',')` splits by comma.

### 25. **File Path**
Address to a file on disk. Can be absolute (`/home/user/file.txt`) or relative (`./data/file.txt`).

### 26. **Directory**
Folder on disk containing files and other directories. Current directory is represented by `'.'`

### 27. **csv Module**
Python standard library with tools for reading/writing CSV files more safely than manual splitting.

### 28. **close() Method**
Explicitly closes a file and releases system resources. Not needed with `with` statement (automatic).

---

## Quick Reference: Common Patterns

### Reading a File
```python
with open('input.txt', 'r') as file:
    content = file.read()  # Entire file as string
```

### Reading Line by Line
```python
with open('input.txt', 'r') as file:
    for line in file:
        line = line.strip()  # Remove newline
        print(line)
```

### Writing to a File
```python
with open('output.txt', 'w') as file:
    file.write('Line 1\n')
    file.write('Line 2\n')
```

### Appending to a File
```python
with open('log.txt', 'a') as file:
    file.write('New entry\n')
```

### Checking File Existence
```python
import os
if os.path.exists('data.txt'):
    print('File found')
else:
    print('File not found')
```

### Listing Files in a Directory
```python
import os
files = os.listdir('.')
for file in files:
    print(file)
```

### Processing CSV Data
```python
with open('data.csv', 'r') as file:
    for line in file:
        fields = line.strip().split(',')
        print(fields)
```

---

## Standards Alignment
- **ODE 5.2.2**: Implement functions and design solutions using appropriate data structures
- **ODE 5.4.1**: Use appropriate file and data formats to solve problems

---

## Practice Tips
1. Always use `with open()` — never use `open()` without `with`
2. Remember to add `'\n'` when writing lines; `.write()` does NOT add it automatically
3. Use `.strip()` to remove newlines when reading
4. Test file operations in small steps; don't write complex code all at once
5. Use `os.path.exists()` before reading to avoid errors
6. Build paths with `os.path.join()`, not string concatenation
