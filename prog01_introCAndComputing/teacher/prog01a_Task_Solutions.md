# prog01a — Variables, Printing, If/Else, and Loops

**INSTRUCTOR SOLUTIONS — DO NOT DISTRIBUTE TO STUDENTS**

**Standards: ODE 5.1.7, 5.2.1**

---

## Walkthrough Answers

### Walkthrough 1: Hello World
**Expected output:**
```
Hello, World!
I am learning C!
This is program number 1
```

### Walkthrough 2: Variables and Math
**Total cost:** $9.00

**Expected output:**
```
Started with 12 apples
Ate 5 apples
Apples left: 7
Total cost at $0.75 each: $9.00
```

### Walkthrough 3: If/Else and a Loop
**Expected output:**
```
Day 1: 45 degrees - Cold.
Day 2: 62 degrees - Nice.
Day 3: 78 degrees - Nice.
Day 4: 55 degrees - Cold.
Day 5: 90 degrees - Hot!
```

---

## Task 1: Personal Info Printer

**Solution:**
```c
#include <stdio.h>

int main() {
    char name[] = "Alex";
    int age = 17;
    float gpa = 3.5;

    printf("Name: %s\n", name);
    printf("Age: %d\n", age);
    printf("GPA: %.1f\n", gpa);

    return 0;
}
```

**Expected Output:**
```
Name: Alex
Age: 17
GPA: 3.5
```

**Instructor Note:**
Students may use different values which is fine. Key things to check:
- Used `char name[]` or `char name[50]` for the string (not `char name`)
- Used `%s` for string, `%d` for int, `%f` or `%.1f` for float
- Common mistake: trying `printf(name)` without format specifier — this works for strings but is bad practice and dangerous

---

## Task 2: Number Checker

**Solution:**
```c
#include <stdio.h>

int main() {
    int num = 7;

    // Check positive, negative, or zero
    if (num > 0) {
        printf("%d is Positive\n", num);
    } else if (num < 0) {
        printf("%d is Negative\n", num);
    } else {
        printf("%d is Zero\n", num);
    }

    // Check even or odd
    if (num % 2 == 0) {
        printf("%d is Even\n", num);
    } else {
        printf("%d is Odd\n", num);
    }

    return 0;
}
```

**Expected Output (for num = 7):**
```
7 is Positive
7 is Odd
```

**Instructor Note:**
- Students might combine the checks into one block — that's fine as long as both checks work
- Common mistake: using `=` instead of `==` in `num % 2 == 0`
- Some students may not understand modulo — quick recap: 7 % 2 = 1 (remainder), 8 % 2 = 0 (evenly divides)
- Have students test with negative numbers and zero to make sure all branches work

---

## Task 3: Countdown Timer

**Solution:**
```c
#include <stdio.h>

int main() {
    for (int i = 10; i >= 1; i--) {
        printf("%d\n", i);
    }
    printf("Liftoff!\n");

    return 0;
}
```

**Expected Output:**
```
10
9
8
7
6
5
4
3
2
1
Liftoff!
```

**Instructor Note:**
- Key concept: decrementing loop with `i--`
- Common mistakes: using `i > 0` (works but counts to 1) vs `i >= 1` (same result but more readable)
- Some students may try to loop from 1 to 10 and print `10 - i` — creative but less clean
- "Liftoff!" must be OUTSIDE the loop, not inside it

---

## Task 4: Times Table Printer

**Solution:**
```c
#include <stdio.h>

int main() {
    int num;
    printf("Enter a number: ");
    scanf("%d", &num);

    for (int i = 1; i <= 10; i++) {
        printf("%d x %d = %d\n", num, i, num * i);
    }

    return 0;
}
```

**Expected Output (if user enters 5):**
```
Enter a number: 5
5 x 1 = 5
5 x 2 = 10
5 x 3 = 15
5 x 4 = 20
5 x 5 = 25
5 x 6 = 30
5 x 7 = 35
5 x 8 = 40
5 x 9 = 45
5 x 10 = 50
```

**Instructor Note:**
- This is their first time using `scanf` in a task — verify they have `&num` (not just `num`)
- Common mistake: forgetting the `&` in scanf, which causes a crash or garbage values
- Some students may hardcode the number instead of using scanf — redirect them to the requirement
- Good exercise: have them try entering a negative number or 0 and observe the output

---

## Common Student Mistakes — Quick Reference

| Mistake | What It Looks Like | Fix |
|---|---|---|
| Missing semicolon | `error: expected ';'` | Add `;` at end of the line |
| Missing `#include` | `implicit declaration of function 'printf'` | Add `#include <stdio.h>` |
| Using `=` instead of `==` | `if (x = 5)` always true | Change to `if (x == 5)` |
| Forgetting `\n` | Output runs together on one line | Add `\n` inside printf strings |
| Forgetting `&` in scanf | Program crashes or gives garbage | `scanf("%d", &num)` needs the `&` |
| Wrong format specifier | Garbage output or warnings | `%d` for int, `%f` for float, `%s` for string |
