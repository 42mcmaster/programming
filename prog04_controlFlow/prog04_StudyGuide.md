# Lesson 04: Control Flow — Study Guide

**Instructor:** Ryan McMaster
**Course:** Programming, Medina County Career Center
**ODE Standards:** 5.3.3 (conditionals), 5.3.5 (loops), 5.3.8 (loop control)

---

## 1. Boolean
A data type with only two values: **True** or **False**. Used to represent logical conditions.
```python
isRaining = True
isWarm = False
```

## 2. True
The boolean value representing "yes" or "affirmative." Capitalized in Python (unlike C's `true`).
```python
hasLicense = True
```

## 3. False
The boolean value representing "no" or "negative." Capitalized in Python (unlike C's `false`).
```python
isEmpty = False
```

## 4. Comparison Operator
A symbol that compares two values and returns a boolean (True or False). Examples: `==`, `!=`, `<`, `>`, `<=`, `>=`.
```python
age = 16
isAdult = age >= 18  # Comparison returns False
```

## 5. if
A control structure that executes a block of code **only if** a condition is True.
```python
if score >= 90:
    print("Excellent!")
```

## 6. elif
Short for "else if." Allows multiple conditions to be checked in sequence. Executes only if previous conditions were False.
```python
if score >= 90:
    print("A")
elif score >= 80:
    print("B")
```

## 7. else
Executes a block of code if all previous conditions (if/elif) were False. Optional, catches all remaining cases.
```python
if age >= 18:
    print("Adult")
else:
    print("Minor")
```

## 8. and
Logical operator that returns True **only if both** conditions are True. (C equivalent: `&&`)
```python
if age >= 16 and hasLicense:
    print("Can drive!")
```

## 9. or
Logical operator that returns True **if at least one** condition is True. (C equivalent: `||`)
```python
if isSunny or isWarmer:
    print("Go to the beach")
```

## 10. not
Logical operator that **reverses** a boolean value. True becomes False, False becomes True. (C equivalent: `!`)
```python
if not isEmpty:
    print("Container has items")
```

## 11. for loop
A control structure that repeats a block of code a set number of times or for each item in a sequence. Simpler than C's `for(i=0; i<n; i++)`.
```python
for i in range(5):
    print(i)
```

## 12. range()
A function that generates a sequence of numbers. `range(5)` produces 0, 1, 2, 3, 4.
```python
for i in range(5):  # 0 to 4
    print(i)
for i in range(1, 6):  # 1 to 5
    print(i)
for i in range(0, 10, 2):  # 0, 2, 4, 6, 8
    print(i)
```

## 13. while loop
A control structure that repeats a block of code **while** a condition is True. Same concept as C.
```python
count = 0
while count < 5:
    print(count)
    count = count + 1
```

## 14. break
A keyword that **immediately exits** a loop, even if the condition is still True.
```python
for i in range(10):
    if i == 5:
        break  # Exit loop
    print(i)
```

## 15. continue
A keyword that **skips the rest** of the current iteration and jumps to the next iteration.
```python
for i in range(5):
    if i == 2:
        continue  # Skip this iteration
    print(i)  # Prints 0, 1, 3, 4
```

## 16. Accumulator
A variable that **accumulates** a value as a loop runs. Used to calculate running totals, sums, or products.
```python
total = 0  # Accumulator
for i in range(1, 6):
    total = total + i  # Add to accumulator
print(total)  # 15
```

## 17. Sentinel Value
A special value that signals the **end of input or a loop**. Often used in while loops to allow a user to stop entering data.
```python
while True:
    userInput = input("Enter a number (or 'quit'): ")
    if userInput == "quit":  # "quit" is the sentinel
        break
    print("You entered:", userInput)
```

## 18. Nested Loop
A loop **inside another loop**. The inner loop runs completely for each iteration of the outer loop.
```python
for i in range(3):
    for j in range(3):
        print(f"({i}, {j})")
```

## 19. Input Validation Loop
A loop that **repeats until valid input is received**. Ensures user enters correct data before proceeding.
```python
while True:
    userAge = input("Enter your age: ")
    if userAge.isdigit() and int(userAge) >= 0:
        userAge = int(userAge)
        break
    print("Invalid input. Please enter a positive number.")
print("Your age is", userAge)
```

## 20. Infinite Loop
A loop that **never ends** because the condition is always True. Often intentional (with `break`), sometimes a mistake.
```python
# Intentional infinite loop with break
while True:
    userInput = input("Enter something: ")
    if userInput == "exit":
        break
```

---

## Quick Reference: Python vs. C

| Concept | C | Python |
|---------|---|--------|
| Boolean values | `true`, `false` | `True`, `False` |
| Blocks | `{ }` braces | **Indentation** |
| if/else | `if (x) { }` | `if x:` |
| Logical AND | `&&` | `and` |
| Logical OR | `||` | `or` |
| Logical NOT | `!` | `not` |
| for loop | `for(i=0;i<n;i++)` | `for i in range(n):` |
| while loop | `while(x) { }` | `while x:` |
| Break loop | `break;` | `break` |
| Skip iteration | `continue;` | `continue` |

---

## ODE Standards Alignment

**5.3.3:** Students demonstrate conditional (if/elif/else) logic.
**5.3.5:** Students apply iteration (for/while) loops.
**5.3.8:** Students use break, continue, and loop control statements.
