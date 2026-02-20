---
marp: true
theme: default
class: invert
paginate: true
---

# Lesson 09: BPA Contest Prep

## Programming
### Medina County Career Center
Instructor: Ryan McMaster

---

## Contest Reality: Your Code Can't Crash

**In a BPA contest:**
- You have limited time to solve multiple problems
- Bad input happens—your code must handle it gracefully
- One crash = zero points on that problem
- You need speed AND correctness

**Three Focus Areas:**
1. Error Handling & Robust Code
2. Algorithm Building Blocks
3. Contest Strategy & Practice

---

## Sub-Lesson 09a: Error Handling

**Why it matters for contests:**
- Input validation prevents crashes
- try/except blocks catch runtime errors
- Defensive programming = reliable solutions

**Common Exceptions:**
- `ValueError`: Bad data type or format
- `TypeError`: Wrong type for operation
- `ZeroDivisionError`: Divide by zero
- `FileNotFoundError`: File doesn't exist

**Contest Strategy:** Always validate input before processing.

---

## Sub-Lesson 09b: Algorithm Practice

**String Algorithms:**
- Palindrome: reads the same forwards and backwards
- Anagram: rearrangement of letters
- Caesar cipher: shift characters by fixed amount

**Math Algorithms:**
- Prime checking: divisibility test
- Factorial: n × (n-1) × ... × 1
- Fibonacci: each term is sum of previous two

**Time Complexity Awareness:**
- O(n): scan a list once
- O(n²): nested loops
- Nested loops = slow in contests with large input

---

## Sub-Lesson 09c: Contest Strategy

**BPA Contest Format:**
- 8-10 short problems per test
- 90 minutes total
- ~9-11 minutes per problem average
- Problems increase in difficulty

**Problem-Solving Steps:**
1. Read carefully—understand I/O format exactly
2. Plan your approach (pseudocode)
3. Code and test with sample input
4. Test edge cases (empty, negative, boundary values)
5. Submit and move on

**Time Management:** If stuck >5 min, skip and return later.

---

## Contest-Style Problem: Example

**Problem:** Count character types in a string

**Input:** "Hello123!"

**Output:**
```
Uppercase: 1
Lowercase: 4
Digits: 3
Special: 1
```

**Key:** Understand format exactly. Handle empty strings. Validate input.

---

## Hands-On Activities

**Task 09a:** Error handling patterns
- Wrap code in try/except
- Input validation function
- File reading with error handling
- Robust calculator

**Task 09b:** Algorithm building blocks
- isPrime, factorial, Fibonacci
- Palindrome, anagram checkers
- Find duplicates in list

**Task 09c:** BPA-style practice
- 8 contest-format problems
- Clear input/output specs
- Timed practice

---

## Independent Challenge: Mock Contest

**Task 09 (DIY):** 5 timed problems (45 minutes)
- Different from guided practice
- Real contest conditions
- You manage your own time
- This is your final check before the actual BPA contest

**What You'll Learn:** Speed, accuracy, and problem-solving under pressure.

---

## Learning Outcomes

By the end of this lesson, you will:
- ✓ Write try/except blocks and validate input
- ✓ Implement core contest algorithms (prime, palindrome, Fibonacci, etc.)
- ✓ Solve contest-style problems quickly and correctly
- ✓ Manage time effectively in a timed environment
- ✓ Test edge cases and handle errors gracefully
