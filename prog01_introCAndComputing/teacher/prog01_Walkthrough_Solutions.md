# prog01 Walkthrough — INSTRUCTOR SOLUTIONS

**DO NOT DISTRIBUTE TO STUDENTS**

**Programming — Medina County Career Center**

---

This is the instructor companion to the student walkthrough. It follows the same structure with added teaching notes.

---

## Part 1 — Install the GCC Compiler

Students open `C:\msys64\mingw64.exe` and run:

```
pacman -S mingw-w64-x86_64-gcc
```

Then verify with `gcc --version`.

**Instructor Note:** If a student gets `command not found` after installing, have them close the MinGW64 window and reopen it. If the install itself fails, try `pacman -Syu` first to update the package database, then retry the gcc install. On rare occasions the school firewall blocks pacman — if that happens, talk to IT.

---

## Part 2 — Hello World

Students create `~/c_practice/` and write `hello.c`:

```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0;
}
```

Compile: `gcc hello.c -o hello.exe`
Run: `./hello.exe`

**Instructor Note:** Common mistakes at this stage — missing semicolons, forgetting the `\n`, writing `#Include` instead of `#include`. If a student gets "undefined reference to WinMain," they probably named their file wrong or forgot `main()`. Have them re-check the code character by character. Celebrate this moment — it's their first compiled program.

---

## Part 3 — Basic Math

Complete `math_test.c`:

```c
#include <stdio.h>

int main() {
    int a = 10;
    int b = 3;

    printf("a + b = %d\n", a + b);
    printf("a - b = %d\n", a - b);
    printf("a * b = %d\n", a * b);
    printf("a / b = %d\n", a / b);
    printf("a %% b = %d\n", a % b);

    return 0;
}
```

**Expected Output:**

```
a + b = 13
a - b = 7
a * b = 30
a / b = 3
a % b = 1
```

**Instructor Note:** The integer division result (10/3 = 3) is the key teaching moment here. Ask students: "Why isn't this 3.333?" If a student asks how to get the decimal, show them that changing `int` to `float` and using `%f` gets there — but save the full explanation for when it comes up naturally in the exercises.

The `%%` in printf trips some students up — remind them `%` is special in printf (it starts a format specifier), so `%%` is how you print a literal percent sign.

---

## Part 4 — User Input

Complete `greeting.c`:

```c
#include <stdio.h>

int main() {
    char name[50];

    printf("Enter your name: ");
    scanf("%49s", name);
    printf("Hello, %s! Welcome to C programming.\n", name);

    return 0;
}
```

**Expected behavior:** Prompts for name, prints greeting.

**Instructor Note:** Students will discover the space limitation of `scanf` with `%s` on their own when someone types a two-word name. That's fine — it's a natural teachable moment about how C handles strings differently from languages they may have seen before. Don't preemptively explain it; let them hit it.

The `%49s` limit is there to prevent buffer overflow. If a student asks why 49 instead of 50, explain that C strings need one extra byte for the null terminator `\0`. This connects to Jared's teaching session content about strings being "just bytes ending with a zero."

---

## Part 5 — Data Types and sizeof

Complete `types.c`:

```c
#include <stdio.h>

int main() {
    int myInt = 42;
    float myFloat = 3.14f;
    char myChar = 'A';
    double myDouble = 2.718281828;

    // Print values
    printf("int: %d\n", myInt);
    printf("float: %f\n", myFloat);
    printf("char: %c (ASCII value: %d)\n", myChar, myChar);
    printf("double: %lf\n", myDouble);

    // Print sizes
    printf("\nSize of int: %zu bytes\n", sizeof(int));
    printf("Size of float: %zu bytes\n", sizeof(float));
    printf("Size of char: %zu bytes\n", sizeof(char));
    printf("Size of double: %zu bytes\n", sizeof(double));

    return 0;
}
```

**Expected Output:**

```
int: 42
float: 3.140000
char: A (ASCII value: 65)
double: 2.718282

Size of int: 4 bytes
Size of float: 4 bytes
Size of char: 1 bytes
Size of double: 8 bytes
```

**Instructor Note:** The two big takeaways here: (1) `char` prints as a letter with `%c` but as a number with `%d` — characters are just numbers, and (2) different types take different amounts of memory. Connect this back to Jared's teaching on memory and data representation. If a student asks why `float` shows 3.140000 instead of 3.14, explain that `%f` defaults to 6 decimal places. You can use `%.2f` for 2 decimal places, but don't belabor it.

---

## Bonus — Peek Under the Hood

This section is self-guided for fast finishers. The four gcc pipeline steps are:

| Step | Flag | Input | Output | What It Does |
|---|---|---|---|---|
| Preprocessor | `-E` | hello.c | hello.i | Expands `#include` directives |
| Compiler | `-S` | hello.c | hello.s | Translates to assembly language |
| Assembler | `-c` | hello.c | hello.o | Converts to binary object file |
| Linker | (none) | hello.o | hello.exe | Links with libraries to make executable |

**Instructor Note:** Most students won't get here during the walkthrough time. That's fine — this is stretch material. For students who do get here, the `hello.i` file is the most eye-opening — they'll see that their 6-line program expands to thousands of lines. The assembly (`hello.s`) is interesting but don't expect them to understand it. The point is just awareness that compilation isn't magic — it's a pipeline.

---

## Troubleshooting Quick Reference

| Problem | Solution |
|---|---|
| `gcc: command not found` | Close and reopen MinGW64 shell. If still failing, re-run the pacman install command. |
| Compilation errors | Read the error message — it tells you the line number. Open with `nano filename.c` and check that line. |
| `undefined reference to WinMain` | Student probably forgot `int main()` or has a typo in the function name. |
| nano not saving | Make sure they hit Ctrl+O then Enter, not just Ctrl+X. |
| Student saved as .txt | Rename in the shell: `mv filename.txt filename.c` |

---

## Pacing Guide

| Section | Expected Time |
|---|---|
| Part 1 (Install GCC) | 5–10 min |
| Part 2 (Hello World) | 10–15 min |
| Part 3 (Basic Math) | 10–15 min |
| Part 4 (User Input) | 10 min |
| Part 5 (Types/sizeof) | 10 min |
| Bonus | Remaining time |

Total: ~45–60 minutes for most students.
