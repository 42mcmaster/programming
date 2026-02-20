prog03_pythonFundamentals - Complete Course Materials
====================================================

Instructor: Ryan McMaster
School: Medina County Career Center
Course: Programming 03 - Python Fundamentals

OVERVIEW:
This package contains all materials for a 3-week introduction to Python programming,
designed for high school CTE students who have completed 2 weeks of C programming.

Focus: Python syntax differences from C, dynamic typing, input/output, and basic programs.

FILE INVENTORY (14 files):
========================

INSTRUCTION & REFERENCE:
1. prog03_Slides.md (MARP format, 9 slides)
   - Covers Sub-Lessons 03a, 03b, 03c
   - Key differences between Python and C
   - Temperature converter and tip calculator examples

2. prog03_StudyGuide.md
   - 18 key terms with definitions
   - Quick reference for Python syntax
   - Comparison table: Python vs C
   - Alignment with Ohio Academic Standards 5.2.1 and 5.2.3

STUDENT WALKTHROUGHS:
3. prog03_Walkthrough.ipynb
   - Complete walkthrough with explanations
   - Sections for each sub-lesson
   - "Try This" cells with blanks for hands-on practice
   - Real program examples (temperature converter, tip calculator)

4. prog03_Walkthrough_Solutions.ipynb (INSTRUCTOR ONLY)
   - All "Try This" cells completed
   - Instructor notes and teaching tips

TASK MATERIALS (3 sub-lessons, 6 notebooks):

SUB-LESSON 03a — Python vs C Translation:
5. prog03a_Task.ipynb
   - 8 exercises translating C snippets to Python
   - Print statements, variables, input/output
   - Type verification exercises

6. prog03a_Task_Solutions.ipynb (INSTRUCTOR ONLY)
   - Complete solutions with notes

SUB-LESSON 03b — Variables, Types, and I/O:
7. prog03b_Task.ipynb
   - 10 exercises on type checking and conversion
   - Input/conversion practice
   - Arithmetic and operator exercises

8. prog03b_Task_Solutions.ipynb (INSTRUCTOR ONLY)
   - Complete solutions with assessment notes

SUB-LESSON 03c — Writing Real Programs:
9. prog03c_Task.ipynb
   - 5 complete program assignments + 1 challenge
   - Temperature converter
   - Tip calculator
   - Payroll calculator
   - Rectangle area/perimeter
   - Grade averaging
   - Currency converter (challenge)

10. prog03c_Task_Solutions.ipynb (INSTRUCTOR ONLY)
    - Complete solutions for all programs

INDEPENDENT WORK:
11. prog03_DIYTask.ipynb
    - "Personal Info Card" project
    - Requires: multiple inputs, calculations, formatted output
    - Reflection questions included

12. prog03_DIYTask_Solutions.ipynb (INSTRUCTOR ONLY)
    - Complete solution with assessment rubric
    - Sample student reflection answers

ASSESSMENT:
13. prog03_Gimkit.csv (28 questions)
    - Game-based review format
    - Covers Python basics and syntax differences from C

14. prog03_GoogleQuiz.csv (25 questions)
    - Multiple choice format
    - Aligned with lesson objectives

LESSON STRUCTURE:
===============

WEEK 1 (Sub-Lesson 03a: Python vs C — 50 minutes)
- 25 min instruction: Slides + Walkthrough intro
- 25 min hands-on: prog03a_Task.ipynb

WEEK 2 (Sub-Lesson 03b: Variables and I/O — 50 minutes)
- 25 min instruction: Walkthrough + Study Guide review
- 25 min hands-on: prog03b_Task.ipynb

WEEK 3 (Sub-Lesson 03c: Real Programs — 50 minutes)
- 25 min instruction: Real program examples from walkthrough
- 25 min hands-on: prog03c_Task.ipynb + start prog03_DIYTask.ipynb

INDEPENDENT WORK:
- prog03_DIYTask.ipynb (at home or in class, 30-45 min)
- Gimkit or GoogleQuiz review (10-15 min)

KEY TOPICS COVERED:
==================

Interpreted vs Compiled
- No compilation needed
- No headers or main() function required

Syntax Changes:
- Indentation (not braces)
- No semicolons
- Comments with # (not //)

Dynamic Typing:
- Variable assignment without type declaration
- type() function to check types
- Automatic type coercion

Input/Output:
- print() function and f-strings
- input() function (returns string)
- Type conversion: int(), float(), str()

Data Types:
- int, float, str, bool

Operators:
- Arithmetic: +, -, *, /, //, %
- String concatenation with +
- / always returns float (unlike C)
- // for integer division

Program Structure:
- Comments → Constants → Input → Processing → Output
- Using f-strings for formatted output

NOTEBOOK SPECIFICATIONS:
=======================
All .ipynb files are valid JSON with:
- kernelspec: Python 3
- nbformat: 4
- nbformat_minor: 4
- Markdown and code cells properly formatted
- Comments and instructor notes throughout

NAMING CONVENTIONS:
==================
- All variable names use camelCase (studentName, not student_name)
- Constants in UPPERCASE (TIP_PERCENT)
- Descriptive, readable names encouraged

DIFFERENTIATION:
===============
- Basic exercises: prog03a_Task and prog03b_Task
- Medium complexity: prog03c_Task (programs 1-3)
- Advanced: prog03c_Task (programs 4-5 and challenge)
- Independent/Accelerated: prog03_DIYTask

NOTES FOR INSTRUCTORS:
=====================
1. Students have C background - leverage this!
   - Show what they'd need to write in C vs Python
   - Emphasize simplicity and readability

2. Common Errors to Watch:
   - Forgetting to convert input() output to int/float
   - Missing f prefix on f-strings
   - Indentation issues (though less critical in notebooks)
   - Confusing / and // operators

3. Timing:
   - 20-30 min instruction per sub-lesson
   - 20-30 min hands-on practice
   - 30-45 min for DIY project

4. Assessment:
   - Task completion: Is logic correct? Are f-strings used?
   - DIY project: Rubric included (20 points)
   - Gimkit/GoogleQuiz: For quick comprehension check

5. Extensions:
   - Have students rewrite C programs from prog01 in Python
   - Modify calculator programs to handle invalid input
   - Add more complex calculations to real programs

====================================================
Last Updated: February 2026
Version: 1.0
====================================================
