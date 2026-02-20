# prog01 Session B — Functions, Arrays, and Memory

**Estimated Time: 2 hours**
**Standards: ODE 5.2.1, 5.2.3, 5.3.8, 2.3.1**

---

## Exercise 3: Functions, Types, and Math (~45 minutes)

In this exercise, you will write functions that perform calculations. Pay close attention to data types—the difference between `int` and `float` will affect your results!

---

### Task 3.1: Temperature Conversion

Write a function that converts a temperature from Fahrenheit to Celsius. The formula is:
**C = (F - 32) * 5/9**

The key learning point: What happens if you use `int` instead of `float`?

**Your C Code:**
```c
#include <stdio.h>

// YOUR CODE HERE
// Write a function called fahrenheitToCelsius
// It should take one float parameter (fahrenheit)
// and return a float (celsius)
// Formula: celsius = (fahrenheit - 32) * 5/9
// Use 5.0 and 9.0 (with decimals) to ensure floating-point division

float fahrenheitToCelsius(float fahrenheit) {
    // YOUR CODE HERE
}

int main() {
    // YOUR CODE HERE
    // Test your function with these values:
    // 32 F (should be 0 C)
    // 212 F (should be 100 C)
    // 68 F (should be 20 C)
    // Print the results with printf using %.2f to show 2 decimal places

    return 0;
}
```

---

### Task 3.2: Clamp Function

Write a function called `clamp()` that constrains a value to be within a specific range.

If the value is less than the minimum, return the minimum.
If the value is greater than the maximum, return the maximum.
Otherwise, return the value unchanged.

**Example:**
- clamp(5, 0, 10) returns 5 (value is within range)
- clamp(-2, 0, 10) returns 0 (value is below range, return min)
- clamp(15, 0, 10) returns 10 (value is above range, return max)

**Your C Code:**
```c
#include <stdio.h>

// YOUR CODE HERE
// Write a function called clamp that takes three int parameters:
// - value: the number to clamp
// - minValue: the minimum allowed value
// - maxValue: the maximum allowed value
// Return the clamped value

int clamp(int value, int minValue, int maxValue) {
    // YOUR CODE HERE
}

int main() {
    // YOUR CODE HERE
    // Test your function with at least 6 cases:
    // - value within range
    // - value below minimum
    // - value above maximum
    // Repeat a couple times with different ranges
    // Print each test case and the result

    return 0;
}
```

---

### Task 3.3: Weighted Average

Write a function that calculates a weighted average of three scores. The weights represent how important each score is.

**Example:**
- Three scores: 80, 90, 70
- Three weights: 0.5, 0.3, 0.2 (must sum to 1.0)
- Weighted average = (80 * 0.5) + (90 * 0.3) + (70 * 0.2) = 40 + 27 + 14 = 81.0

**Your C Code:**
```c
#include <stdio.h>

// YOUR CODE HERE
// Write a function called weightedAverage that takes:
// - Three float parameters for scores (score1, score2, score3)
// - Three float parameters for weights (weight1, weight2, weight3)
// Return a float representing the weighted average

float weightedAverage(float score1, float score2, float score3,
                      float weight1, float weight2, float weight3) {
    // YOUR CODE HERE
    // Calculate: (score1 * weight1) + (score2 * weight2) + (score3 * weight3)
}

int main() {
    // YOUR CODE HERE
    // Test with this example:
    // Scores: 80, 90, 70
    // Weights: 0.5, 0.3, 0.2
    // Expected output: 81.00

    return 0;
}
```

---

### Task 3.4: Grade Calculator

Write a function that converts a numeric score (0-100) to a letter grade (A-F) using these rules:
- 90-100: A
- 80-89: B
- 70-79: C
- 60-69: D
- 0-59: F

**Your C Code:**
```c
#include <stdio.h>

// YOUR CODE HERE
// Write a function called getGrade that takes one int parameter (score)
// and returns a char representing the letter grade

char getGrade(int score) {
    // YOUR CODE HERE
    // Use if/else statements to determine the grade
    // Return 'A', 'B', 'C', 'D', or 'F'
}

int main() {
    // YOUR CODE HERE
    // Test your function with these scores:
    // 95 (should be A)
    // 85 (should be B)
    // 75 (should be C)
    // 65 (should be D)
    // 50 (should be F)
    // For each test, print the score and the corresponding grade

    return 0;
}
```

---

## Exercise 4: Arrays and Loops (~45 minutes)

In this exercise, you will work with arrays of numbers and practice nested loops.

---

### Task 4.1: Find Maximum in Array

Write a function that searches through an array of integers and returns the largest value.

**Your C Code:**
```c
#include <stdio.h>

// YOUR CODE HERE
// Write a function called findMax that takes:
// - An int array (called numbers)
// - The size of the array (int size)
// Return the maximum value in the array

int findMax(int numbers[], int size) {
    // YOUR CODE HERE
    // Start with the first element as maxValue
    // Loop through the remaining elements
    // If you find a larger value, update maxValue
    // Return maxValue
}

int main() {
    // YOUR CODE HERE
    // Create an array: {15, 3, 42, 8, 23, 1, 99}
    // Calculate the size using sizeof trick: sizeof(array) / sizeof(array[0])
    // Call findMax and print the result
    // Expected output: 99

    return 0;
}
```

---

### Task 4.2: Calculate Array Average

Write a function that computes the average of all values in an array.

**Important:** Be careful with integer division! Use float for the result.

**Your C Code:**
```c
#include <stdio.h>

// YOUR CODE HERE
// Write a function called calculateAverage that takes:
// - An int array (called numbers)
// - The size of the array (int size)
// Return a float representing the average

float calculateAverage(int numbers[], int size) {
    // YOUR CODE HERE
    // Sum all the numbers using a loop
    // Divide the sum by size (convert to float to avoid integer division)
    // Return the average
}

int main() {
    // YOUR CODE HERE
    // Create an array: {10, 20, 30, 40, 50}
    // Call calculateAverage and print the result
    // Expected output: 30.00
    // Use printf with %.2f format specifier

    return 0;
}
```

---

### Task 4.3: Reverse an Array In Place

Write a function that reverses the order of elements in an array. For example, {1, 2, 3} becomes {3, 2, 1}.

**Hint:** Use two pointers—one starting at the beginning, one at the end. Swap them and move them toward the middle.

**Your C Code:**
```c
#include <stdio.h>

// YOUR CODE HERE
// Write a function called reverseArray that takes:
// - An int array (called numbers)
// - The size of the array (int size)
// Reverse the array in place (no return needed, use void)

void reverseArray(int numbers[], int size) {
    // YOUR CODE HERE
    // Use two loop variables: left (start at 0) and right (start at size-1)
    // While left < right:
    //   - Swap numbers[left] and numbers[right]
    //   - Increment left
    //   - Decrement right
}

// Helper function to print an array
void printArray(int numbers[], int size) {
    printf("[");
    for (int i = 0; i < size; i++) {
        printf("%d", numbers[i]);
        if (i < size - 1) printf(", ");
    }
    printf("]\n");
}

int main() {
    // YOUR CODE HERE
    // Create an array: {1, 2, 3, 4, 5}
    // Print the original array
    // Call reverseArray
    // Print the reversed array
    // Expected output:
    // Original: [1, 2, 3, 4, 5]
    // Reversed: [5, 4, 3, 2, 1]

    return 0;
}
```

---

### Task 4.4: Multiplication Table

Write a program that prints a 10x10 multiplication table using nested loops.

**Expected Output:**
```
   1   2   3   4   5   6   7   8   9  10
1  1   2   3   4   5   6   7   8   9  10
2  2   4   6   8  10  12  14  16  18  20
3  3   6   9  12  15  18  21  24  27  30
...
```

**Your C Code:**
```c
#include <stdio.h>

int main() {
    // YOUR CODE HERE
    // Print the header row: "   1   2   3   4   5   6   7   8   9  10"
    // Use a nested loop:
    //   - Outer loop: rows (1 to 10)
    //   - Inner loop: columns (1 to 10)
    // For each cell, print the product of row * column
    // Format each number to take up 4 characters width using %4d

    return 0;
}
```

---

## Exercise 5: Strings and Memory (~30 minutes)

In this exercise, you will work with strings (character arrays) and implement string functions.

---

### Task 5.1: String Length Function

Write a function called `myStrlen()` that counts the number of characters in a string. This is similar to the built-in `strlen()` function.

**How it works:** Walk through the string character by character until you encounter the null terminator `\0`. Count how many characters you passed through.

**Your C Code:**
```c
#include <stdio.h>

// YOUR CODE HERE
// Write a function called myStrlen that takes:
// - A char pointer (char *s)
// Return an int representing the length of the string

int myStrlen(char *s) {
    // YOUR CODE HERE
    // Initialize a counter to 0
    // Use a loop: while (s[i] != '\0')
    // Increment the counter
    // Return the counter
    // Do NOT use the built-in strlen() function
}

int main() {
    // YOUR CODE HERE
    // Test your function with these strings:
    // "Hello" (should be 5)
    // "C Programming" (should be 13)
    // "" (empty string, should be 0)
    // For each test, print the string and its length

    return 0;
}
```

---

### Task 5.2: Caesar Cipher

A Caesar cipher shifts each letter in a message by a fixed number of positions in the alphabet.

**Example:** Shift by 1
- 'A' becomes 'B'
- 'B' becomes 'C'
- 'Z' wraps around to 'A'
- Non-letters stay the same

**Your C Code:**
```c
#include <stdio.h>
#include <ctype.h>

// YOUR CODE HERE
// Write a function called caesarCipher that takes:
// - A char array (the message to encode)
// - An int (the shift amount)
// Modify the array in place (each character gets shifted)

void caesarCipher(char message[], int shift) {
    // YOUR CODE HERE
    // Loop through each character in the message
    // If the character is uppercase (use isupper() from ctype.h):
    //   - Shift it within the range 'A' to 'Z'
    //   - Use modulo 26 to wrap around (e.g., 'Z' + 1 wraps to 'A')
    // If the character is lowercase (use islower()):
    //   - Shift it within the range 'a' to 'z'
    //   - Use modulo 26 to wrap around
    // If it's not a letter, leave it unchanged
}

int main() {
    // YOUR CODE HERE
    // Test with this message: "Hello World!"
    // Shift it by 3
    // Expected output: "Khoor Zruog!"
    // To verify: H->K, e->h, l->o, l->o, o->r (shifted by 3)

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
- [ ] Code compiles without errors or warnings
- [ ] Program runs without crashing
- [ ] Output matches expected behavior
- [ ] Code has comments explaining key lines
- [ ] Variable names use camelCase
- [ ] All functions are tested in main()

---

## Extension Challenges

If you finish early, try these extensions:

**Extension 3.1:** Modify the temperature converter to ask the user for input using `scanf()`.

**Extension 4.1:** Write a function that sorts an array of numbers in ascending order.

**Extension 4.2:** Write a function that searches for a specific value in an array and returns its index.

**Extension 5.1:** Write a function that reverses a string in place.

**Extension 5.2:** Modify the Caesar cipher to handle a phrase with spaces and punctuation correctly.

