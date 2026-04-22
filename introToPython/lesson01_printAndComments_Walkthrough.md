# Lesson 01 — Printing and Comments (Teacher Walkthrough)

> **Teacher-only file.** Do not share with students. This is your script for the ~20-minute whole-class opener.

**Student deliverable for today:** `lesson01_printAndComments_Task.ipynb`
**ODE standards touched:** 5.1.1 (programs solve problems), 5.4.2 (write and edit code in the IDE), 5.5.5 (comments).

---

## Learning Objectives

By the end of this lesson students should be able to:

1. Open a Jupyter notebook cell and run it.
2. Use `print()` to display text and numbers.
3. Pass multiple arguments to `print()` separated by commas.
4. Write single-line comments with `#` and explain why comments matter.

---

## Section 1 — What is Python? (2 minutes)

**Say to the class:**

> "Python is a programming language. A programming language is just a set of rules the computer can understand. When you write Python, you're writing **instructions** that the computer will follow, one line at a time, top to bottom. That's it. There is no magic."

> "The program we'll use all semester is called a **Jupyter notebook**. A notebook is a document where you can type Python into little boxes called **cells**, and the computer runs each cell when you press **Shift+Enter**. The result appears right underneath the cell."

**Demo on the projector:**

1. Open any `.ipynb` file in VS Code.
2. Click on a code cell.
3. Press `Shift+Enter` and show that nothing happens visibly because the cell was empty.

Now type this into a fresh cell and run it:

```python
print("Hello, world!")
```

**Say:**

> "That line did one thing. It printed the words 'Hello, world!' to the screen. Later in life, you will still be using `print` to check what your code is doing. It's the most important tool you have."

---

## Section 2 — The `print()` function (5 minutes)

**Introduce the vocabulary:**

> "The word `print` is what we call a **function**. For now, just think of a function as a **verb** — it does something. The parentheses `()` hold whatever you want the function to act on. Whatever you put inside the parentheses is called an **argument**."

Walk through these examples, one cell at a time, running each one:

```python
print("Hello!")
```

```python
print(42)
```

```python
print(3.14)
```

**Say after each:**

> "Notice it doesn't care if it's a word or a number. It just prints whatever you give it."

Now show that text has to be in **quotes**:

```python
print(Hello)     # This will crash — there's no variable called Hello
print("Hello")   # This works — it's text
```

**Say:**

> "Anything inside quotes is what Python calls a **string** — just a piece of text. If you forget the quotes, Python will look for a variable with that name, and it won't find one, so it crashes. The quotes are what tell Python: 'this is literally the letters H-e-l-l-o.'"

**Demo both single and double quotes work:**

```python
print('Single quotes also work.')
print("Double quotes work the same way.")
```

### Multiple arguments

Show that `print()` can take more than one thing at once, separated by commas:

```python
print("My name is", "Ryan")
print("The answer is", 42)
print("Pi is approximately", 3.14159)
```

**Say:**

> "When you give `print` multiple arguments separated by commas, it automatically puts a space between them. That saves you from having to type the space yourself."

### Blank lines and separators

```python
print()              # Prints a blank line
print("Line 1")
print("Line 2")
print("---")
print("Line 3")
```

---

## Section 3 — Comments (5 minutes)

**Say to the class:**

> "Sometimes you want to write notes to yourself inside your code — notes that Python ignores, but that help you remember what the code was supposed to do. Those are called **comments**."

**Demo:**

```python
# This is a comment. Python will not run it.
print("This line runs")
# print("This line does not run because it's commented out")
```

**Say:**

> "Everything after a `#` on a line is a comment. Python skips right over it. You have three big reasons to use comments:"

1. **Leave a note to yourself** so when you come back tomorrow you remember what you were doing.
2. **Explain to other people** — including me when I'm grading — what your code is trying to do.
3. **Temporarily disable a line** of code without deleting it.

**Show comment at end of line:**

```python
print("Hello")   # This greets the user
```

**Show a multi-line block of comments:**

```python
# Program: Greeting
# Author: Ryan
# Date: April 2026
# Purpose: Say hi to the world.
print("Hi!")
```

**Say:**

> "That block of comments at the top is called a **header comment**. I want to see one of these at the top of every task you turn in. It tells me who wrote the program and what it does."

---

## Section 4 — Common Mistakes (3 minutes)

Walk through each mistake on the projector. Type it wrong first, show the error, then fix it.

**Mistake 1: Forgotten quotes.**

```python
print(Hello)
# NameError: name 'Hello' is not defined
```

Fix:

```python
print("Hello")
```

**Mistake 2: Unmatched quotes.**

```python
print("Hello)
# SyntaxError: EOL while scanning string literal
```

Fix:

```python
print("Hello")
```

**Mistake 3: Capital P.**

```python
Print("Hello")
# NameError: name 'Print' is not defined
```

Fix:

```python
print("Hello")
```

**Say:**

> "Python is **case-sensitive**. `print` is not the same word as `Print`. Lowercase always."

**Mistake 4: Missing parentheses.**

```python
print "Hello"
# SyntaxError
```

Fix:

```python
print("Hello")
```

---

## Section 5 — Quick Recap (2 minutes)

Close by asking the class these questions out loud:

1. "What does `print` do?"
2. "What character starts a comment?"
3. "Why is `print(Hello)` different from `print("Hello")`?"
4. "Does Python care about capital letters?"

Then hand off to the task:

> "OK, now open `lesson01_printAndComments_Task.ipynb` and work through the exercises. First one to get through all of them, raise your hand and I'll check it."

---

## Vocabulary introduced today

- **Program** — a set of instructions the computer runs.
- **Cell** — a box in a Jupyter notebook where you type code.
- **Function** — a named action the computer can do (like `print`).
- **Argument** — the value you give to a function, written inside the parentheses.
- **String** — text wrapped in quotes.
- **Comment** — a note in your code that Python ignores, marked with `#`.
- **Syntax error** — you typed something Python can't understand.
- **Case-sensitive** — `Print` and `print` are different words to Python.
