# prog01 DIY Task Solutions — INSTRUCTOR ONLY

## IMPORTANT: DO NOT DISTRIBUTE TO STUDENTS

This document contains the complete solution code and detailed instructor notes. Share only the task assignment (`prog01_DIYTask.md`) with students.

---

## Complete Solution Code

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
    my_int = 42;
    my_float = 3.14f;
    my_char = 'A';
    my_double = 2.71828;


    // PART 3: Print addresses and sizes of stack variables
    printf("=== STACK MEMORY ===\n");
    printf("int:    Address = %p,  Size = %lu bytes\n", (void*)&my_int, sizeof(int));
    printf("float:  Address = %p,  Size = %lu bytes\n", (void*)&my_float, sizeof(float));
    printf("char:   Address = %p,  Size = %lu bytes\n", (void*)&my_char, sizeof(char));
    printf("double: Address = %p,  Size = %lu bytes\n", (void*)&my_double, sizeof(double));

    printf("\nObservation: Stack addresses are typically CLOSE TOGETHER (within a few bytes).\n\n");


    // PART 4: Allocate an array on the heap
    printf("=== HEAP MEMORY ===\n");
    int* arr = NULL;  // Pointer to array

    arr = (int*)malloc(5 * sizeof(int));


    // PART 5: Check if malloc succeeded
    if (arr == NULL) {
        printf("Error: malloc failed!\n");
        return 1;
    }

    printf("Heap array allocated at address: %p\n", (void*)arr);
    printf("Size of allocated memory: %lu bytes\n\n", 5 * sizeof(int));


    // PART 6: Fill the heap array with values
    arr[0] = 10;
    arr[1] = 20;
    arr[2] = 30;
    arr[3] = 40;
    arr[4] = 50;


    // PART 7: Print all array values
    printf("=== ARRAY VALUES ===\n");
    for (int i = 0; i < 5; i++) {
        printf("arr[%d] = %d\n", i, arr[i]);
    }

    printf("\n");


    // BONUS: Print addresses of each array element
    printf("=== BONUS: ARRAY ELEMENT ADDRESSES ===\n");
    for (int i = 0; i < 5; i++) {
        printf("arr[%d] at address %p\n", i, (void*)&arr[i]);
    }

    printf("\n");


    // PART 8: Free the allocated memory
    free(arr);

    printf("Memory freed. Program complete!\n");

    return 0;
}
```

---

## Expected Output

A typical run will produce something like:

```
=== STACK MEMORY ===
int:    Address = 0x7ffe5fbff8ac,  Size = 4 bytes
float:  Address = 0x7ffe5fbff8a8,  Size = 4 bytes
char:   Address = 0x7ffe5fbff8a4,  Size = 1 byte
double: Address = 0x7ffe5fbff890,  Size = 8 bytes

Observation: Stack addresses are typically CLOSE TOGETHER (within a few bytes).

=== HEAP MEMORY ===
Heap array allocated at address: 0x55e7ac0c5260
Size of allocated memory: 20 bytes

=== ARRAY VALUES ===
arr[0] = 10
arr[1] = 20
arr[2] = 30
arr[3] = 40
arr[4] = 50

=== BONUS: ARRAY ELEMENT ADDRESSES ===
arr[0] at address 0x55e7ac0c5260
arr[1] at address 0x55e7ac0c5264
arr[2] at address 0x55e7ac0c5268
arr[3] at address 0x55e7ac0c526c
arr[4] at address 0x55e7ac0c5270

Memory freed. Program complete!
```

---

## Instructor Notes

### Key Teaching Points

1. **Stack vs. Heap Addresses**
   - Stack addresses (like `0x7ffe...`) are typically in a high memory range on modern systems
   - Heap addresses (like `0x55e7...`) are typically much lower
   - The difference is often several billion bytes
   - This demonstrates that these are truly different memory regions

2. **Stack Variable Spacing**
   - Variables declared on the stack are close together
   - In the example above, they span from `0x7ffe5fbff890` to `0x7ffe5fbff8ac`—a range of about 28 bytes
   - Variables are stored in reverse order of declaration (grows downward on most systems)

3. **Data Type Sizes**
   - `int`: 4 bytes (on 32-bit and 64-bit systems)
   - `float`: 4 bytes
   - `char`: 1 byte
   - `double`: 8 bytes
   - `sizeof()` is a compile-time operator—it tells us the size without running code

4. **Array Contiguity** (Bonus Section)
   - Array elements are stored consecutively in memory
   - For an `int` array, each element is 4 bytes apart
   - `arr[0]` at `0x55e7ac0c5260`
   - `arr[1]` at `0x55e7ac0c5264` (difference: 4 bytes)
   - `arr[2]` at `0x55e7ac0c5268` (difference: 4 bytes)
   - This is why array indexing is just pointer arithmetic: `arr[i]` == `*(arr + i)`

5. **Dynamic Memory Management**
   - `malloc()` requests memory from the heap at runtime
   - The OS decides where to place it
   - Always check if `malloc()` returns NULL (allocation failure)
   - Always `free()` memory when done to prevent memory leaks
   - The heap can fragment if memory is repeatedly allocated and freed

### Common Student Mistakes to Watch For

1. **Forgetting the cast to `(void*)`**
   - `printf("%p", &my_int)` may work but is technically incorrect
   - Using `printf("%p", (void*)&my_int)` is the proper way

2. **Not assigning values before printing**
   - Variables declared but not initialized have garbage values
   - Encourage initializing all variables

3. **Forgetting to `free()` memory**
   - This is a major source of memory leaks in C programs
   - Emphasize: allocate with `malloc()` → use → `free()`

4. **Using `sizeof()` on a pointer instead of the type**
   - `sizeof(arr)` where `arr` is a pointer will give 8 (on 64-bit systems)
   - Should use `sizeof(int)` or `5 * sizeof(int)`

5. **Arithmetic on void pointers**
   - Some compilers may give warnings about `void*` arithmetic
   - Encourage casting to `(char*)` or `(int*)` if needed for pointer math

### Assessment Criteria

Full credit should require:
- [ ] All four stack variables declared and initialized
- [ ] `printf()` calls use correct format specifiers (`%p`, `%lu`)
- [ ] `malloc()` correctly allocates 5 integers
- [ ] NULL check after `malloc()` is present
- [ ] Array is populated with values
- [ ] Array values are printed in a loop
- [ ] `free()` is called at the end
- [ ] Code compiles without errors or warnings
- [ ] Code runs and produces sensible output
- [ ] (Bonus) Array element addresses are printed and show 4-byte spacing

### Discussion Questions for Students

After completing this task, ask students:

1. "Why are the stack and heap addresses so different?"
   - Answer: They are different regions of memory managed by the OS. Stack grows downward, heap grows upward.

2. "What happens if you don't `free()` the memory?"
   - Answer: It remains allocated until the program exits (memory leak).

3. "Why can't we just declare `int arr[5]` instead of using `malloc()`?"
   - Answer: Stack allocation size must be known at compile time. `malloc()` allows runtime size.

4. "What does `sizeof()` do at compile time vs. runtime?"
   - Answer: `sizeof()` is evaluated at compile time. Addresses are known only at runtime.

5. "Why is array contiguity important?"
   - Answer: It allows fast sequential access and enables pointer arithmetic.

### Extension Activities

- Have students modify the program to allocate a 2D array (array of pointers to arrays)
- Ask them to implement a simple memory tracker that logs allocations/deallocations
- Have them investigate `calloc()` (allocates and initializes to zero)
- Explore `realloc()` to resize allocated memory blocks
