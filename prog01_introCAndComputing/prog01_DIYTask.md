# prog01 DIY Task — Memory Explorer

## Overview

This is a hands-on challenge task designed for students who finish the main lessons early or who want to explore memory management in C at a deeper level. You will write a program that interacts directly with the computer's memory, observing how C allocates space on the **stack** and the **heap**.

## Learning Objectives

By completing this task, you will:
- Understand how different data types use memory
- See the actual memory addresses where your variables are stored
- Learn the difference between stack and heap allocation
- Practice using `malloc()` and `free()` for dynamic memory
- Understand array layout in memory

## The Task

Write a C program named `memory_explorer.c` that demonstrates memory allocation and addresses.

### Requirements

Your program must:

1. **Declare stack variables** of different types:
   - One `int`
   - One `float`
   - One `char`
   - One `double`

2. **Print the memory address** of each variable using `printf` with the `%p` format specifier

3. **Print the size in bytes** of each variable using the `sizeof` operator

4. **Allocate a heap array** of 5 integers using `malloc()`

5. **Print the heap array's address** and compare it visually to the stack addresses (they should be very different!)

6. **Populate the array** with some sample values (e.g., 10, 20, 30, 40, 50)

7. **Print all array values** to verify they were stored correctly

8. **Free the allocated memory** using `free()`

9. **BONUS (optional):** Print the address of each array element and show that they are contiguous in memory (each element is typically 4 bytes apart for an int array)

### Starter Code

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    // PART 1: Declare stack variables of different types
    int my_int;           // Stack: integer
    float my_float;       // Stack: floating-point
    char my_char;         // Stack: single character
    double my_double;     // Stack: double-precision float

    // PART 2: Assign values to the stack variables
    // YOUR CODE HERE: Assign a value to my_int (try 42)

    // YOUR CODE HERE: Assign a value to my_float (try 3.14)

    // YOUR CODE HERE: Assign a value to my_char (try 'A')

    // YOUR CODE HERE: Assign a value to my_double (try 2.71828)


    // PART 3: Print addresses and sizes of stack variables
    printf("=== STACK MEMORY ===\n");
    printf("int:    Address = %p,  Size = %lu bytes\n", // YOUR CODE HERE: Add (void*)&my_int
    printf("float:  Address = %p,  Size = %lu bytes\n", // YOUR CODE HERE: Add (void*)&my_float
    printf("char:   Address = %p,  Size = %lu bytes\n", // YOUR CODE HERE: Add (void*)&my_char
    printf("double: Address = %p,  Size = %lu bytes\n", // YOUR CODE HERE: Add (void*)&my_double

    printf("\nObservation: Stack addresses are typically CLOSE TOGETHER (within a few bytes).\n\n");


    // PART 4: Allocate an array on the heap
    printf("=== HEAP MEMORY ===\n");
    int* arr = NULL;  // Pointer to array

    // YOUR CODE HERE: Use malloc to allocate space for 5 integers
    // Hint: arr = (int*)malloc(5 * sizeof(int));


    // PART 5: Check if malloc succeeded
    if (arr == NULL) {
        printf("Error: malloc failed!\n");
        return 1;
    }

    printf("Heap array allocated at address: %p\n", (void*)arr);
    printf("Size of allocated memory: %lu bytes\n\n", 5 * sizeof(int));


    // PART 6: Fill the heap array with values
    // YOUR CODE HERE: Set arr[0] = 10
    // YOUR CODE HERE: Set arr[1] = 20
    // YOUR CODE HERE: Set arr[2] = 30
    // YOUR CODE HERE: Set arr[3] = 40
    // YOUR CODE HERE: Set arr[4] = 50


    // PART 7: Print all array values
    printf("=== ARRAY VALUES ===\n");
    for (int i = 0; i < 5; i++) {
        printf("arr[%d] = %d\n", i, arr[i]);
    }

    printf("\n");


    // BONUS: Print addresses of each array element
    printf("=== BONUS: ARRAY ELEMENT ADDRESSES ===\n");
    // YOUR CODE HERE: Uncomment and complete the loop below
    // for (int i = 0; i < 5; i++) {
    //     printf("arr[%d] at address %p\n", i, (void*)&arr[i]);
    // }

    // Observation: Notice that each address differs by 4 bytes
    // (because each int is 4 bytes on most systems)

    printf("\n");


    // PART 8: Free the allocated memory
    // YOUR CODE HERE: Call free(arr) to release the heap memory

    printf("Memory freed. Program complete!\n");

    return 0;
}
```

## What to Observe

When you run this program, notice:

1. **Stack addresses** are relatively close to each other (printed in hex with `%p`)
2. **Heap address** is typically much higher than stack addresses
3. **Size of each type**: `int` and `float` are usually 4 bytes, `double` is usually 8 bytes, `char` is usually 1 byte
4. **Array elements** (BONUS) are contiguous—each element address is 4 bytes higher than the previous (for int arrays)

## Compilation and Testing

Compile with:
```bash
gcc -o memory_explorer memory_explorer.c
```

Run with:
```bash
./memory_explorer
```

## Stretch Ideas

If you finish early and want to push further:

- Modify the program to allocate an array of `double` values and compare the spacing (should be 8 bytes apart)
- Use a loop to allocate and print multiple smaller arrays, observing how they are positioned in heap memory
- Investigate `calloc()` as an alternative to `malloc()`
- Write code to print the stack and heap addresses relative to each other (calculate the difference)

## Submission

Save your completed file as `memory_explorer.c` and test it thoroughly before submitting.
