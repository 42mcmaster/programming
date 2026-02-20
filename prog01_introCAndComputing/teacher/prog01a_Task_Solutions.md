# prog01 Session A — Syntax, Compilation, and Number Systems

**INSTRUCTOR SOLUTIONS — DO NOT DISTRIBUTE TO STUDENTS**

**Standards: ODE 5.1.7, 5.2.1, 2.3.1, 2.3.2**

---

## Exercise 1: Syntax and Compilation

### Task 1.1: Variable Declaration and Printing

**Solution:**
```c
#include <stdio.h>

int main() {
    // Declare an integer variable x with value 10
    int x = 10;

    // Print the variable to the console using printf
    printf("%d\n", x);

    return 0;
}
```

**Expected Output:**
```
10
```

**Instructor Note:**
Students often forget `printf()` function or try to use `cout` (C++). Emphasize that C uses `printf()` with format specifiers like `%d` for integers. The `\n` adds a newline. This is a good time to introduce format specifiers which will be used throughout the course.

---

### Task 1.2: If/Else Statement

**Solution:**
```c
#include <stdio.h>

int main() {
    int age = 16;

    // Use an if/else statement to check age
    if (age >= 18) {
        printf("You are an adult\n");
    } else {
        printf("You are a minor\n");
    }

    return 0;
}
```

**Expected Output:**
```
You are a minor
```

**Instructor Note:**
Common mistakes:
- Using `=` instead of `==` in the condition (this assigns rather than compares)
- Forgetting braces `{}` around multi-statement blocks (though optional for single statements)
- Using `else if` when only two branches are needed

Point out the similarity between JavaScript's `if (age >= 18)` and C's syntax—they are nearly identical. This builds confidence that languages share common patterns.

---

### Task 1.3: For Loop

**Solution:**
```c
#include <stdio.h>

int main() {
    // Use a for loop to print numbers 1 through 10
    for (int i = 1; i <= 10; i++) {
        printf("%d\n", i);
    }

    return 0;
}
```

**Expected Output:**
```
1
2
3
4
5
6
7
8
9
10
```

**Instructor Note:**
The syntax is identical to JavaScript. Students may forget:
- The loop counter increment (`i++`)
- Parentheses around the loop conditions
- The comparison operator (`<=` vs `<`)

This is a perfect time to explain loop anatomy: initialization, condition, increment. Have students experiment with different loop conditions to see the effect.

---

### Task 1.4: Function Definition and Return

**Solution:**
```c
#include <stdio.h>

// Function to return the larger of two integers
int max(int a, int b) {
    if (a > b) {
        return a;
    } else {
        return b;
    }
}

int main() {
    // Call the max function with 7 and 3
    int result = max(7, 3);

    // Print the result
    printf("%d\n", result);

    return 0;
}
```

**Expected Output:**
```
7
```

**Instructor Note:**
Key teaching points:
- In C, the return type (`int`) must be specified BEFORE the function name
- Functions must be defined before `main()` OR you must use a function prototype
- The function can use a ternary operator as an alternative: `return (a > b) ? a : b;`

Common mistakes:
- Forgetting the return type
- Placing the function definition AFTER `main()` without a forward declaration
- Not storing the return value in a variable

---

## Exercise 2: Encoding and Number Systems

### Task 2.1: ASCII Values

**Solution:**
```c
#include <stdio.h>
#include <string.h>

int main() {
    // Declare a string with the value "Hi!"
    char str[] = "Hi!";

    // Use a loop to iterate through each character
    // strlen() gives us the length of the string
    for (int i = 0; i < strlen(str); i++) {
        // Print the character (%c) and its ASCII value (%d)
        printf("Character: %c  ASCII: %d\n", str[i], (int)str[i]);
    }

    return 0;
}
```

**Expected Output:**
```
Character: H  ASCII: 72
Character: i  ASCII: 105
Character: !  ASCII: 33
```

**Instructor Note:**
Teaching points:
- A string in C is an array of characters
- `strlen()` requires `#include <string.h>`
- A char can be cast to int using `(int)` to see its ASCII value
- The loop iterates from 0 to strlen(str)-1

Alternative approach without strlen():
```c
for (int i = 0; str[i] != '\0'; i++) {
    printf("Character: %c  ASCII: %d\n", str[i], (int)str[i]);
}
```

This teaches students that strings in C are terminated by a null character `\0`.

---

### Task 2.2: ASCII Arithmetic

**Solution:**
```c
#include <stdio.h>

// Function to convert uppercase to lowercase using arithmetic
char toLower(char c) {
    // Add 32 to the uppercase char to get lowercase
    // This works because 'a' - 'A' = 32 in ASCII
    return c + 32;
}

int main() {
    // Test the function with several uppercase letters
    char testChars[] = "HELLO";

    for (int i = 0; testChars[i] != '\0'; i++) {
        char original = testChars[i];
        char converted = toLower(original);
        printf("%c becomes %c\n", original, converted);
    }

    return 0;
}
```

**Expected Output:**
```
H becomes h
E becomes e
L becomes l
L becomes l
O becomes o
```

**Instructor Note:**
Important concept to emphasize:
- ASCII is a standard that assigns numbers to characters
- Uppercase letters (A-Z) have values 65-90
- Lowercase letters (a-z) have values 97-122
- The difference is always 32

This is an elegant example of how understanding encoding allows us to manipulate characters with simple arithmetic. Some students may want to check if a character is uppercase first using `isupper()` from `<ctype.h>`, which is a good extension.

---

### Task 2.3: Binary Representation

**Solution:**
```c
#include <stdio.h>

int main() {
    int num = 13;
    int binary[32];  // Array to store binary digits
    int index = 0;

    // Keep dividing by 2 and store remainders
    int tempNum = num;
    while (tempNum > 0) {
        binary[index] = tempNum % 2;  // Get remainder (0 or 1)
        tempNum = tempNum / 2;         // Divide by 2
        index++;
    }

    // Print the binary representation in reverse order
    printf("Decimal: %d\n", num);
    printf("Binary: ");
    for (int i = index - 1; i >= 0; i--) {
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
This is a conceptually challenging exercise. Walk through the algorithm step-by-step:
1. 13 % 2 = 1, 13 / 2 = 6
2. 6 % 2 = 0, 6 / 2 = 3
3. 3 % 2 = 1, 3 / 2 = 1
4. 1 % 2 = 1, 1 / 2 = 0 (stop)

Reading the remainders bottom-to-top: 1101 (which equals 13 in decimal)

Advanced discussion: Introduce bitwise operators as an alternative way to extract binary digits:
```c
for (int i = 31; i >= 0; i--) {
    printf("%d", (num >> i) & 1);
}
```

---

### Task 2.4: Integer Overflow

**Solution:**
```c
#include <stdio.h>

int main() {
    unsigned char x = 250;

    // Use a loop to add 1 to x six times and observe overflow
    for (int i = 0; i < 6; i++) {
        printf("%d\n", x);
        x++;  // Add 1 to x
    }

    return 0;
}
```

**Expected Output:**
```
250
251
252
253
254
255
0
```

**Instructor Note:**
This demonstrates a critical concept in computer science: integer overflow. Key points:
- `unsigned char` can hold values 0-255 (8 bits)
- When x reaches 255 and you add 1, it wraps around to 0
- This is defined behavior in C for unsigned types
- With signed integers, overflow is undefined behavior (dangerous!)

Discuss real-world implications:
- Y2K bug (2-digit years overflowed from 99 to 00)
- Security vulnerabilities in buffer overflows
- The importance of choosing the right data type

Have students experiment with what happens if they use `signed char` instead—the behavior is less predictable and depends on the system.

---

## Common Student Mistakes and Teaching Tips

**Mistake 1: Missing `#include` statements**
- Students write code without the necessary headers
- Solution: Start every program template with the required includes

**Mistake 2: Confusing `=` with `==`**
- Using `if (x = 5)` instead of `if (x == 5)`
- Solution: Have students verbalize: "single = is assignment, double == is comparison"

**Mistake 3: Forgetting format specifiers in printf()**
- Writing `printf(x)` instead of `printf("%d\n", x)`
- Solution: Create a cheat sheet of common format specifiers: `%d` (int), `%f` (float), `%c` (char), `%s` (string)

**Mistake 4: Off-by-one errors in loops**
- Using `i < 10` when they meant `i <= 10`
- Solution: Have students trace through loops manually with concrete examples

**Mistake 5: Not understanding array indexing**
- Trying to access string[10] when the string only has 10 characters (indices 0-9)
- Solution: Always emphasize that C indexing is 0-based

---

## Time Allocation Guide

- Task 1.1: 8-10 minutes
- Task 1.2: 8-10 minutes
- Task 1.3: 10-12 minutes
- Task 1.4: 12-15 minutes
- Task 2.1: 10-12 minutes
- Task 2.2: 8-10 minutes
- Task 2.3: 15-18 minutes (may require step-by-step guidance)
- Task 2.4: 8-10 minutes

Total: approximately 80-107 minutes (allows for discussion and troubleshooting)

