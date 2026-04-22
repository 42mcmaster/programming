# Lesson 09 — `while` Loops, `break`, and `continue` (Teacher Walkthrough)

> **Teacher-only file.** ~20-minute script.

**Student deliverable:** `lesson09_whileLoops_Task.ipynb`
**ODE standards touched:** 5.3.6 (iteration), 5.3.8 (nested structures & loop control), 5.4.2, 5.5.7 (input validation).

---

## Learning Objectives

1. Write a `while` loop that runs as long as a condition is True.
2. Use `break` to exit a loop early.
3. Use `continue` to skip the rest of the current iteration.
4. Build an **input validation loop** that rejects bad input.

---

## Section 1 — `for` vs `while` (2 minutes)

**Say:**

> "A `for` loop is for when you already know how many times you'll repeat — count 10 times, loop through each character, etc. A `while` loop is for when you don't know in advance. It keeps going **while** a condition is still True, and stops when the condition becomes False."

> "Good rule of thumb: 'I know how many' → `for`. 'I keep going until something happens' → `while`."

---

## Section 2 — Basic `while` (5 minutes)

### The anatomy

```python
while CONDITION:
    <body — indented code that repeats>
```

Demo — counting up:

```python
count = 1
while count <= 5:
    print("count =", count)
    count = count + 1
```

**Walk the class through each piece:**

1. `count = 1` — starting value, set BEFORE the loop.
2. `while count <= 5:` — the condition checked each time before running the body.
3. The body prints and then **increments** `count`.
4. When `count` becomes 6, `count <= 5` is False, the loop exits.

**Flag the critical rule:**

> "The condition must **eventually** become False. If it never does, the loop runs forever — an **infinite loop**. Watch what happens if I forget to add 1:"

```python
count = 1
while count <= 5:
    print(count)
    # count = count + 1   ← forgot this
```

> "If you run that, Python will print 1 forever until you hit **Interrupt** (the stop button in the notebook). Every `while` loop needs something inside that makes progress toward the exit condition."

---

## Section 3 — `break` (4 minutes)

**Say:**

> "Sometimes you want to exit a loop in the middle. That's what `break` does. `break` immediately jumps out of the loop, even if the condition is still True."

```python
for i in range(10):
    if i == 5:
        break
    print(i)
# Prints 0, 1, 2, 3, 4 — stops at 5
```

### The classic `while True` + `break` pattern

> "One of the most common patterns in Python: start with `while True:` (which would loop forever), then use `break` inside to exit when you're ready."

```python
while True:
    answer = input("Enter 'quit' to stop: ")
    if answer == "quit":
        break
    print(f"You entered: {answer}")
print("Bye!")
```

> "This pattern is extremely common for menus, sensors, user input that can come in any number of times. We'll use it in the validation section."

---

## Section 4 — `continue` (3 minutes)

**Say:**

> "`continue` is different. It doesn't exit the loop — it just skips the rest of the **current** iteration and jumps to the next one."

```python
for i in range(10):
    if i % 2 == 0:
        continue            # Skip even numbers
    print(i)
# Prints 1, 3, 5, 7, 9 — only odds
```

**Say:**

> "Read that: 'if the number is even, skip to the next iteration.' The `print` line only runs when `continue` did NOT fire."

**`break` vs `continue`:**

| Keyword | Effect |
|---|---|
| `break` | Exits the loop entirely. |
| `continue` | Skips to the next iteration. |

---

## Section 5 — Input validation loop (4 minutes)

**This is the big practical pattern of the lesson. Put this on the board:**

```python
while True:
    VALUE = input(PROMPT)
    if VALUE is valid:
        break
    else:
        print error message
```

Demo — force the user to enter a positive number:

```python
while True:
    text = input("Enter a positive number: ")
    if text.isdigit() and int(text) > 0:
        age = int(text)
        break
    print("That's not a positive number. Try again.")

print(f"Thanks! You entered {age}.")
```

**Step through the logic:**

1. `while True` — loop forever until we `break`.
2. Ask the user for input.
3. Check if it's valid. If it is, convert it, break, done.
4. If it isn't, print an error and loop again.

**Say:**

> "`.isdigit()` is a string method that returns True if the string is all digits (no negative sign, no decimal point). This is a quick-and-clean way to check for a positive integer before you try to convert it. If you want to accept negative numbers or decimals, the check gets fancier — for this class, `.isdigit()` is fine for positive ints."

### Validated menu choice

```python
while True:
    choice = input("Choose (A/B/C): ").upper()
    if choice in ("A", "B", "C"):
        break
    print("Please enter A, B, or C.")

print(f"You chose {choice}.")
```

> "Tiny hint: `in` lets you check membership. `choice in (\"A\", \"B\", \"C\")` is equivalent to `choice == \"A\" or choice == \"B\" or choice == \"C\"`, but cleaner."

---

## Section 6 — Sentinel loop (1 minute)

**Say:**

> "Another classic pattern: keep reading input until the user enters a special 'stop' value. That value is called a **sentinel**."

```python
total = 0
while True:
    text = input("Enter a number (0 to stop): ")
    number = float(text)
    if number == 0:
        break
    total += number
print(f"Total: {total}")
```

> "`0` is the sentinel here. Any legitimate value signals 'keep going,' and `0` signals 'I'm done.'"

---

## Section 7 — Nested loops (1 minute, skim)

**Say:**

> "You can put a loop inside another loop. That's a **nested loop**. The inner loop runs completely each time the outer loop goes once around."

```python
for i in range(3):
    for j in range(3):
        print(f"({i}, {j})", end=" ")
    print()
```

Expected:

```
(0, 0) (0, 1) (0, 2) 
(1, 0) (1, 1) (1, 2) 
(2, 0) (2, 1) (2, 2) 
```

> "The inner loop runs 3 times for every 1 run of the outer loop. Total of 9 prints. Common for grids, tables, and patterns."

---

## Section 8 — Common Mistakes (1 minute)

**Mistake 1: Infinite loop — forgot to update the counter.**

```python
count = 1
while count <= 5:
    print(count)
    # Forgot count += 1 — runs forever
```

**Mistake 2: Condition is always False.**

```python
count = 10
while count < 5:     # Already false, never runs
    print(count)
    count -= 1
```

**Mistake 3: Using `=` in a while condition.**

```python
while count = 5:     # SyntaxError
while count == 5:    # Correct
```

**Mistake 4: `break` or `continue` outside a loop.**

```python
# At the top level of a file
break      # SyntaxError — break only works inside a loop
```

---

## Section 9 — Quick Recap (1 minute)

Ask:

1. "When do you use `for` vs `while`?"
2. "What does every `while` loop need to guarantee it ends?"
3. "What does `break` do? What does `continue` do?"
4. "What's the common pattern for input validation?" (`while True: ... if valid: break`)

Hand off:

> "Open `lesson09_whileLoops_Task.ipynb`."

---

## Vocabulary introduced today

- **while loop** — repeats as long as a condition is True.
- **Infinite loop** — a loop that never ends because its exit condition is never met.
- **break** — exits the loop immediately.
- **continue** — skips the rest of the current iteration, moves to the next.
- **Input validation** — the pattern of looping until the user gives valid data.
- **Sentinel value** — a special input that signals 'stop' (like entering 0 or `quit`).
- **Nested loop** — a loop inside another loop.
