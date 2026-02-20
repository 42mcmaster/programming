# Lesson 01: Introduction to C and Computing
## Study Guide


---

## QUICK REFERENCE: C SYNTAX

### Basic Program Structure
```c
#include <stdio.h>      // Include standard input/output library

int main() {            // Program entry point, returns int
    // Code goes here
    return 0;           // Return 0 to indicate successful execution
}
```

### Variable Declaration
```c
int age;                // Declare an integer
int count = 5;          // Declare and initialize an integer
float salary = 45000.50;  // Declare and initialize a float
char grade = 'A';       // Declare and initialize a char (single quotes)
unsigned char status;   // Unsigned char for values 0-255
```

### printf() - Output to Screen
```c
printf("Hello, World!\n");              // Print text

// Format specifiers:
printf("%d\n", 42);                     // %d for integers
printf("%f\n", 3.14);                   // %f for floats (default 6 decimals)
printf("%.2f\n", 3.14159);              // %.2f for 2 decimal places
printf("%c\n", 'A');                    // %c for single character
printf("%s\n", "Hello");                // %s for strings
printf("%p\n", &variable);              // %p for memory addresses (pointers)
printf("Age: %d, Name: %s\n", 25, "Bob");  // Multiple values
```

### scanf() - Input from User
```c
int age;
printf("Enter your age: ");
scanf("%d", &age);                      // %d for int, & gets address

float price;
scanf("%f", &price);                    // %f for float

char initial;
scanf("%c", &initial);                  // %c for char

char name[50];
scanf("%s", name);                      // %s for string (no & needed!)
```

### Basic Operators
```c
// Arithmetic
int sum = 10 + 5;       // Addition
int diff = 10 - 5;      // Subtraction
int product = 10 * 5;   // Multiplication
int quotient = 10 / 5;  // Division (integer division if both operands are int)
int remainder = 10 % 3; // Modulus (remainder)

// Comparison
a == b                  // Equal to
a != b                  // Not equal to
a > b                   // Greater than
a < b                   // Less than
a >= b                  // Greater than or equal to
a <= b                  // Less than or equal to

// Logical
a && b                  // AND (both must be true)
a || b                  // OR (either can be true)
!a                      // NOT (negation)
```

### Data Type Sizes (Typical Values)
```
char               1 byte      (-128 to 127, or 0 to 255 unsigned)
int                4 bytes     (-2,147,483,648 to 2,147,483,647)
float              4 bytes     (approximately -3.4e38 to 3.4e38)
unsigned char      1 byte      (0 to 255)
```

### Arrays
```c
int numbers[5];                 // Array of 5 integers
int scores[3] = {90, 85, 92};   // Array with initialization
char letters[4] = {'A', 'B', 'C', '\0'};  // Array of chars (mini-string)
```

### Compiling and Running
```bash
gcc program.c -o program        // Compile program.c, output to 'program'
./program                       // Run the executable (Linux/Mac)
program.exe                     // Run the executable (Windows)
gcc -Wall program.c -o program  // Compile with all warnings enabled
```

### Includes (Libraries)
```c
#include <stdio.h>              // Standard input/output (printf, scanf)
#include <stdlib.h>             // Standard library (malloc, free, rand, etc.)
#include <math.h>               // Math functions (sqrt, sin, cos, etc.)
#include <string.h>             // String functions (strcpy, strlen, etc.)
```

### Memory and Pointers
```c
int x = 10;
int *ptr = &x;                  // ptr holds the address of x
printf("%p\n", ptr);            // Print the address
printf("%d\n", *ptr);           // Dereference: print the value at that address

// Dynamic memory allocation
int *arr = (int *)malloc(5 * sizeof(int));  // Allocate 5 integers
free(arr);                      // Free the memory
arr = NULL;                     // Good practice: set to NULL after freeing
```

---

## VOCABULARY

**1. Compiler**
A program that translates source code from a high-level programming language into machine code (object code) that a computer can execute.

**2. Interpreter**
A program that reads and executes source code directly, line by line, without converting it to machine code first.

**3. Source Code**
Human-readable program text written in a programming language. This is what programmers write before compilation.

**4. Object Code**
Machine-readable binary code produced by a compiler. Object code must be linked with libraries to create an executable program.

**5. Binary**
A number system that uses only two digits: 0 and 1. This is the fundamental language of computers.

**6. Hexadecimal**
A number system that uses 16 digits (0-9 and A-F). Hexadecimal is often used to represent binary values more compactly in programming.

**7. ASCII**
American Standard Code for Information Interchange. A character encoding standard that assigns numbers (0-127) to letters, digits, and symbols so computers can store and display text.

**8. Byte**
A unit of computer memory consisting of 8 bits. One byte can store values from 0 to 255 (unsigned) or -128 to 127 (signed).

**9. Bit**
The smallest unit of information in computing. A bit is either 0 or 1.

**10. Data Type**
A classification that specifies what kind of values a variable can hold and how much memory it requires (examples: int, float, char).

**11. int**
A data type used to store whole numbers (integers). Typically requires 4 bytes and holds values from approximately -2.1 billion to 2.1 billion.

**12. float**
A data type used to store decimal numbers (floating-point values). Typically requires 4 bytes and has limited precision.

**13. char**
A data type used to store a single character. Requires 1 byte and stores values as ASCII codes (0-127 for standard ASCII).

**14. unsigned char**
A char data type that stores only non-negative values (0-255). Used when negative values are not needed to maximize the range of positive values.

**15. Pointer**
A variable that stores a memory address. Pointers allow indirect access to data and are fundamental to dynamic memory allocation.

**16. Memory Address**
A numerical identifier for a location in computer memory. Each byte in memory has a unique address.

**17. Stack**
A region of memory used for automatic storage of local variables and function call information. Memory on the stack is automatically freed when variables go out of scope.

**18. Heap**
A region of memory used for dynamic memory allocation. Memory on the heap persists until explicitly freed by the programmer.

**19. malloc**
A function that allocates a block of memory on the heap. Must be followed by proper memory management and eventual use of free().

**20. free**
A function that deallocates (releases) memory on the heap that was previously allocated with malloc(). Prevents memory leaks.

**21. Null Terminator**
The character '\0' (ASCII value 0) used to mark the end of a string in C. Every string must end with a null terminator.

**22. String (C)**
In C, a string is an array of char values terminated by a null terminator ('\0'). Strings are used to store and manipulate text.

**23. Array**
A collection of elements of the same data type stored in contiguous memory locations. Elements are accessed using an index (starting at 0).

**24. sizeof**
An operator that returns the number of bytes a data type or variable occupies in memory.

**25. Integer Division**
Division between two integers that discards the fractional part. Example: 7 / 2 = 3 (not 3.5).

**26. Overflow**
An error that occurs when a value exceeds the maximum range that a data type can store, causing incorrect results or wraparound behavior.

## ODE COMPETENCIES COVERED

**2.3.1 - ASCII Character Encoding**
- Understanding how characters are represented as numbers
- ASCII values for common characters
- Using char data type to store and manipulate characters

**2.3.2 - Binary, Hexadecimal, and Overflow**
- Converting between decimal, binary, and hexadecimal
- Understanding how numbers are stored in memory
- Detecting and managing integer overflow conditions

**5.1.7 - Compilers and Compilation**
- The compilation pipeline: preprocess → compile → assemble → link
- Using gcc to compile programs
- Understanding source code vs. object code vs. executable

**5.2.1 - Data Types**
- Selecting appropriate data types (int, float, char)
- Understanding memory requirements of each type
- Type conversion and casting

**5.2.3 - Arithmetic Operations**
- Basic arithmetic operators (+, -, *, /, %)
- Integer vs. floating-point division
- Order of operations in expressions

**5.3.8 - Nested Loops**
- Loop structures and control flow
- Nested loop patterns for multi-dimensional problems
- Loop counter management and boundary conditions

---

## KEY TAKEAWAYS

- C is a compiled language requiring compilation before execution
- Understanding data types and memory is fundamental to C programming
- The compilation pipeline transforms source code into executable machine code
- Character data is stored as ASCII numeric values
- Arrays and pointers enable working with multiple values and dynamic memory
- Every C program must have a main() function where execution begins
- Proper memory management (allocation and deallocation) is essential for avoiding leaks
