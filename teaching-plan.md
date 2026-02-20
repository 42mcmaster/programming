# Teaching Plan

Two weeks, two in-person visits. Goal: ramp kids up in C and low-level concepts in week 1,
then tackle the CS50 Filter image manipulation exercise in week 2.

---

## Week 1: Tuesday Teaching Session (Feb 24)

### Block 1 (~45 min): Context + How Computers Actually Work

- Jared's background and career path
- **Why C still matters:**
  - The lingua franca of computing — almost every language defines itself in relation to
    C. Rust, Go, Zig, Swift all explain how they're different from C. C is the baseline.
  - FFI and interop — when any two languages need to talk to each other, they almost
    always do it through C's calling conventions and data layout. The C ABI is the
    universal interface.
  - The world runs on C — Linux/Windows/macOS kernels, Postgres, SQLite, Nginx, CPython,
    the Ruby interpreter, V8 (your JS engine), compilers for almost every language you've
    used. All C or C/C++.
  - Performance — C compiles to machine code with minimal abstraction overhead. Game
    engines, embedded systems, operating systems, databases — when you need to go as fast
    as the hardware allows, C is still the tool.
  - But it's dangerous — no bounds checking, no garbage collector, no safety net. Buffer
    overflows, use-after-free, null pointer dereferences. This is why languages like Rust
    exist: same performance, but the compiler catches your memory mistakes.
  - Learning C teaches you what the computer is actually doing. Every other language hides
    things from you (for good reasons). C shows you the machine.
- Side-by-side: same program in JS and C — types, braces, `main()`, `#include`
- **Compilation vs interpretation** _(5.1.7)_: "JS has an engine that reads your code at
  runtime. In C, you turn your code into a binary the CPU runs directly — there's no
  middleman."
  - Live: write `hello.c`, compile with `gcc`, run it
  - Show the full pipeline at least once (preprocess → compile → assemble → link)
- **Binary and hex** _(2.3.2)_: Everything in the computer is bytes. Show the same number
  in decimal, binary, hex. "When you see `0xFF`, that's 255, that's the max value a single
  byte can hold." Use `objdump` to peek at the binary — "this is what your program
  actually looks like to the CPU."
- **ASCII** _(2.3.1)_: Characters are just numbers. `'A'` is 65. Show a small ASCII table.
  `printf("%d", 'A');` — demystify it.

### Block 2 (~60 min): C Fundamentals + The Machine Model

**1. Types and memory** _(5.2.1, 2.3.2)_ (~15 min)

- `int`, `float`, `char`, `unsigned char` / `BYTE` — each has a fixed size
- `sizeof` — show them the sizes
- Integer division: `5 / 2` is `2` _(5.2.3)_
- Overflow: what happens when you add 1 to 255 in an unsigned char _(2.3.2)_

**2. Pointers and memory layout** (~20 min)

- Memory is a giant numbered array of bytes. A pointer is an address.
- Stack vs heap: stack is automatic and scoped, heap is manual (`malloc`/`free`)
- "In JS, garbage collection cleans up for you. In C, you're the garbage collector."
- Demo: print addresses with `&`, show `sizeof` on pointers, maybe draw a diagram
- Arrays and pointers are the same thing — an array is a contiguous buffer of memory, and
  the array name is just a pointer to the first slot. This is why you always pass a size
  alongside an array in C (unlike JS, it doesn't know its own length), and why buffer
  overflows exist (nothing stops you from reading past the end)

**3. Strings: the low-level truth** _(2.3.1)_ (~10 min)

- "In JS, a string is a magic object. In C, it's just bytes ending with a zero."
- `char name[] = "hello";` — 6 bytes, null terminator
- Ties pointers, memory, types, and ASCII together in one example

**4. Functions** _(5.2.1, 5.2.3)_ (~15 min)

- Functions with typed signatures — return type, parameter types, void
- Write a few small functions together: average, clamp, etc.
- `scanf` for user input — brief intro so they can use it in exercises
- Build something together: ask user for a count, `malloc` an array of that size, read
  numbers in, compute the average, `free` it — ties the whole memory model together

### Competencies hit in Week 1 teaching

| Competency                  | Where                                                |
| --------------------------- | ---------------------------------------------------- |
| 2.3.1 (ASCII)               | ASCII demo, strings section, cipher exercise         |
| 2.3.2 (binary/hex/overflow) | Binary/hex intro, overflow demo, hex exercise        |
| 5.1.7 (compilers)           | Full gcc pipeline walkthrough                        |
| 5.2.1 (data types)          | Types section, sizeof, functions                     |
| 5.2.3 (arithmetic)          | Int division, averages, every exercise               |

---

## Week 1: Exercises (Wed–Fri, ~4 hours)

**Exercise 1: Syntax + compilation** (~45 min) _(5.1.7, 5.2.1)_

- Translate 3–4 small JS snippets to C
- Covers: typed variables, printf, if/else, for loops, basic functions
- Each one: write it, compile it, run it, fix the compiler errors _(5.4.6–5.4.7)_

**Exercise 2: Encoding and number systems** (~45 min) _(2.3.1, 2.3.2)_

- Print each character of a string along with its ASCII value
- Write a function that converts a single lowercase letter to uppercase using arithmetic
  (not a library function — they learn `'a' - 'A'` is 32)
- Write a program that prints a number in binary (loop and divide by 2)
- Explore integer overflow: start with `unsigned char x = 250;`, keep adding, print each
  step

**Exercise 3: Functions, types, and math** (~45 min) _(5.2.1, 5.2.3)_

- Temperature converter (int vs float division matters)
- `int clamp(int value, int min, int max)` — clamp a value to a range
- Weighted average function with three inputs and three weights
- Grade calculator from a numeric score

**Exercise 4: Arrays and loops** (~45 min) _(5.3.8)_

- 1D: find the max, compute average, reverse an array in place
- Nested loop emphasis throughout _(5.3.8)_

**Exercise 5: Strings + dynamic memory** (~45 min) _(2.3.1)_

- `int my_strlen(char *s)` — walk until `\0`
- Caesar cipher: shift each character by n _(2.3.1 — ASCII arithmetic in action)_
- Dynamic input exercise: use `scanf` to get a count from the user, `malloc` an array,
  read values in, compute stats (max, min, average), `free` it

**Stretch:** Use `&` and `sizeof` to print addresses and sizes of variables on the stack,
then malloc something and print its address — "see, it's a different region of memory"

---

## Week 2: Tuesday Teaching Session (Mar 3)

### Block 1 (~60 min): Structs + 2D Arrays _(5.2.1, 5.3.8)_

- Review week 1 — what clicked, what was hard
- **Structs** _(5.2.1)_: grouping related data into a custom type, dot notation access
  - Define a simple struct, make an array of them, write a function that operates on it
  - "Next hour you'll see a struct called `RGBTRIPLE` — same idea"
- **2D arrays** _(5.3.8)_: `int grid[rows][cols]`, nested loops
  - Walk through indexing, row-major layout
  - "An image is just a 2D array of pixels. Each pixel is a struct with three bytes."

### Block 2 (~60 min): Image Exercise Walkthrough _(5.2.3, 5.3.8, 5.4.6–5.4.7)_

- Walk through the scaffold: `bmp.h`, `helpers.h`, `filter.c` — "you only touch
  `helpers.c`"
- Code grayscale together — arithmetic, rounding, nested loops
- Start blur: 3x3 box, boundary handling
- Introduce edge detection (Sobel) conceptually for stretch kids
- **Debugging emphasis** _(5.4.6–5.4.7)_: printf-debugging pixel values, checking boundary
  cases, reading compiler errors

### Exercise: Filter Problem Set (Wed–Fri, ~4 hours) _(5.2.3, 5.3.8, 5.4.6–5.4.7)_

- Everyone: grayscale, reflect, blur
- Stretch: edge detection (Sobel operator)
