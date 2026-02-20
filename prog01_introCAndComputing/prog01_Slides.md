---
marp: true
theme: default
class: invert
paginate: true
---

# Lesson 01: Introduction to C & Computing
## Programming
### Medina County Career Center
**Guest Instructor: Jared Henderson**

---

## Sub-Lesson 01a: Why C and How Computers Work

# Why C Still Matters

- **Lingua franca of computing**: Used everywhere in industry
- **The world runs on C**:
  - Linux kernel, Windows, macOS
  - PostgreSQL, SQLite
  - CPython, Node.js (V8 engine)
- **Performance**: Compiles to fast machine code
- **Trade-off**: No safety net — why Rust exists today
- **Interoperability (FFI)**: Bridges between languages

---

## Sub-Lesson 01a: Why C and How Computers Work

# C vs JavaScript: The Same Program

**JavaScript:**
```javascript
console.log("Hello, World!");
```

**C:**
```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0;
}
```

---

Key differences:
- C requires `#include` (imports) and `main()` function
- C needs explicit types (`int`, `void`)
- C uses braces `{}` for code blocks

---

## Sub-Lesson 01a: Why C and How Computers Work

# Compilation vs Interpretation

| JavaScript | C |
|-----------|---|
| Interpreted at runtime | Compiled before running |
| Engine reads & executes code on the fly | Code converted to machine instructions (binary) |
| Slower but flexible | Faster execution |
| Errors found during execution | Errors found at compile time |

---

**The C Pipeline:**
```
Source Code → Preprocess → Compile → Assemble → Link → Binary
  hello.c      (headers)   (to ASM)   (to obj)  (libs)  (executable)
```

Run with: `gcc hello.c -o hello` → `./hello`

---

## Sub-Lesson 01a: Why C and How Computers Work

# Binary, Hex, and Bytes

Everything in a computer is **bytes** (0–255).

| Decimal | Binary | Hex |
|---------|--------|-----|
| 65 | 01000001 | 0x41 |
| 255 | 11111111 | 0xFF |
| 10 | 00001010 | 0x0A |

**Why hex?** Cleaner than binary, easier than decimal for programmers.

Numbers can **overflow**: if `int` max is 2,147,483,647 and you add 1 → wraps to negative!

---

## Sub-Lesson 01a: Why C and How Computers Work

# ASCII: Characters Are Just Numbers

Computers store characters as numbers using **ASCII**.

```
'A' = 65    'a' = 97    '0' = 48    ' ' = 32
'B' = 66    'b' = 98    '1' = 49    '\n' = 10
```

String `"hello"` in memory:
```
h    e    l    l    o    \0
104  101  108  108  111  0
```

6 bytes total (including null terminator `\0`).

---

## Sub-Lesson 01b: C Fundamentals & The Machine Model

# Types and Memory

C requires **explicit types**:

| Type | Size | Range | Example |
|------|------|-------|---------|
| `int` | 4 bytes | -2.1B to +2.1B | `42` |
| `float` | 4 bytes | ~7 decimals | `3.14` |
| `char` | 1 byte | -128 to 127 | `'A'` |
| `unsigned char` | 1 byte | 0 to 255 | `'X'` |

Use `sizeof()` to check: `sizeof(int)` returns 4.

**Integer division**: `5 / 2 = 2` (not 2.5!)

---

## Sub-Lesson 01b: C Fundamentals & The Machine Model

# Memory Layout: Stack vs Heap

**Memory is a numbered array of bytes:**

```
High Address  [Stack]      (local variables, function calls)
              |-----------|
              |   local x |  automatic, freed when scope ends
              |-----------|
              |  (unused) |
              |-----------|
              [Heap]       (malloc'd memory)
              |  allocated|  must free manually
              |-----------|
Low Address   [Code]       (program instructions)
```
---

- **Stack**: fast, automatic cleanup, limited size
- **Heap**: larger, must `malloc()` and `free()`

---

## Sub-Lesson 01b: C Fundamentals & The Machine Model

# Pointers and Strings

**Pointer**: holds memory address of a variable.

```c
int x = 42;
int *ptr = &x;   // & means "address of"
printf("%d\n", *ptr);  // * means "value at"
```

**Strings**: arrays of `char` with null terminator:

```c
char str[6] = "hello";  // h,e,l,l,o,\0
char *name = "world";   // pointer to first char
printf("%s\n", name);   // %s prints until \0
```

---

## Sub-Lesson 01b: C Fundamentals & The Machine Model

# Functions: Typed Signatures

Functions in C require **explicit types**:

```c
int add(int a, int b) {
    return a + b;
}

void greet(char *name) {
    printf("Hello, %s!\n", name);
}

int getUserInput() {
    int num;
    scanf("%d", &num);   // & = address to store value
    return num;
}
```

- Return type comes first: `int`, `void`, `float`, etc.
- Parameters must be typed: `int a`, `char *name`
- `scanf()` reads from user, needs address (`&`)