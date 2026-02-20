# Prog05: Functions & Modules
## Programming Course | Medina County Career Center
**Instructor: Ryan McMaster**

---

## Overview

This directory contains a complete lesson package covering Python functions and modules for high school CTE students. All materials assume students have completed Python basics (variables, control flow) and are familiar with C function syntax.

## Files

### Instructional Materials

1. **prog05_Slides.md** (10 slides)
   - MARP presentation format for classroom use
   - Covers all three sub-lessons: function definition, scope & modules, putting it together
   - Compares C vs Python function syntax
   - High school appropriate level

2. **prog05_StudyGuide.md** (18 key terms)
   - Quick reference guide for 18 essential vocabulary terms
   - Includes definitions, examples, and comparison with C
   - Aligned with ODE standards 5.2.1, 5.2.2, 5.2.3
   - Covers: functions, parameters, return, scope, modules, imports, etc.

### Walkthrough Notebooks

3. **prog05_Walkthrough.ipynb** (STUDENT VERSION)
   - 14 code examples with explanatory markdown cells
   - Student cells contain `# Your code here` blanks for guided practice
   - Topics: function definition, parameters, defaults, keyword args, docstrings, scope, modules

4. **prog05_Walkthrough_Solutions.ipynb** (INSTRUCTOR VERSION)
   - Complete solutions with detailed instructor notes in each section
   - "Instructor Note:" cells explain key concepts and common student misconceptions
   - DO NOT DISTRIBUTE

### Sub-Lesson 05a: Function Definition Tasks

5. **prog05a_Task.ipynb** (STUDENT VERSION - 8 exercises)
   - Simple Area Calculator
   - Circle Area (using math.pi)
   - BMI Calculator
   - Letter Grade Function (if-elif-else)
   - Price with Tax (default parameters)
   - Temperature Converter
   - Greeting with Default Parameter
   - Challenge: Absolute Value (without using built-in abs())

6. **prog05a_Task_Solutions.ipynb** (INSTRUCTOR VERSION)
   - Detailed solutions for all 8 exercises
   - Instructor notes on approach and common mistakes
   - DO NOT DISTRIBUTE

### Sub-Lesson 05b: Scope & Modules Tasks

7. **prog05b_Task.ipynb** (STUDENT VERSION - 10 exercises)
   - Scope tracing exercises
   - Local vs global variable understanding
   - Using the global keyword (with caution)
   - Math module: sqrt, ceil, floor, pow, pi
   - from...import syntax
   - Random module: randint, choice, shuffle
   - Challenge: Coin flip simulation combining functions and modules

8. **prog05b_Task_Solutions.ipynb** (INSTRUCTOR VERSION)
   - Complete solutions demonstrating best practices
   - Shows both correct approaches and anti-patterns
   - DO NOT DISTRIBUTE

### Sub-Lesson 05c: Multi-Function Program

9. **prog05c_Task.ipynb** (STUDENT VERSION - Calculator Program)
   - Part 1: Four operation functions (add, subtract, multiply, divide)
   - Part 2: Menu display function
   - Part 3: performCalculation function that calls operation functions
   - Part 4: Main runCalculator program with user loop
   - Part 5: Demo of working program

10. **prog05c_Task_Solutions.ipynb** (INSTRUCTOR VERSION)
    - Complete calculator implementation
    - Demonstrates function composition and program organization
    - Shows error handling (division by zero)
    - DO NOT DISTRIBUTE

### Independent Project

11. **prog05_DIYTask.ipynb** (STUDENT VERSION - Dice Game)
    - Five functions to implement:
      - rollDice(): rolls two dice, returns sum
      - checkFirstRoll(roll): returns "win", "lose", or point
      - checkPointRoll(roll, point): returns "win", "lose", or "continue"
      - playGame(): orchestrates one complete game
      - Main program: loop for multiple games
    - Game rules: craps-style dice game with win/lose/point conditions
    - Combines functions, modules (random), and program flow

12. **prog05_DIYTask_Solutions.ipynb** (INSTRUCTOR VERSION)
    - Complete dice game implementation
    - Shows professional code structure and comments
    - DO NOT DISTRIBUTE

### Assessment Materials

13. **prog05_Gimkit.csv** (28 questions)
    - Gimkit format (Question, Correct Answer, 3 Incorrect Answers)
    - Questions on function syntax, parameters, modules, scope
    - ~1 point each
    - Fast-paced game format

14. **prog05_GoogleQuiz.csv** (28 questions)
    - Google Quiz format (Question, 4 Options A-D, Correct Answer, Points)
    - Different questions than Gimkit for post-lesson assessment
    - Mix of 1-2 point questions for varied difficulty
    - Topics: function basics, modules, scope, type hints

15. **Unit2_EndOfUnit_GoogleQuiz.csv** (38 questions)
    - Comprehensive end-of-unit assessment
    - Covers prog03, prog04, prog05
    - Approximately 70% prog05 (functions & modules)
    - Approximately 30% review (control flow, data types, operations)
    - Google Quiz format
    - 1-2 point questions for comprehensive evaluation

---

## Student Learning Path

### Week 1: Function Basics
1. Attend lecture using prog05_Slides.md
2. Read prog05_StudyGuide.md for vocabulary
3. Work through prog05_Walkthrough.ipynb
4. Complete prog05a_Task.ipynb exercises

### Week 2: Scope & Modules
1. Complete prog05b_Task.ipynb exercises
2. Practice with math and random modules
3. Understand variable scope through exercises

### Week 3: Multi-Function Programs
1. Complete prog05c_Task.ipynb (calculator project)
2. Work on prog05_DIYTask.ipynb (dice game project)
3. Test understanding with prog05_GoogleQuiz.csv

### Final Assessment
- Take Unit2_EndOfUnit_GoogleQuiz.csv for comprehensive review

---

## Lesson Content Summary

### Sub-Lesson 05a: Defining Functions (~25 min + hands-on)
- def keyword and function structure
- Parameters and arguments (positional and keyword)
- Return values and return statements
- Default parameter values
- Docstrings for documentation
- Comparison with C: `int add(int a, int b)` vs `def add(a, b):`
- Type hints (optional, not enforced)

### Sub-Lesson 05b: Scope and Modules (~25 min + hands-on)
- Variable scope: local vs global
- Local variables (function scope only)
- Global variables (accessible everywhere)
- The global keyword (use sparingly)
- Importing modules: `import math` and `from math import sqrt`
- Built-in modules: math, random, os, sys
- Math module functions: sqrt, ceil, floor, pi, pow
- Random module functions: randint, choice, shuffle
- Writing custom modules (save functions in .py file, import them)

### Sub-Lesson 05c: Putting It Together (~25 min + hands-on)
- Functions calling other functions
- Building multi-function programs
- Code organization best practices
- Separation of concerns (display, calculation, control)
- Testing with print statements
- Error handling (division by zero example)
- Professional code structure

---

## Key Learning Objectives (ODE 5.2.1, 5.2.2, 5.2.3)

Students will be able to:
- Define functions with parameters and return values
- Use default and keyword arguments effectively
- Write docstrings to document functions
- Understand and apply variable scope
- Import and use built-in modules (math, random)
- Create and use custom modules
- Compose multiple functions into coherent programs
- Organize code for maintainability and reusability

---

## Technical Details

### Notebook Format
- Valid JSON format (nbformat 4, nbformat_minor 4)
- Python 3 kernel
- Student versions have `# Your code here` placeholder cells
- Instructor versions have complete solutions and instructor notes

### Code Standards
- Heavy commenting for educational clarity
- camelCase for variable/function names
- Defensive programming (e.g., division by zero checks)
- Professional high school CTE level
- No emojis (professional standard)

### Quiz Formats
- **Gimkit**: Question, Correct Answer, Incorrect Answer 1-3
- **Google Quiz**: Question, Option A-D, Correct Answer (column position), Points

---

## Notes for Instructors

1. **Pacing**: Each sub-lesson can be taught in one 50-minute class period with hands-on practice.

2. **Differentiation**:
   - Students who finish early can attempt "Challenge" problems
   - Walkthrough Examples 1-10 are essential; Examples 11-14 (type hints, composition) can be optional

3. **Assessment Strategy**:
   - Use prog05_GoogleQuiz.csv after each sub-lesson
   - Use prog05_Gimkit.csv for formative assessment/review
   - Use Unit2_EndOfUnit_GoogleQuiz.csv for summative assessment

4. **Common Misconceptions**:
   - Students may think local variables persist between function calls
   - May confuse parameters (definition) with arguments (calls)
   - May think global keyword is needed to READ global variables (not true)
   - May struggle with the distinction between function calls vs definitions

5. **Extensions**:
   - Have students convert the calculator to use a dictionary for operations
   - Have students create a module with game functions
   - Discuss lambda functions (briefly, as extension)

---

## Standards Alignment

- **ODE 5.2.1**: Define and use functions with parameters and return values
- **ODE 5.2.2**: Use and understand variable scope
- **ODE 5.2.3**: Import and use modules; create custom modules

---

**Created for**: Medina County Career Center Programming Course
**Instructor**: Ryan McMaster
**Date**: 2026

