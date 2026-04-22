# Intro to Python — Teacher Curriculum

**Instructor:** Ryan McMaster
**Course:** SE1 Programming — Medina County Career Center
**Audience:** Students with no prior C (or other language) experience.
**Format:** Each lesson is designed for a ~20-minute whole-class walkthrough followed by ~60 minutes of independent work on the matching task notebook.

---

## Folder Layout

- `lesson0X_..._Task.ipynb` — **student-facing** notebooks. Committed to the repo; students complete these.
- `teacher/` — **teacher-only** materials. This folder is in `.gitignore` and must NOT be committed.
  - `lesson0X_..._Walkthrough.md` — narrated teacher script for reading to the class.
  - `lesson0X_..._Solution.ipynb` — working solution key for each task notebook.

## Lesson Sequence

| # | Topic | Walkthrough (teacher/) | Task (student) | Solution (teacher/) |
|---|---|---|---|---|
| 01 | Print & Comments | `teacher/lesson01_printAndComments_Walkthrough.md` | `lesson01_printAndComments_Task.ipynb` | `teacher/lesson01_printAndComments_Solution.ipynb` |
| 02 | Variables & Data Types | `teacher/lesson02_variablesAndTypes_Walkthrough.md` | `lesson02_variablesAndTypes_Task.ipynb` | `teacher/lesson02_variablesAndTypes_Solution.ipynb` |
| 03 | Input & Type Conversion | `teacher/lesson03_inputAndConversion_Walkthrough.md` | `lesson03_inputAndConversion_Task.ipynb` | `teacher/lesson03_inputAndConversion_Solution.ipynb` |
| 04 | Arithmetic & f-strings | `teacher/lesson04_arithmeticAndFstrings_Walkthrough.md` | `lesson04_arithmeticAndFstrings_Task.ipynb` | `teacher/lesson04_arithmeticAndFstrings_Solution.ipynb` |
| 05 | Comparison Operators | `teacher/lesson05_comparisonOperators_Walkthrough.md` | `lesson05_comparisonOperators_Task.ipynb` | `teacher/lesson05_comparisonOperators_Solution.ipynb` |
| 06 | if / elif / else | `teacher/lesson06_ifElifElse_Walkthrough.md` | `lesson06_ifElifElse_Task.ipynb` | `teacher/lesson06_ifElifElse_Solution.ipynb` |
| 07 | Logical Operators (and/or/not) | `teacher/lesson07_logicalOperators_Walkthrough.md` | `lesson07_logicalOperators_Task.ipynb` | `teacher/lesson07_logicalOperators_Solution.ipynb` |
| 08 | for loops & range() | `teacher/lesson08_forLoopsAndRange_Walkthrough.md` | `lesson08_forLoopsAndRange_Task.ipynb` | `teacher/lesson08_forLoopsAndRange_Solution.ipynb` |
| 09 | while loops, break, continue | `teacher/lesson09_whileLoops_Walkthrough.md` | `lesson09_whileLoops_Task.ipynb` | `teacher/lesson09_whileLoops_Solution.ipynb` |
| 10 | Functions & Docstrings | `teacher/lesson10_functions_Walkthrough.md` | `lesson10_functions_Task.ipynb` | `teacher/lesson10_functions_Solution.ipynb` |

## How to use this folder

- **Walkthroughs are teacher-only** (markdown, easy to edit). They contain a full narrative script, common student mistakes, and live-code examples. Do not share these files with students.
- **Solution notebooks are teacher-only** (ipynb). Use them to check student work and as a reference while circulating the room.
- **Task notebooks are student-facing** (ipynb). Each has 5–7 exercises that mirror the walkthrough. Students commit them to the repo when finished.
- The entire `teacher/` subfolder is excluded by `.gitignore`. Keep it that way — students should never see the solution keys before attempting the work.
- There are no comparisons to C or any other language in these materials. Every concept is introduced on its own terms.

## Standards Coverage (ODE 145060)

Across the 10 lessons: 5.1.1, 5.1.2, 5.1.8, 5.2.1, 5.2.3, 5.2.4, 5.3.1, 5.3.4, 5.3.5, 5.3.6, 5.3.8, 5.3.9, 5.4.2, 5.4.3, 5.4.6, 5.5.2, 5.5.5, 5.5.6, 5.5.7.
