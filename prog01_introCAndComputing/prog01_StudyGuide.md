# Lesson 01: Introduction to C and Computing
## Study Guide & Reference

**Programming — Medina County Career Center**

---

This guide is your reference for everything in Lesson 01. Use it while you work through the task files — it has syntax examples, worked problems, and vocabulary you'll need.

---

## 1. BASIC PROGRAM STRUCTURE

Every C program follows the same skeleton. Here's the simplest possible program:

```c
#include <stdio.h>      // Include the standard input/output library

int main() {            // Every C program starts here
    printf("Hello MCCC!\n"); // Print something to the screen
    return 0;           // Tell the OS the program finished successfully
}
```

**What each piece does:**
- `#include <stdio.h>` — loads the library that gives you `printf` and `scanf`
- `int main()` — the entry point; your program always starts running from here
- `return 0;` — signals that the program ended without errors
- Every statement ends with a semicolon `;`
- Code blocks are wrapped in curly braces `{ }`

**How it compares to JavaScript and Python:**

| Concept | JavaScript | Python | C |
|---|---|---|---|
| Print to screen | `console.log("Hi")` | `print("Hi")` | `printf("Hi\n");` |
| Entry point | Just runs top-down | Just runs top-down | Must have `int main()` |
| End of statement | Optional `;` | Newline | Required `;` |
| Code blocks | `{ }` | Indentation | `{ }` |

---

## 2. VARIABLES AND DATA TYPES

In C, you **must** declare what type a variable is before you use it. This is different from JavaScript and Python where the type is figured out automatically.

### Declaring Variables

```c
int age = 17;                // Whole number (integer)
float price = 9.99;          // Decimal number
char grade = 'A';            // Single character (use single quotes)
unsigned char brightness = 200;  // Whole number 0-255 only
```

### How it compares:

| What you want | JavaScript | Python | C |
|---|---|---|---|
| Whole number | `var x = 10;` | `x = 10` | `int x = 10;` |
| Decimal | `var x = 3.14;` | `x = 3.14` | `float x = 3.14;` |
| Character | `var x = 'A';` | `x = 'A'` | `char x = 'A';` |
| Text/String | `var x = "Hi";` | `x = "Hi"` | `char x[] = "Hi";` |

### Data Type Sizes

```
Type               Size        Range
char               1 byte      -128 to 127 (or 0 to 255 unsigned)
int                4 bytes     about -2.1 billion to 2.1 billion
float              4 bytes     decimal numbers (about 7 digits of precision)
double             8 bytes     decimal numbers (about 15 digits of precision)
unsigned char      1 byte      0 to 255
```

### Worked Example: Declaring and Printing Variables

```c
#include <stdio.h>

int main() {
    int studentCount = 25;
    float avgScore = 87.5;
    char section = 'B';

    printf("Section %c has %d students\n", section, studentCount);
    printf("Their average score is %.1f\n", avgScore);

    return 0;
}
```

**Output:**
```
Section B has 25 students
Their average score is 87.5
```

---

## 3. PRINTF — PRINTING OUTPUT

`printf` uses **format specifiers** as placeholders that get replaced by values.

### Format Specifiers

| Specifier | What it prints | Example |
|---|---|---|
| `%d` | Integer | `printf("%d", 42);` → `42` |
| `%f` | Float (6 decimal places) | `printf("%f", 3.14);` → `3.140000` |
| `%.2f` | Float (2 decimal places) | `printf("%.2f", 3.14);` → `3.14` |
| `%c` | Single character | `printf("%c", 'A');` → `A` |
| `%s` | String (text) | `printf("%s", "Hello");` → `Hello` |
| `%p` | Memory address | `printf("%p", &x);` → `0x7fff...` |
| `%4d` | Integer, 4 chars wide | `printf("%4d", 5);` → `   5` |
| `%%` | Literal percent sign | `printf("100%%");` → `100%` |

### Worked Example: Multiple Format Specifiers

```c
#include <stdio.h>

int main() {
    char name[] = "Ryan";
    int age = 30;
    float gpa = 3.85;

    printf("Name: %s\n", name);
    printf("Age: %d\n", age);
    printf("GPA: %.2f\n", gpa);
    printf("All together: %s is %d with a %.2f GPA\n", name, age, gpa);

    return 0;
}
```

**Output:**
```
Name: Ryan
Age: 30
GPA: 3.85
All together: Ryan is 30 with a 3.85 GPA
```

---

## 4. SCANF — USER INPUT

`scanf` reads input from the keyboard. You need the `&` symbol before the variable name (except for strings).

```c
int age;
printf("Enter your age: ");
scanf("%d", &age);           // & means "the address of age"

float price;
printf("Enter price: ");
scanf("%f", &price);         // & is required for float too

char name[50];
printf("Enter name: ");
scanf("%49s", name);         // NO & needed for strings (arrays)
```

### Worked Example: Getting User Input

```c
#include <stdio.h>

int main() {
    int fahrenheit;

    printf("Enter a temperature in Fahrenheit: ");
    scanf("%d", &fahrenheit);

    printf("You entered: %d degrees F\n", fahrenheit);

    return 0;
}
```

**Output (if user types 72):**
```
Enter a temperature in Fahrenheit: 72
You entered: 72 degrees F
```

**Important:** `scanf` with `%s` only reads up to the first space. If you type "John Smith" it will only capture "John."

---

## 5. OPERATORS

### Arithmetic Operators

```c
int a = 10, b = 3;

a + b    // 13  (addition)
a - b    // 7   (subtraction)
a * b    // 30  (multiplication)
a / b    // 3   (integer division — truncates the decimal!)
a % b    // 1   (modulus — the remainder)
```

### Integer Division vs Float Division

This is one of the most common gotchas in C:

```c
// Integer division: both sides are int, result is int
int result1 = 10 / 3;        // result1 = 3 (not 3.33!)

// Float division: at least one side is float, result is float
float result2 = 10.0 / 3;    // result2 = 3.333333
float result3 = (float)10 / 3;  // result3 = 3.333333 (cast forces float)
```

**Rule of thumb:** If you want decimal results, make sure at least one number has a decimal point (like `5.0` instead of `5`) or use a cast like `(float)`.

### Comparison Operators

```c
a == b    // Equal to (double equals!)
a != b    // Not equal to
a > b     // Greater than
a < b     // Less than
a >= b    // Greater than or equal to
a <= b    // Less than or equal to
```

**Common mistake:** Using `=` (assignment) when you mean `==` (comparison). `if (x = 5)` assigns 5 to x — it doesn't compare!

### Logical Operators

```c
a && b    // AND — both must be true
a || b    // OR — either can be true
!a        // NOT — flips true to false
```

---

## 6. IF/ELSE STATEMENTS

```c
if (condition) {
    // runs if condition is true
} else if (anotherCondition) {
    // runs if the first was false and this one is true
} else {
    // runs if nothing above was true
}
```

### Worked Example: If/Else

```c
#include <stdio.h>

int main() {
    int temperature = 45;

    if (temperature >= 80) {
        printf("It's hot outside!\n");
    } else if (temperature >= 60) {
        printf("It's nice outside.\n");
    } else {
        printf("It's cold outside.\n");
    }

    return 0;
}
```

**Output:**
```
It's cold outside.
```

### How it compares:

**JavaScript:**
```javascript
if (temperature >= 80) {
    console.log("It's hot outside!");
}
```

**Python:**
```python
if temperature >= 80:
    print("It's hot outside!")
```

**C:**
```c
if (temperature >= 80) {
    printf("It's hot outside!\n");
}
```

Notice: JavaScript and C look almost identical. Python uses `:` and indentation instead of `{ }`.

---

## 7. FOR LOOPS

```c
for (initialization; condition; increment) {
    // code that repeats
}
```

### Worked Example: Counting with a Loop

```c
#include <stdio.h>

int main() {
    // Print numbers 1 through 5
    for (int i = 1; i <= 5; i++) {
        printf("Count: %d\n", i);
    }

    return 0;
}
```

**Output:**
```
Count: 1
Count: 2
Count: 3
Count: 4
Count: 5
```

### How it compares:

**JavaScript:**
```javascript
for (var i = 1; i <= 5; i++) {
    console.log("Count: " + i);
}
```

**Python:**
```python
for i in range(1, 6):
    print(f"Count: {i}")
```

**C:**
```c
for (int i = 1; i <= 5; i++) {
    printf("Count: %d\n", i);
}
```

Again, JavaScript and C are nearly identical. Python uses `range()` instead.

### Worked Example: Summing Numbers

```c
#include <stdio.h>

int main() {
    int sum = 0;

    for (int i = 1; i <= 10; i++) {
        sum = sum + i;
    }

    printf("The sum of 1-10 is: %d\n", sum);

    return 0;
}
```

**Output:**
```
The sum of 1-10 is: 55
```

---

## 8. FUNCTIONS

In C, functions must specify their **return type** and the **types of their parameters**. Functions must be defined before `main()` or declared with a prototype.

```c
returnType functionName(paramType param1, paramType param2) {
    // function body
    return value;
}
```

### Worked Example: A Simple Function

```c
#include <stdio.h>

// Function defined BEFORE main
int add(int a, int b) {
    return a + b;
}

int main() {
    int result = add(5, 3);
    printf("5 + 3 = %d\n", result);

    return 0;
}
```

**Output:**
```
5 + 3 = 8
```

### How it compares:

**JavaScript:**
```javascript
function add(a, b) {
    return a + b;
}
```

**Python:**
```python
def add(a, b):
    return a + b
```

**C:**
```c
int add(int a, int b) {
    return a + b;
}
```

The big difference: C requires you to say what types go in (`int a, int b`) and what type comes out (`int` before the function name).

### Worked Example: Function That Returns a Character

```c
#include <stdio.h>

char getGrade(int score) {
    if (score >= 90) return 'A';
    else if (score >= 80) return 'B';
    else if (score >= 70) return 'C';
    else if (score >= 60) return 'D';
    else return 'F';
}

int main() {
    int myScore = 85;
    char myGrade = getGrade(myScore);
    printf("Score %d = Grade %c\n", myScore, myGrade);

    return 0;
}
```

**Output:**
```
Score 85 = Grade B
```

### Void Functions (no return value)

If a function doesn't return anything, use `void`:

```c
void sayHello(char name[]) {
    printf("Hello, %s!\n", name);
}
```

---

## 9. ARRAYS

An array holds multiple values of the same type in a row.

```c
int scores[5];                      // Array of 5 integers (uninitialized)
int grades[3] = {90, 85, 92};       // Array initialized with values
char word[6] = "Hello";             // String (array of chars + null terminator)
```

### Accessing Array Elements

Arrays are **0-indexed** — the first element is at position 0:

```c
int nums[4] = {10, 20, 30, 40};
printf("%d\n", nums[0]);   // 10 (first element)
printf("%d\n", nums[1]);   // 20 (second element)
printf("%d\n", nums[3]);   // 40 (last element)
```

### Worked Example: Looping Through an Array

```c
#include <stdio.h>

int main() {
    int temps[5] = {72, 68, 75, 80, 65};
    int size = 5;

    printf("Daily temperatures:\n");
    for (int i = 0; i < size; i++) {
        printf("  Day %d: %d degrees\n", i + 1, temps[i]);
    }

    return 0;
}
```

**Output:**
```
Daily temperatures:
  Day 1: 72 degrees
  Day 2: 68 degrees
  Day 3: 75 degrees
  Day 4: 80 degrees
  Day 5: 65 degrees
```

### Getting Array Size

```c
int nums[] = {10, 20, 30, 40, 50};
int size = sizeof(nums) / sizeof(nums[0]);  // 5
```

This works because `sizeof(nums)` gives the total bytes (20) and `sizeof(nums[0])` gives the size of one element (4), so 20/4 = 5.

---

## 10. STRINGS IN C

In C, a string is just an array of characters that ends with a special **null terminator** character `\0`. This is how C knows where the string ends.

```c
char greeting[] = "Hello";
// This is really: {'H', 'e', 'l', 'l', 'o', '\0'}
// It takes 6 bytes, not 5!
```

### Worked Example: Examining a String

```c
#include <stdio.h>

int main() {
    char word[] = "Cat";

    // Print each character and its ASCII value
    for (int i = 0; word[i] != '\0'; i++) {
        printf("word[%d] = '%c' (ASCII: %d)\n", i, word[i], word[i]);
    }

    return 0;
}
```

**Output:**
```
word[0] = 'C' (ASCII: 67)
word[1] = 'a' (ASCII: 97)
word[2] = 't' (ASCII: 116)
```

### String Functions (need `#include <string.h>`)

```c
strlen(str)        // Returns the length of the string (not counting \0)
strcpy(dest, src)  // Copies src into dest
strcmp(a, b)       // Compares two strings (returns 0 if equal)
```

---

## 11. ASCII AND CHARACTER ENCODING

Every character has a numeric value in the ASCII table. This is how computers store text — as numbers.

**Key ASCII values to know:**
- `'A'` = 65, `'B'` = 66, ..., `'Z'` = 90
- `'a'` = 97, `'b'` = 98, ..., `'z'` = 122
- `'0'` = 48, `'1'` = 49, ..., `'9'` = 57
- Space = 32, `'!'` = 33

**The gap between uppercase and lowercase is always 32:**
- `'A'` (65) + 32 = `'a'` (97)
- `'B'` (66) + 32 = `'b'` (98)

### Worked Example: Character Arithmetic

```c
#include <stdio.h>

int main() {
    char upper = 'A';
    char lower = upper + 32;  // 65 + 32 = 97 = 'a'

    printf("Uppercase: %c (ASCII: %d)\n", upper, upper);
    printf("Lowercase: %c (ASCII: %d)\n", lower, lower);
    printf("Difference: %d\n", lower - upper);

    return 0;
}
```

**Output:**
```
Uppercase: A (ASCII: 65)
Lowercase: a (ASCII: 97)
Difference: 32
```

---

## 12. BINARY AND NUMBER SYSTEMS

Computers store everything as binary (base 2) — just 0s and 1s.

**Decimal to Binary conversion:**
Repeatedly divide by 2 and collect the remainders, then read them bottom-to-top.

```
13 ÷ 2 = 6  remainder 1
 6 ÷ 2 = 3  remainder 0
 3 ÷ 2 = 1  remainder 1
 1 ÷ 2 = 0  remainder 1

Read bottom-to-top: 1101
So 13 in decimal = 1101 in binary
```

**Binary to Decimal conversion:**
Multiply each digit by its power of 2 and add them up.

```
1101 in binary:
(1 × 8) + (1 × 4) + (0 × 2) + (1 × 1) = 8 + 4 + 0 + 1 = 13
```

**Hexadecimal (base 16):**
Uses digits 0-9 and letters A-F (A=10, B=11, C=12, D=13, E=14, F=15).

```
0xFF = (15 × 16) + 15 = 255
0x0A = 10
0x1F = (1 × 16) + 15 = 31
```

---

## 13. INTEGER OVERFLOW

Every data type has a maximum value. When you go past it, the value **wraps around**.

For `unsigned char` (1 byte, range 0-255):
```
254 + 1 = 255  ✓ (still in range)
255 + 1 = 0    ← overflow! wraps back to 0
```

### Worked Example: Seeing Overflow

```c
#include <stdio.h>

int main() {
    unsigned char x = 253;

    for (int i = 0; i < 5; i++) {
        printf("x = %d\n", x);
        x = x + 1;
    }

    return 0;
}
```

**Output:**
```
x = 253
x = 254
x = 255
x = 0
x = 1
```

---

## 14. MEMORY AND POINTERS (PREVIEW)

Every variable lives at a specific address in memory. You can see that address using `&`:

```c
int x = 42;
printf("Value: %d\n", x);       // Prints: 42
printf("Address: %p\n", &x);    // Prints something like: 0x7ffeeb34
printf("Size: %zu bytes\n", sizeof(x));  // Prints: 4
```

A **pointer** is a variable that stores a memory address:

```c
int x = 10;
int *ptr = &x;          // ptr now holds the address of x
printf("%d\n", *ptr);   // Dereference: prints 10 (the value at that address)
```

You'll work more with pointers in later lessons. For now, just know they exist and that `&` gives you an address.

---

## 15. COMPILING AND RUNNING

In the MinGW64 shell:

```bash
gcc myprogram.c -o myprogram.exe    # Compile
./myprogram.exe                     # Run
```

If you get errors, read them — they tell you the line number and what went wrong.

```bash
gcc -Wall myprogram.c -o myprogram.exe   # Compile with all warnings (helpful!)
```

**The compilation pipeline** (what happens behind the scenes):
```
myprogram.c → [Preprocessor] → [Compiler] → [Assembler] → [Linker] → myprogram.exe
```

---

## 16. COMMON INCLUDES

```c
#include <stdio.h>     // printf, scanf
#include <stdlib.h>    // malloc, free, rand
#include <string.h>    // strlen, strcpy, strcmp
#include <math.h>      // sqrt, sin, cos (compile with -lm flag)
#include <ctype.h>     // isupper, islower, toupper, tolower
```

---

## VOCABULARY

**Compiler** — A program that translates source code into machine code the computer can run.

**Interpreter** — A program that reads and runs code line by line without compiling first (like Python and JavaScript).

**Source Code** — The human-readable program text you write.

**Object Code** — Machine-readable binary code produced by the compiler.

**Binary** — A number system using only 0 and 1. The fundamental language of computers.

**Hexadecimal** — A number system using 16 digits (0-9 and A-F). Used to represent binary more compactly.

**ASCII** — American Standard Code for Information Interchange. Assigns numbers to characters so computers can store text.

**Byte** — 8 bits. Can store values from 0 to 255 (unsigned) or -128 to 127 (signed).

**Bit** — The smallest unit of data. A single 0 or 1.

**Data Type** — A classification that says what kind of value a variable holds and how much memory it uses.

**Pointer** — A variable that stores a memory address instead of a regular value.

**Memory Address** — A number that identifies a specific location in the computer's memory.

**Stack** — Memory region for local variables. Automatically managed — memory is freed when variables go out of scope.

**Heap** — Memory region for dynamically allocated data. You must manually free it.

**malloc** — Function that allocates memory on the heap. Must be paired with `free()`.

**free** — Function that releases heap memory allocated by `malloc()`.

**Null Terminator** — The `\0` character that marks the end of a string in C.

**Array** — A collection of same-type values stored in a row in memory. Accessed by index starting at 0.

**sizeof** — An operator that tells you how many bytes a type or variable uses.

**Integer Division** — Division between two integers that throws away the decimal part. `7 / 2 = 3`, not 3.5.

**Overflow** — When a value exceeds the maximum for its data type and wraps around.

---

## ODE COMPETENCIES COVERED

**2.3.1** — ASCII Character Encoding
**2.3.2** — Binary, Hexadecimal, and Overflow
**5.1.7** — Compilers and Compilation
**5.2.1** — Data Types
**5.2.3** — Arithmetic Operations
**5.3.8** — Nested Loops
