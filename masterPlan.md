# Programming Course — Master Plan
## Medina County Career Center | Instructor: Ryan McMaster
### ODE Course: 145060 Programming

---

## Course Overview

This course is restructured to begin with C programming fundamentals taught by guest instructor **Jared Henderson**, then transitions to Python for the remainder of the course. The C foundation gives students a low-level understanding of how computers actually work before moving to a higher-level language. Python lessons build toward **BPA contest readiness**.

Arduino content will be added later (timing TBD — possibly before or after Python).

---

## Unit 1: C Programming & Computing Fundamentals
**Guest Instructor: Jared Henderson**

### prog01_introCAndComputing
**Jared Visit 1 (1 period teaching) + 2 days follow-on work (4 hours)**

Teaching Session Topics:
- Why C matters (lingua franca of computing, FFI, performance)
- Compilation vs interpretation — gcc pipeline (5.1.7)
- Binary, hex, and overflow (2.3.2)
- ASCII and character encoding (2.3.1)
- Types and memory — int, float, char, sizeof (5.2.1)
- Pointers and memory layout — stack vs heap, malloc/free
- Strings as byte arrays with null terminators (2.3.1)
- Functions with typed signatures (5.2.1, 5.2.3)
- scanf for user input

Follow-On Exercises (grouped into 2 sessions):
- **Session A** (~2 hrs): Syntax & compilation (JS→C translation), encoding & number systems (ASCII values, uppercase conversion, binary printing, overflow)
- **Session B** (~2 hrs): Functions/types/math (temperature converter, clamp, weighted average), arrays & loops (max, average, reverse), strings & dynamic memory (strlen, Caesar cipher, malloc)

ODE Competencies: 2.3.1, 2.3.2, 5.1.7, 5.2.1, 5.2.3, 5.3.8, 5.4.6, 5.4.7

Deliverables:
- [x] prog01_Slides.md (MARP)
- [x] prog01_StudyGuide.md
- [x] prog01_Walkthrough.md (Windows setup + first C programs — matches cTest.pdf format)
- [x] prog01_Walkthrough_Solutions.md (Instructor version)
- [x] prog01a_Task.md (Session A exercises — student)
- [x] prog01a_Task_Solutions.md (Session A — instructor)
- [x] prog01b_Task.md (Session B exercises — student)
- [x] prog01b_Task_Solutions.md (Session B — instructor)
- [x] prog01_DIYTask.md (Stretch: memory exploration)
- [x] prog01_DIYTask_Solutions.md
- [x] prog01_Gimkit.csv
- [x] prog01_GoogleQuiz.csv

### prog02_structsAndImageProcessing
**Jared Visit 2 (1 period teaching) + 2 days follow-on work (4 hours)**

Teaching Session Topics:
- Review of Week 1
- Structs — custom types, dot notation, RGBTRIPLE (5.2.1)
- 2D arrays — grid[rows][cols], nested loops, row-major layout (5.3.8)
- Image as 2D array of pixel structs
- Filter scaffold walkthrough (bmp.h, helpers.h, filter.c)
- Grayscale coded together
- Debugging with printf (5.4.6, 5.4.7)

Follow-On Exercises (grouped into 2 sessions):
- **Session A** (~2 hrs): Grayscale and reflect filters
- **Session B** (~2 hrs): Blur filter + stretch: edge detection (Sobel)

ODE Competencies: 5.2.1, 5.2.3, 5.3.8, 5.4.6, 5.4.7

Deliverables:
- [x] prog02_Slides.md (MARP)
- [x] prog02_StudyGuide.md
- [x] prog02_Walkthrough.md (Filter setup + grayscale walkthrough)
- [x] prog02_Walkthrough_Solutions.md
- [x] prog02a_Task.md (Session A — grayscale + reflect)
- [x] prog02a_Task_Solutions.md
- [x] prog02b_Task.md (Session B — blur + edge detection)
- [x] prog02b_Task_Solutions.md
- [x] prog02_DIYTask.md (Creative filter)
- [x] prog02_DIYTask_Solutions.md
- [x] prog02_Gimkit.csv
- [x] prog02_GoogleQuiz.csv
- [x] Unit1_EndOfUnit_GoogleQuiz.csv (35-40 questions)

---

## Unit 2: Python Fundamentals
**Instructor: Ryan McMaster**

*Note: Students already have C experience with types, variables, loops, functions, compilation. Python intro is lighter — focuses on syntax differences and Python-specific features rather than re-teaching fundamentals.*

### prog03_pythonFundamentals
**Python syntax, variables, I/O, types — bridging from C**

Topics:
- Python vs C — interpreted, dynamic typing, no braces/semicolons
- IDLE setup and script mode
- Variables (no type declarations, camelCase convention)
- Data types: int, float, str, bool — type() and isinstance()
- Input/output: print(), input(), f-strings
- Type conversion: int(), float(), str()
- Basic arithmetic (same operators, but / always returns float)
- Comments and program structure

ODE Competencies: 5.2.1, 5.2.3

### prog04_controlFlow
**Conditionals and loops in Python**

Topics:
- Boolean expressions and comparison operators
- if / elif / else (indentation-based blocks)
- Logical operators: and, or, not
- for loops with range() — connecting to C for loops
- while loops — sentinel values, input validation
- break and continue
- Nested loops

ODE Competencies: 5.3.3, 5.3.5, 5.3.8

### prog05_functionsAndModules
**Defining functions, parameters, return values, modules**

Topics:
- Defining functions with def — parameters and return
- Default parameters and keyword arguments
- Variable scope (local vs global)
- Importing modules: math, random
- Writing your own modules
- Docstrings

ODE Competencies: 5.2.1, 5.2.2, 5.2.3

### Unit2_EndOfUnit_GoogleQuiz.csv (35-40 questions covering prog03-prog05)

---

## Unit 3: Intermediate Python

### prog06_stringsAndLists
**String methods, list operations, data processing**

Topics:
- String methods: .upper(), .lower(), .strip(), .split(), .join(), .find(), .replace()
- String slicing and indexing
- Lists: creation, indexing, slicing, append, insert, remove, pop
- List comprehensions
- Sorting and searching
- Nested lists (connecting to 2D arrays from C)

ODE Competencies: 5.3.5, 5.3.8

### prog07_fileIOAndOS
**File reading/writing, os module, file system manipulation**

Topics:
- Opening files: open(), read(), readline(), readlines()
- Writing files: write(), writelines()
- Context managers (with statement)
- CSV file processing
- os module: os.listdir(), os.path, os.rename(), os.mkdir()
- Practical file manipulation tasks

ODE Competencies: 5.2.2, 5.4.1

### prog08_dataStructures
**Dictionaries, tuples, sets, complex data**

Topics:
- Dictionaries: creation, access, methods, iteration
- Tuples: immutability, packing/unpacking
- Sets: unique values, set operations
- Nested data structures (list of dicts, dict of lists)
- JSON basics
- Choosing the right data structure

ODE Competencies: 5.2.1, 5.3.5

### Unit3_EndOfUnit_GoogleQuiz.csv (35-40 questions covering prog06-prog08)

---

## Unit 4: Advanced Python & BPA Prep

### prog09_bpaContestPrep
**BPA-level problem solving, timed practice, contest strategies**

Topics:
- Error handling: try/except
- Complex string processing algorithms
- Multi-step data processing
- Working with formatted output
- Mathematical algorithms
- Timed practice problems modeled on BPA format
- Test-taking strategies for programming contests

ODE Competencies: 5.2.3, 5.3.5, 5.3.8, 5.4.6, 5.4.7

### Unit4_EndOfUnit_GoogleQuiz.csv (35-40 questions)

---

## ODE Competency Coverage Map

| Competency | Description | Covered In |
|---|---|---|
| 2.3.1 | ASCII / character encoding | prog01, prog06 |
| 2.3.2 | Binary, hex, number systems | prog01 |
| 5.1.1 | Safety procedures | All lessons (standard practice) |
| 5.1.7 | Compilers / interpreters | prog01, prog03 |
| 5.2.1 | Data types and variables | prog01, prog02, prog03, prog05, prog08 |
| 5.2.2 | Modules and libraries | prog05, prog07 |
| 5.2.3 | Arithmetic and expressions | prog01, prog03, prog05, prog09 |
| 5.3.3 | Selection structures | prog04 |
| 5.3.5 | Loop structures | prog04, prog06, prog08, prog09 |
| 5.3.8 | Nested loops / 2D structures | prog01, prog02, prog04, prog06, prog09 |
| 5.4.1 | File I/O | prog07 |
| 5.4.6 | Testing and debugging | prog01, prog02, prog09 |
| 5.4.7 | Error identification | prog01, prog02, prog09 |

---

## Notes

- **File format for C lessons (prog01, prog02):** All files are `.md` since C code is compiled on Windows with gcc, not run in Jupyter. Students write `.c` files in a text editor.
- **File format for Python lessons (prog03+):** Standard `.ipynb` Jupyter notebooks for walkthroughs and tasks.
- **Arduino lessons:** Placeholder — will be added later (potentially between Units 1 and 2, or after Unit 4).
- **Pacing:** Sub-lessons are NOT tied to calendar days. Teacher controls pacing.
- **Each lesson target:** 20-30 min instruction per sub-lesson, then hands-on work.
