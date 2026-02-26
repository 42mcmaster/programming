# prog01 DIY Challenge — Memory Explorer

**Programming — Medina County Career Center**

---

## What Is This?

This is an optional challenge for students who finish the main task files and want to go deeper. You'll write a program that peeks under the hood at how C stores data in memory — seeing actual memory addresses and understanding the difference between the stack and the heap.

---

## What You'll Learn

- How different data types use different amounts of memory
- What memory addresses look like and how to print them
- The difference between stack memory (automatic) and heap memory (manual)
- How to use `malloc()` and `free()` for dynamic memory allocation
- How arrays are laid out in memory (spoiler: everything is in a row)

---

## Part 1: Walkthrough — Seeing Memory (Copy-Paste)

**Copy and paste** this program into a file called `memory_peek.c`:

```c
#include <stdio.h>

int main() {
    int age = 17;
    float gpa = 3.5;
    char letter = 'A';

    printf("=== Where do variables live? ===\n\n");

    printf("age    = %d\n", age);
    printf("  Address: %p\n", (void*)&age);
    printf("  Size:    %zu bytes\n\n", sizeof(age));

    printf("gpa    = %.1f\n", gpa);
    printf("  Address: %p\n", (void*)&gpa);
    printf("  Size:    %zu bytes\n\n", sizeof(gpa));

    printf("letter = '%c'\n", letter);
    printf("  Address: %p\n", (void*)&letter);
    printf("  Size:    %zu byte\n\n", sizeof(letter));

    printf("Notice: all three addresses are close together.\n");
    printf("That's because they all live on the STACK.\n");

    return 0;
}
```

Compile and run it:
```
gcc memory_peek.c -o memory_peek.exe
./memory_peek.exe
```

**Question:** How many bytes does an `int` use? A `float`? A `char`?

```
YOUR ANSWER:


```

**What to notice:**
- `&age` gives you the **address** of the variable (where it lives in memory)
- `(void*)` is a cast needed for `%p` to work properly
- `sizeof()` tells you how many bytes a variable uses
- All three addresses should look similar — they're all on the **stack**

---

## Part 2: The Challenge

Now write your own program called `memory_explorer.c` that does the following:

### Step 1: Stack Variables

Declare one variable of each type and give them values:
- `int` (try 42)
- `float` (try 3.14)
- `char` (try 'X')
- `double` (try 2.71828)

For each one, print its value, its address (`%p`), and its size (`sizeof`).

### Step 2: Heap Allocation

Allocate an array of 5 integers on the **heap** using `malloc()`:

```c
#include <stdlib.h>  // You need this for malloc and free

int *arr = (int *)malloc(5 * sizeof(int));
```

After allocating:
- Check that `arr` is not `NULL` (malloc can fail if memory runs out)
- Print the address of the array
- Fill it with values: 10, 20, 30, 40, 50
- Print all the values using a loop
- **Free the memory** when you're done: `free(arr);`

### Step 3: Compare Stack vs Heap

Print the address of one of your stack variables and the heap array side by side. Notice how different they are — the stack and heap are in completely different regions of memory.

### Bonus: Array Element Addresses

Print the address of each element in your heap array:

```c
for (int i = 0; i < 5; i++) {
    printf("arr[%d] at address %p\n", i, (void*)&arr[i]);
}
```

You should see that each address is exactly 4 bytes apart (because each `int` is 4 bytes). This proves that arrays store elements **contiguously** in memory — one right after the other.

---

## Starter Code

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    // === STEP 1: Stack Variables ===
    // Declare and initialize: int, float, char, double
    // Print each one's value, address, and size

    // === STEP 2: Heap Allocation ===
    // Allocate an array of 5 ints with malloc
    // Check for NULL
    // Fill with values 10, 20, 30, 40, 50
    // Print all values
    // Free the memory

    // === STEP 3: Compare ===
    // Print a stack address and the heap address to compare

    // === BONUS: Element Addresses ===
    // Print the address of each array element

    return 0;
}
```

---

## What to Observe When You Run It

1. **Stack addresses** are close together (within a few bytes of each other)
2. **Heap address** is typically in a very different range than stack addresses
3. **Type sizes:** `char` = 1 byte, `int` = 4 bytes, `float` = 4 bytes, `double` = 8 bytes
4. **Array elements** (bonus) have addresses exactly 4 bytes apart for `int` arrays

---

## Compilation

```
gcc memory_explorer.c -o memory_explorer.exe
./memory_explorer.exe
```

---

## Stretch Ideas

If you finish and want to keep exploring:
- Allocate an array of `double` instead and see how the address spacing changes (should be 8 bytes apart)
- Try allocating multiple small arrays and see where they end up in heap memory
- Look up `calloc()` — it's like `malloc()` but it initializes everything to zero
- What happens if you try to use the array *after* calling `free()`? (Don't do this in production code, but it's interesting to see)

---

## Submission

Save your completed `memory_explorer.c` and make sure it compiles and runs without errors or warnings before submitting.
