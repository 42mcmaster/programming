# prog01c — Arrays, Strings, and Encoding

**INSTRUCTOR SOLUTIONS — DO NOT DISTRIBUTE TO STUDENTS**

**Standards: ODE 5.2.1, 5.3.8, 2.3.1, 2.3.2**

---

## Walkthrough Answers

### Walkthrough 1: Working with an Array
**Sum:** 490, **Average:** 81.67

**Expected output:**
```
Scores: 88 72 95 64 81 90
Sum: 490
Average: 81.67
```

### Walkthrough 2: Strings and ASCII
**'H'** has ASCII value **72**. **'e'** has ASCII value **101**.

**Expected output:**
```
Examining the string "Hello":

  word[0] = 'H'  ASCII value: 72
  word[1] = 'e'  ASCII value: 101
  word[2] = 'l'  ASCII value: 108
  word[3] = 'l'  ASCII value: 108
  word[4] = 'o'  ASCII value: 111

Fun fact: 'A' = 65, 'a' = 97, difference = 32
'H' + 32 = 'h'
```

### Walkthrough 3: Integer Overflow
**Overflow happens at 255.** It wraps to **0**.

**Expected output:**
```
unsigned char can hold 0 to 255
Starting at 250, adding 1 each time:

  x = 250
  x = 251
  x = 252
  x = 253
  x = 254
  x = 255
  x = 0
  x = 1

Notice: after 255, it wraps back to 0!
This is called INTEGER OVERFLOW.
```

---

## Task 1: Find the Maximum

**Solution:**
```c
#include <stdio.h>

int findMax(int numbers[], int size) {
    int maxValue = numbers[0];

    for (int i = 1; i < size; i++) {
        if (numbers[i] > maxValue) {
            maxValue = numbers[i];
        }
    }

    return maxValue;
}

int main() {
    int numbers[] = {15, 3, 42, 8, 23, 1, 99, 7};
    int size = sizeof(numbers) / sizeof(numbers[0]);

    int max = findMax(numbers, size);
    printf("Maximum value: %d\n", max);

    return 0;
}
```

**Expected Output:**
```
Maximum value: 99
```

**Instructor Note:**
Key concepts:
- Start with `numbers[0]` as the assumed max, then loop from index `1`
- The `sizeof` trick: `sizeof(numbers)` = 32 bytes (8 ints × 4 bytes), `sizeof(numbers[0])` = 4 bytes, so 32/4 = 8 elements
- Arrays in C decay to pointers when passed to functions, so you MUST pass the size separately
- Common mistake: starting `maxValue` at 0 — this fails if all numbers are negative
- Common mistake: starting the loop at 0 instead of 1 — works but does an unnecessary comparison

Alternative approach some students may try:
```c
int maxValue = numbers[0];
for (int i = 0; i < size; i++) {  // starting at 0 is fine, just redundant
    if (numbers[i] > maxValue) {
        maxValue = numbers[i];
    }
}
```
This is perfectly acceptable — the only difference is one extra comparison.

---

## Task 2: ASCII Explorer

**Solution:**
```c
#include <stdio.h>

char toUpper(char c) {
    return c - 32;
}

int main() {
    // Part A: Print A-Z with ASCII values
    printf("=== ASCII Table: A-Z ===\n");
    for (char c = 'A'; c <= 'Z'; c++) {
        printf("'%c' = %d\n", c, c);
    }

    printf("\n");

    // Part B: Test toUpper function
    printf("=== toUpper Tests ===\n");
    printf("'%c' -> '%c'\n", 'h', toUpper('h'));
    printf("'%c' -> '%c'\n", 'e', toUpper('e'));
    printf("'%c' -> '%c'\n", 'l', toUpper('l'));
    printf("'%c' -> '%c'\n", 'p', toUpper('p'));

    return 0;
}
```

**Expected Output:**
```
=== ASCII Table: A-Z ===
'A' = 65
'B' = 66
'C' = 67
'D' = 68
'E' = 69
'F' = 70
'G' = 71
'H' = 72
'I' = 73
'J' = 74
'K' = 75
'L' = 76
'M' = 77
'N' = 78
'O' = 79
'P' = 80
'Q' = 81
'R' = 82
'S' = 83
'T' = 84
'U' = 85
'V' = 86
'W' = 87
'X' = 88
'Y' = 89
'Z' = 90

=== toUpper Tests ===
'h' -> 'H'
'e' -> 'E'
'l' -> 'L'
'p' -> 'P'
```

**Instructor Note:**
Part A teaching points:
- You can use a `char` as a loop variable — `char c = 'A'; c <= 'Z'; c++` works because chars are just small integers
- Printing with `%c` shows the character, `%d` shows the number
- This is a great way to memorize that A=65, Z=90

Part B teaching points:
- Subtracting 32 from a lowercase ASCII value gives the uppercase version
- This only works for letters! Calling `toUpper('5')` would give garbage
- A more robust version would check `if (c >= 'a' && c <= 'z')` first
- The standard library has `toupper()` in `<ctype.h>`, but writing our own teaches the concept

---

## Task 3: Decimal to Binary Converter

**Solution:**
```c
#include <stdio.h>

int main() {
    int num = 13;
    int binary[32];
    int count = 0;

    int temp = num;
    while (temp > 0) {
        binary[count] = temp % 2;
        temp = temp / 2;
        count++;
    }

    printf("Decimal: %d\n", num);
    printf("Binary: ");
    for (int i = count - 1; i >= 0; i--) {
        printf("%d", binary[i]);
    }
    printf("\n");

    return 0;
}
```

**Expected Output:**
```
Decimal: 13
Binary: 1101
```

**Instructor Note:**
Walk through the algorithm step by step for students who are stuck:

```
temp = 13
  13 % 2 = 1  → binary[0] = 1,  temp = 13/2 = 6
  6  % 2 = 0  → binary[1] = 0,  temp = 6/2  = 3
  3  % 2 = 1  → binary[2] = 1,  temp = 3/2  = 1
  1  % 2 = 1  → binary[3] = 1,  temp = 1/2  = 0  → stop

binary array: {1, 0, 1, 1}
Print reverse: 1101
```

Key points:
- The remainders come out in reverse order, so we store them in an array and print backwards
- We use a `temp` variable so we don't destroy the original `num`
- `int binary[32]` — 32 is more than enough bits for any int value
- Edge case: if `num` is 0, the while loop never executes and nothing prints. Students can add a special case: `if (num == 0) printf("0");`

**Verification for bonus values:**
- 8 → 1000
- 42 → 101010
- 255 → 11111111

---

## Task 4: String Length Counter

**Solution:**
```c
#include <stdio.h>

int myStrlen(char *s) {
    int count = 0;
    while (s[count] != '\0') {
        count++;
    }
    return count;
}

int main() {
    char str1[] = "Hello";
    printf("\"%s\" has length %d\n", str1, myStrlen(str1));

    char str2[] = "C Programming";
    printf("\"%s\" has length %d\n", str2, myStrlen(str2));

    char str3[] = "";
    printf("\"%s\" has length %d\n", str3, myStrlen(str3));

    return 0;
}
```

**Expected Output:**
```
"Hello" has length 5
"C Programming" has length 13
"" has length 0
```

**Instructor Note:**
This exercise teaches the fundamental concept that C strings are null-terminated:
- `"Hello"` is actually stored as `{'H', 'e', 'l', 'l', 'o', '\0'}` — 6 bytes, but length 5
- The null terminator `\0` is NOT counted in the length
- The empty string `""` is just `{'\0'}` — one byte, length 0
- This is how ALL string functions in C know where a string ends

Key teaching moment: This is DIFFERENT from Python and JavaScript where strings know their own length. In C, you must scan for the `\0` every time, which is why C string operations can be slower.

Common mistakes:
- Using `strlen()` — the whole point is to write it yourself
- Off-by-one: counting the `\0` in the length
- Forgetting the empty string test case

Alternative implementation some students may try:
```c
int myStrlen(char *s) {
    int i;
    for (i = 0; s[i] != '\0'; i++) {
        // empty body — just counting
    }
    return i;
}
```
This is equivalent and perfectly fine.

---

## Common Student Mistakes — Quick Reference

| Mistake | What It Looks Like | Fix |
|---|---|---|
| Array out of bounds | Garbage values or crash | Check loop uses `< size`, not `<= size` |
| Not printing in reverse | Binary output is backwards | Loop from `count-1` down to `0` |
| Initializing max to 0 | Fails with all-negative arrays | Use `numbers[0]` as initial max |
| Counting null terminator | String length off by one | Stop when you hit `'\0'`, don't count it |
| Modifying original value | Can't print original number | Use a `temp` variable for the division loop |
| Using `strlen()` in Task 4 | Defeats the purpose | Write the loop manually |
