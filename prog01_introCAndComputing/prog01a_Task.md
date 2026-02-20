# prog01 Session A — Syntax, Compilation, and Number Systems

**Estimated Time: 2 hours**
**Standards: ODE 5.1.7, 5.2.1, 2.3.1, 2.3.2**

---

## Exercise 1: Syntax and Compilation (~45 minutes)

In this exercise, you will translate code from a language you already know into C. Each snippet is shown in **both JavaScript and Python** — use whichever one makes more sense to you.

For each snippet:
1. Read the JS or Python version
2. Write the equivalent C code in the provided template
3. Compile it with `gcc` in the MinGW64 shell
4. Run the program and verify the output

Remember: In C, you need `#include` statements, a `main()` function, typed variables, and semicolons at the end of statements!

---

### Task 1.1: Variable Declaration and Printing

**JavaScript:**
```javascript
var x = 10;
console.log(x);
```

**Python:**
```python
x = 10
print(x)
```

**Your C Code:**
```c
#include <stdio.h>

int main() {
    // YOUR CODE HERE
    // Declare an integer variable x with value 10
    // Print it to the console

    return 0;
}
```

---

### Task 1.2: If/Else Statement

**JavaScript:**
```javascript
var age = 16;
if (age >= 18) {
    console.log("You are an adult");
} else {
    console.log("You are a minor");
}
```

**Python:**
```python
age = 16
if age >= 18:
    print("You are an adult")
else:
    print("You are a minor")
```

**Your C Code:**
```c
#include <stdio.h>

int main() {
    int age = 16;

    // YOUR CODE HERE
    // Use an if/else statement to print the appropriate message

    return 0;
}
```

---

### Task 1.3: For Loop

**JavaScript:**
```javascript
for (var i = 1; i <= 10; i++) {
    console.log(i);
}
```

**Python:**
```python
for i in range(1, 11):
    print(i)
```

**Your C Code:**
```c
#include <stdio.h>

int main() {
    // YOUR CODE HERE
    // Use a for loop to print the numbers 1 through 10

    return 0;
}
```

---

### Task 1.4: Function Definition and Return

**JavaScript:**
```javascript
function max(a, b) {
    if (a > b) {
        return a;
    } else {
        return b;
    }
}

var result = max(7, 3);
console.log(result);
```

**Python:**
```python
def max(a, b):
    if a > b:
        return a
    else:
        return b

result = max(7, 3)
print(result)
```

**Your C Code:**
```c
#include <stdio.h>

// YOUR CODE HERE
// Write a function called max that takes two integers (a and b)
// and returns the larger one

int main() {
    // YOUR CODE HERE
    // Call the max function with 7 and 3, store the result, and print it

    return 0;
}
```

---

## Exercise 2: Encoding and Number Systems (~45 minutes)

In this exercise, you will work with character encoding, ASCII values, and different number bases. These concepts are fundamental to understanding how computers represent data.

---

### Task 2.1: ASCII Values

Write a program that takes a string and prints each character along with its ASCII value.

**Example Output:**
```
Character: H  ASCII: 72
Character: i  ASCII: 105
Character: !  ASCII: 33
```

**Your C Code:**
```c
#include <stdio.h>
#include <string.h>

int main() {
    // YOUR CODE HERE
    // Declare a string with the value "Hi!"
    // Use a loop to iterate through each character
    // For each character, print the character and its ASCII value using %d
    // Hint: a char can be printed as both a character (%c) and a number (%d)

    return 0;
}
```

---

### Task 2.2: ASCII Arithmetic

The distance between uppercase and lowercase letters in ASCII is 32. For example:
- 'A' has ASCII value 65
- 'a' has ASCII value 97
- Difference: 97 - 65 = 32

Write a function that converts a lowercase letter to uppercase using this arithmetic rule.

**Your C Code:**
```c
#include <stdio.h>

// YOUR CODE HERE
// Write a function called toLower (that takes one char parameter)
// and returns the lowercase version using arithmetic
// Hint: subtract 32 from the uppercase char to get lowercase

char toLower(char c) {
    // YOUR CODE HERE
}

int main() {
    // YOUR CODE HERE
    // Test your function with several uppercase letters
    // Print the original character and the converted character
    // Example: 'A' becomes 'a'

    return 0;
}
```

---

### Task 2.3: Binary Representation

Write a program that converts a decimal number to binary by repeatedly dividing by 2 and collecting remainders.

**Example:**
- Input: 13
- Process: 13/2=6r1, 6/2=3r0, 3/2=1r1, 1/2=0r1
- Output: 1101 (reading remainders bottom-to-top)

**Your C Code:**
```c
#include <stdio.h>

int main() {
    int num = 13;
    // YOUR CODE HERE
    // Create a loop that divides num by 2
    // Store each remainder in an array
    // After the loop, print the remainders in reverse order (bottom-to-top)
    // This gives you the binary representation

    return 0;
}
```

---

### Task 2.4: Integer Overflow

Integer overflow occurs when a variable exceeds its maximum value. For an `unsigned char`, the max is 255. When you add 1 to 255, it wraps around to 0.

**Your C Code:**
```c
#include <stdio.h>

int main() {
    unsigned char x = 250;

    // YOUR CODE HERE
    // Use a loop to add 1 to x six times
    // After each addition, print the current value of x
    // Observe what happens when x exceeds 255
    // Expected output:
    // 251
    // 252
    // 253
    // 254
    // 255
    // 0 (overflow!)

    return 0;
}
```

---

## Compilation Instructions

In the MinGW64 shell, compile and run like this:

```
gcc myprogram.c -o myprogram.exe
./myprogram.exe
```

If you get errors, read them — they tell you the line number. Open the file with `nano myprogram.c` and fix it.

---

## Submission Checklist

For each task, ensure:
- [ ] Code compiles without errors
- [ ] Program runs without crashing
- [ ] Output matches expected behavior
- [ ] Code has comments explaining key lines
- [ ] Variable names use camelCase

