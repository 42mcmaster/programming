# prog01b — Functions, Return Types, and Int vs Float

**INSTRUCTOR SOLUTIONS — DO NOT DISTRIBUTE TO STUDENTS**

**Standards: ODE 5.2.1, 5.2.3**

---

## Walkthrough Answers

### Walkthrough 1: Your First Function
**Expected output:**
```
Original: 8
Doubled: 16
Doubling 15 gives: 30
```

### Walkthrough 2: Int vs Float Division
**Expected output:**
```
int / int: 10 / 3 = 3
float / float: 10.0 / 3.0 = 3.3333
(float)int / int: 10 / 3 = 3.3333
Wrong way: 10 / 3 = 3.0000
```

**Why the "Wrong way" is wrong:** Even though the result is stored in a `float`, the division `a / b` happens first as integer division (both `a` and `b` are `int`), giving `3`. That `3` is then converted to `3.0000` when stored in the float. The decimal precision is already lost.

### Walkthrough 3: A Function with Float
**Area for radius 2.5:** 19.63

**Expected output:**
```
Circle with radius 5.0 has area 78.54
Circle with radius 10.0 has area 314.16
Circle with radius 2.5 has area 19.63
```

---

## Task 1: Temperature Converter

**Solution:**
```c
#include <stdio.h>

float fahrenheitToCelsius(float fahrenheit) {
    return (fahrenheit - 32) * 5.0 / 9.0;
}

int main() {
    printf("%.2f F = %.2f C\n", 32.0, fahrenheitToCelsius(32.0));
    printf("%.2f F = %.2f C\n", 212.0, fahrenheitToCelsius(212.0));
    printf("%.2f F = %.2f C\n", 72.0, fahrenheitToCelsius(72.0));
    printf("%.2f F = %.2f C\n", 98.6, fahrenheitToCelsius(98.6));

    return 0;
}
```

**Expected Output:**
```
32.00 F = 0.00 C
212.00 F = 100.00 C
72.00 F = 22.22 C
98.60 F = 37.00 C
```

**Instructor Note:**
This is the critical int-vs-float teaching moment. If a student writes `5 / 9` instead of `5.0 / 9.0`, their output will be all zeros (because `5 / 9 = 0` in integer division). Have them intentionally try the wrong version to see the difference:

```c
// WRONG — integer division
return (fahrenheit - 32) * 5 / 9;    // 5/9 = 0, everything becomes 0

// RIGHT — float division
return (fahrenheit - 32) * 5.0 / 9.0;
```

Also note: `98.6 F = 37.00 C` is normal human body temperature — a good real-world connection.

---

## Task 2: Max of Two Numbers

**Solution:**
```c
#include <stdio.h>

int max(int a, int b) {
    if (a > b) {
        return a;
    } else {
        return b;
    }
}

int main() {
    printf("max(7, 3) = %d\n", max(7, 3));
    printf("max(2, 9) = %d\n", max(2, 9));
    printf("max(-5, -1) = %d\n", max(-5, -1));
    printf("max(4, 4) = %d\n", max(4, 4));

    return 0;
}
```

**Expected Output:**
```
max(7, 3) = 7
max(2, 9) = 9
max(-5, -1) = -1
max(4, 4) = 4
```

**Instructor Note:**
Key teaching points:
- The function must be defined BEFORE `main()` — placing it after causes a compiler error (unless a prototype is used, which we haven't taught yet)
- The equal case (4, 4) returns 4 from the `else` branch — either value works since they're the same
- Alternative one-liner: `return (a > b) ? a : b;` — mention the ternary operator for interested students
- Common mistake: returning `a` or `b` as separate variables instead of the parameter values

Negative number test (`-5, -1`): `-1` is greater than `-5`. Some students may be confused by this — good time to review number lines.

---

## Task 3: Grade Calculator

**Solution:**
```c
#include <stdio.h>

char getGrade(int score) {
    if (score >= 90) {
        return 'A';
    } else if (score >= 80) {
        return 'B';
    } else if (score >= 70) {
        return 'C';
    } else if (score >= 60) {
        return 'D';
    } else {
        return 'F';
    }
}

int main() {
    printf("Score: 95 -> Grade: %c\n", getGrade(95));
    printf("Score: 82 -> Grade: %c\n", getGrade(82));
    printf("Score: 74 -> Grade: %c\n", getGrade(74));
    printf("Score: 61 -> Grade: %c\n", getGrade(61));
    printf("Score: 45 -> Grade: %c\n", getGrade(45));

    return 0;
}
```

**Expected Output:**
```
Score: 95 -> Grade: A
Score: 82 -> Grade: B
Score: 74 -> Grade: C
Score: 61 -> Grade: D
Score: 45 -> Grade: F
```

**Instructor Note:**
- Order matters: checking `>= 90` first, then `>= 80`, etc. guarantees correct ranges
- The function returns a `char` (note the single quotes: `'A'`, not `"A"`)
- `%c` is used to print the char in printf
- Common mistake: checking exact ranges like `score >= 90 && score <= 100` — this works but is unnecessarily verbose since the cascade already handles it
- Edge case discussion: what should happen for scores above 100 or below 0? The current code gives A for >100 and F for <0, which is reasonable

---

## Task 4: Weighted Average Calculator

**Solution:**
```c
#include <stdio.h>

float weightedAverage(float score1, float score2, float score3,
                      float weight1, float weight2, float weight3) {
    return (score1 * weight1) + (score2 * weight2) + (score3 * weight3);
}

int main() {
    float homework = 85.0;
    float midterm = 78.0;
    float finalExam = 92.0;

    float hwWeight = 0.40;
    float midWeight = 0.25;
    float finalWeight = 0.35;

    printf("Homework:   %.2f x %.2f = %.2f\n", homework, hwWeight, homework * hwWeight);
    printf("Midterm:    %.2f x %.2f = %.2f\n", midterm, midWeight, midterm * midWeight);
    printf("Final Exam: %.2f x %.2f = %.2f\n", finalExam, finalWeight, finalExam * finalWeight);

    float grade = weightedAverage(homework, midterm, finalExam,
                                  hwWeight, midWeight, finalWeight);
    printf("Final Grade: %.2f\n", grade);

    return 0;
}
```

**Expected Output:**
```
Homework:   85.00 x 0.40 = 34.00
Midterm:    78.00 x 0.25 = 19.50
Final Exam: 92.00 x 0.35 = 32.20
Final Grade: 85.70
```

**Instructor Note:**
- The function itself is simple — the main work is in organizing the data and testing
- Real-world connection: this is exactly how many grade books calculate final grades
- Common mistake: passing weights that don't sum to 1.0 — the math still works but the result isn't meaningful as a "percentage"
- The detailed output format (showing each component) helps students verify their math manually
- Verification: 34.00 + 19.50 + 32.20 = 85.70 ✓

---

## Common Student Mistakes — Quick Reference

| Mistake | What It Looks Like | Fix |
|---|---|---|
| Integer division | Temperature converter returns all 0s | Use `5.0 / 9.0` not `5 / 9` |
| Function after main | `error: implicit declaration of function` | Move function definition above `main()` |
| Missing return type | `error: expected type-specifier` | Add `int`, `float`, or `char` before function name |
| Wrong return type | Function returns garbage | Match the return type to what you're returning |
| Calling without storing | `max(7, 3);` does nothing visible | Use `printf("%d", max(7, 3))` or store in a variable |
| Char vs String | Using `"A"` instead of `'A'` | Single quotes for `char`, double quotes for strings |
