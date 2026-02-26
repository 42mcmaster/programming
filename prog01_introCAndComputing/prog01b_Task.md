# prog01b — Functions, Return Types, and Int vs Float

**Programming — Medina County Career Center**
**Standards: ODE 5.2.1, 5.2.3**

---

## Before You Start

By now you should be comfortable creating `.c` files in VS Code, compiling in MinGW64, and running your programs. If you need a refresher on any syntax, check the **Study Guide**.

For each program:
1. Create a new `.c` file in VS Code
2. Write (or paste) the code
3. Compile with: `gcc filename.c -o filename.exe`
4. Run with: `./filename.exe`

---

## Part 1: Walkthrough Examples

These examples introduce functions and the difference between integer and float math.

---

### Walkthrough 1: Your First Function (Copy-Paste)

**Copy and paste** this program into a new file called `double_it.c`:

```c
#include <stdio.h>

// This function takes an integer and returns it doubled
int doubleValue(int x) {
    return x * 2;
}

int main() {
    int original = 8;
    int doubled = doubleValue(original);

    printf("Original: %d\n", original);
    printf("Doubled: %d\n", doubled);
    printf("Doubling 15 gives: %d\n", doubleValue(15));

    return 0;
}
```

Compile and run it:
```
gcc double_it.c -o double_it.exe
./double_it.exe
```

**Question:** What were the three lines of output?

```
YOUR ANSWER:


```

**What to notice:**
- `int doubleValue(int x)` — the first `int` is the **return type**, `int x` is the **parameter type**
- The function is defined **above** `main()` so the compiler knows about it
- You can call a function with a variable (`doubleValue(original)`) or a literal (`doubleValue(15)`)
- The function returns a value that you can store in a variable or print directly

---

### Walkthrough 2: Int vs Float Division (Type This One)

This is one of the **most important** things to understand in C. **Type this program** into `division.c`:

```c
#include <stdio.h>

int main() {
    // Integer division: both sides are int
    int a = 10;
    int b = 3;
    int intResult = a / b;
    printf("int / int: %d / %d = %d\n", a, b, intResult);

    // Float division: at least one side is float
    float c = 10.0;
    float d = 3.0;
    float floatResult = c / d;
    printf("float / float: %.1f / %.1f = %.4f\n", c, d, floatResult);

    // Mixed: casting int to float
    float castResult = (float)a / b;
    printf("(float)int / int: %d / %d = %.4f\n", a, b, castResult);

    // The WRONG way (common mistake)
    float wrongResult = a / b;  // Division happens as int FIRST, then becomes float
    printf("Wrong way: %d / %d = %.4f\n", a, b, wrongResult);

    return 0;
}
```

Compile and run it:
```
gcc division.c -o division.exe
./division.exe
```

**Question:** What was the "Wrong way" result? Why is it wrong?

```
YOUR ANSWER:


```

**What to notice:**
- `10 / 3` as integers gives `3` — the decimal part is thrown away (not rounded!)
- `10.0 / 3.0` as floats gives `3.3333`
- `(float)a / b` forces float division even with int variables
- Just storing the result in a float (`float wrongResult = a / b`) does NOT fix it — the integer division already happened

---

### Walkthrough 3: A Function with Float (Type This One)

**Type this program** into `circle.c`:

```c
#include <stdio.h>

float circleArea(float radius) {
    float pi = 3.14159;
    return pi * radius * radius;
}

void printCircleInfo(float radius) {
    float area = circleArea(radius);
    printf("Circle with radius %.1f has area %.2f\n", radius, area);
}

int main() {
    printCircleInfo(5.0);
    printCircleInfo(10.0);
    printCircleInfo(2.5);

    return 0;
}
```

Compile and run it:
```
gcc circle.c -o circle.exe
./circle.exe
```

**Question:** What was the area for a circle with radius 2.5?

```
YOUR ANSWER:


```

**What to notice:**
- `float circleArea(float radius)` — takes a float, returns a float
- `void printCircleInfo(float radius)` — `void` means this function **does not return** anything; it just prints
- One function can call another function (`printCircleInfo` calls `circleArea`)
- `%.2f` limits the output to 2 decimal places

---

## Part 2: Your Tasks

Use the Study Guide and walkthrough examples as reference. For each task, create a new `.c` file.

---

### Task 1: Temperature Converter

Create a file called `tempconv.c`.

**What to do:**
Write a function called `fahrenheitToCelsius` that takes a `float` temperature in Fahrenheit and returns the Celsius equivalent. The formula is:

**C = (F - 32) × 5.0 / 9.0**

**Important:** Use `5.0` and `9.0`, not `5` and `9`. If you use integers, you'll get integer division and wrong answers.

In `main()`, test your function with these values: 32°F, 212°F, 72°F, and 98.6°F.

**Here's how it looks in JavaScript and Python:**

**JavaScript:**
```javascript
function fahrenheitToCelsius(f) {
    return (f - 32) * 5 / 9;
}
console.log(fahrenheitToCelsius(32));   // 0
console.log(fahrenheitToCelsius(212));  // 100
```

**Your C starter code:**
```c
#include <stdio.h>

// Write your fahrenheitToCelsius function here
// Remember: return type is float, parameter type is float

int main() {
    // Call your function with 32, 212, 72, and 98.6
    // Print each result using printf with %.2f
    // Format: "XX.XX F = XX.XX C"

    return 0;
}
```

**Expected output:**
```
32.00 F = 0.00 C
212.00 F = 100.00 C
72.00 F = 22.22 C
98.60 F = 37.00 C
```

---

### Task 2: Max of Two Numbers

Create a file called `maxnum.c`.

**What to do:**
Write a function called `max` that takes two integers and returns the larger one. If they're equal, it can return either. Test it in `main()` with at least 4 different pairs of numbers, including a case where they're equal.

**Here's how it looks in Python:**
```python
def max(a, b):
    if a > b:
        return a
    else:
        return b
```

**Your C starter code:**
```c
#include <stdio.h>

// Write your max function here
// Takes two ints, returns an int

int main() {
    // Test with: (7, 3), (2, 9), (-5, -1), (4, 4)
    // Print each result like: "max(7, 3) = 7"

    return 0;
}
```

**Expected output:**
```
max(7, 3) = 7
max(2, 9) = 9
max(-5, -1) = -1
max(4, 4) = 4
```

---

### Task 3: Grade Calculator

Create a file called `grades.c`.

**What to do:**
Write a function called `getGrade` that takes an integer score (0-100) and returns a `char` representing the letter grade:
- 90-100: A
- 80-89: B
- 70-79: C
- 60-69: D
- 0-59: F

Test it in `main()` with scores: 95, 82, 74, 61, 45.

**Your C starter code:**
```c
#include <stdio.h>

// Write your getGrade function here
// Takes an int (score), returns a char (letter grade)
// Use if/else if/else to check the ranges

int main() {
    // Test with 95, 82, 74, 61, 45
    // Print each like: "Score: 95 -> Grade: A"

    return 0;
}
```

**Expected output:**
```
Score: 95 -> Grade: A
Score: 82 -> Grade: B
Score: 74 -> Grade: C
Score: 61 -> Grade: D
Score: 45 -> Grade: F
```

---

### Task 4: Weighted Average Calculator

Create a file called `weighted.c`.

**What to do:**
Write a function called `weightedAverage` that takes three float scores and three float weights, and returns the weighted average.

**Formula:** `(score1 × weight1) + (score2 × weight2) + (score3 × weight3)`

The weights should add up to 1.0 (like 0.5, 0.3, 0.2).

In `main()`, calculate a student's final grade where:
- Homework = 85, weight = 0.40
- Midterm = 78, weight = 0.25
- Final Exam = 92, weight = 0.35

**Your C starter code:**
```c
#include <stdio.h>

// Write your weightedAverage function here
// Takes 6 floats (3 scores and 3 weights), returns a float

int main() {
    // Calculate the weighted average for the homework, midterm, and final
    // Print it like: "Final Grade: XX.XX"

    return 0;
}
```

**Expected output:**
```
Homework:   85.00 x 0.40 = 34.00
Midterm:    78.00 x 0.25 = 19.50
Final Exam: 92.00 x 0.35 = 32.20
Final Grade: 85.70
```

---

## Compilation Reminder

```
gcc filename.c -o filename.exe
./filename.exe
```

Common function mistakes to watch for:
- Forgetting to define the function **above** `main()`
- Mismatched return type (declaring `int` but returning a `float`)
- Forgetting to use `5.0` instead of `5` for float division
- Not storing the return value: `max(7, 3);` does nothing unless you `printf` it or store it

---

## Submission Checklist

- [ ] All walkthrough questions answered
- [ ] `tempconv.c` — compiles, runs, correct Celsius values
- [ ] `maxnum.c` — compiles, runs, returns the larger number in all cases
- [ ] `grades.c` — compiles, runs, correct letter grades for all scores
- [ ] `weighted.c` — compiles, runs, correct weighted average
- [ ] All code has comments explaining what it does
