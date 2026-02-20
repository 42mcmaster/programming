# Lesson 09: BPA Contest Prep — Study Guide

**Instructor:** Ryan McMaster
**Course:** Programming (CTE) | Medina County Career Center
**Ohio Standards:** ODE 5.2.3, 5.3.5, 5.3.8, 5.4.6, 5.4.7

---

## Key Terms & Concepts

### Error Handling

**Exception**
A runtime error that interrupts program execution. Examples: division by zero, file not found, invalid input type.

**try Block**
Section of code where an error might occur. Python attempts to execute it; if an exception happens, control jumps to the except block.

**except Block**
Code that executes only if an exception occurs in the try block. Lets your program recover gracefully instead of crashing.

Example:
```python
try:
    num = int(input("Enter a number: "))
    result = 10 / num
except ZeroDivisionError:
    print("Cannot divide by zero")
except ValueError:
    print("That's not a number")
```

**ValueError**
Raised when a function receives an argument of the correct type but an inappropriate value. Example: `int("hello")` causes ValueError.

**TypeError**
Raised when an operation or function is applied to an object of an inappropriate type. Example: `len(42)` causes TypeError.

**ZeroDivisionError**
Raised when division or modulo operation is performed with zero as the divisor. Example: `10 / 0`.

**FileNotFoundError**
Raised when an attempt is made to open a file that does not exist. Example: `open("missing.txt")`.

**Defensive Programming**
Practice of writing code that anticipates and handles errors, invalid input, and unexpected conditions before they cause a crash. In contests: validate input, check list bounds, handle empty inputs.

---

### Algorithms & Problem-Solving

**Algorithm**
Step-by-step procedure to solve a problem. In contests, you choose the right algorithm for the problem constraints. A slow algorithm on large input = timeout = no points.

**Palindrome**
String or number that reads the same forwards and backwards. Example: "racecar" or 12321. Contest use: check if input string is a palindrome, or find longest palindrome substring.

**Anagram**
Word or phrase formed by rearranging letters of another word. Example: "listen" and "silent". Contest use: check if two words are anagrams (same letters, different order).

**Prime Number**
Natural number greater than 1 that has no positive divisors other than 1 and itself. Examples: 2, 3, 5, 7, 11. Contest use: check if number is prime, find all primes up to n.

Algorithm:
```python
def isPrime(n):
    if n < 2:
        return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False
    return True
```

**Factorial**
Product of all positive integers from 1 to n (denoted n!). Example: 5! = 5 × 4 × 3 × 2 × 1 = 120. Contest use: combinatorics, permutations.

Iterative approach (better for contests):
```python
def factorial(n):
    result = 1
    for i in range(2, n + 1):
        result *= i
    return result
```

**Fibonacci Sequence**
Sequence where each number is the sum of the two preceding ones: 0, 1, 1, 2, 3, 5, 8, 13, ... Contest use: generate Fibonacci numbers, find nth Fibonacci term.

Generator approach (memory-efficient):
```python
def fibonacci(n):
    a, b = 0, 1
    for _ in range(n):
        yield a
        a, b = b, a + b
```

**Binary Search**
Efficient algorithm that finds an element in a sorted list by repeatedly dividing the search space in half. Time complexity: O(log n). Only works on sorted data. Much faster than linear search for large lists.

**Time Complexity**
Measure of how an algorithm's runtime grows with input size. In contests:
- O(n): linear—scan list once, acceptable for n ≤ 10⁶
- O(n²): quadratic—nested loops, acceptable for n ≤ 10⁴
- O(n³): cubic—rarely acceptable in contests
- Nested loops = slow; avoid if possible

**Edge Case**
Boundary or extreme input that tests if your solution handles all scenarios. Examples:
- Empty list or string
- Single element
- Negative numbers
- Zero
- Maximum/minimum values
- Duplicate elements

In contests: test edge cases before submitting. A solution that works on sample input but fails on edge cases = partial/no credit.

---

## Quick Reference: Error Handling Pattern

```python
# Basic try/except
try:
    # risky code here
    pass
except SpecificException:
    # handle specific error
    pass
except AnotherException:
    # handle another error
    pass
else:
    # executes if no exception
    pass
finally:
    # always executes (cleanup, close files)
    pass
```

---

## Quick Reference: Common Contest Algorithms

### Check if String is Palindrome
```python
s = "racecar"
print(s == s[::-1])  # True
```

### Check if Two Words are Anagrams
```python
def isAnagram(word1, word2):
    return sorted(word1) == sorted(word2)
```

### Check if Number is Prime
```python
def isPrime(n):
    if n < 2:
        return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False
    return True
```

### Calculate Factorial
```python
def factorial(n):
    result = 1
    for i in range(2, n + 1):
        result *= i
    return result
```

### Generate Fibonacci Sequence
```python
def fibonacci(n):
    a, b = 0, 1
    for _ in range(n):
        yield a
        a, b = b, a + b
```

### Find Duplicates in List
```python
numbers = [1, 2, 3, 2, 4, 1]
duplicates = list(set([x for x in numbers if numbers.count(x) > 1]))
```

---

## Ohio Standards Alignment

- **5.2.3:** Implement algorithms using sequences, nested loops, and decision structures.
- **5.3.5:** Use dictionaries and lists to manage collections of data.
- **5.3.8:** Apply error handling techniques and exception management.
- **5.4.6:** Optimize code for efficiency and readability.
- **5.4.7:** Apply debugging strategies and testing methodologies.

---

## Contest Tips Summary

1. **Read Carefully:** Understand input/output format exactly.
2. **Test Edge Cases:** Empty, single, negative, boundary values.
3. **Handle Errors:** Use try/except. Validate input.
4. **Time Management:** ~9 min per problem. Skip if stuck >5 min.
5. **Code Style Matters Less:** In contests, correctness > style. But readable code is easier to debug.
6. **Know Your Algorithms:** Palindrome, anagram, prime, factorial, Fibonacci are frequent.
7. **Test Before Submitting:** Run sample input/output first.

---

## Additional Resources

- BPA Official Website: bpa.org (contest rules, past tests)
- Python Documentation: python.org (str methods, list methods, built-in functions)
- LeetCode / HackerRank: Free timed practice problems
- Your Instructor: Office hours for algorithm questions

---

*Last Updated: February 2025*
