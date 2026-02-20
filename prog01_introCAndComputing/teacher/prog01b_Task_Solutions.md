# prog01 Session B — Functions, Arrays, and Memory

**INSTRUCTOR SOLUTIONS — DO NOT DISTRIBUTE TO STUDENTS**

**Standards: ODE 5.2.1, 5.2.3, 5.3.8, 2.3.1**

---

## Exercise 3: Functions, Types, and Math

### Task 3.1: Temperature Conversion

**Solution:**
```c
#include <stdio.h>

// Function to convert Fahrenheit to Celsius
float fahrenheitToCelsius(float fahrenheit) {
    // Formula: C = (F - 32) * 5/9
    // Use 5.0 and 9.0 (with decimals) to ensure floating-point division
    return (fahrenheit - 32) * 5.0 / 9.0;
}

int main() {
    // Test the function with known values
    float f1 = 32.0;
    float c1 = fahrenheitToCelsius(f1);
    printf("%.2f F = %.2f C\n", f1, c1);

    float f2 = 212.0;
    float c2 = fahrenheitToCelsius(f2);
    printf("%.2f F = %.2f C\n", f2, c2);

    float f3 = 68.0;
    float c3 = fahrenheitToCelsius(f3);
    printf("%.2f F = %.2f C\n", f3, c3);

    return 0;
}
```

**Expected Output:**
```
32.00 F = 0.00 C
212.00 F = 100.00 C
68.00 F = 20.00 C
```

**Instructor Note:**
This task illustrates the critical difference between integer and floating-point division:
- If written as `(fahrenheit - 32) * 5 / 9`, C performs integer division (5/9 = 0), yielding wrong results
- By writing `5.0 / 9.0`, we force floating-point division

Have students intentionally write the wrong version to see the difference:
```c
// Wrong: integer division
return (fahrenheit - 32) * 5 / 9;  // Returns 0 for 32 F!

// Right: floating-point division
return (fahrenheit - 32) * 5.0 / 9.0;  // Returns 0.00 for 32 F
```

---

### Task 3.2: Clamp Function

**Solution:**
```c
#include <stdio.h>

// Function to clamp a value within a range
int clamp(int value, int minValue, int maxValue) {
    // If value is below minimum, return minimum
    if (value < minValue) {
        return minValue;
    }
    // If value is above maximum, return maximum
    else if (value > maxValue) {
        return maxValue;
    }
    // Otherwise, value is within range
    else {
        return value;
    }
}

int main() {
    // Test cases demonstrating all three conditions

    // Test 1: Value within range
    printf("clamp(5, 0, 10) = %d\n", clamp(5, 0, 10));

    // Test 2: Value below minimum
    printf("clamp(-2, 0, 10) = %d\n", clamp(-2, 0, 10));

    // Test 3: Value above maximum
    printf("clamp(15, 0, 10) = %d\n", clamp(15, 0, 10));

    // Test 4: Different range
    printf("clamp(75, 50, 100) = %d\n", clamp(75, 50, 100));

    // Test 5: At minimum boundary
    printf("clamp(0, 0, 10) = %d\n", clamp(0, 0, 10));

    // Test 6: At maximum boundary
    printf("clamp(10, 0, 10) = %d\n", clamp(10, 0, 10));

    return 0;
}
```

**Expected Output:**
```
clamp(5, 0, 10) = 5
clamp(-2, 0, 10) = 0
clamp(15, 0, 10) = 10
clamp(75, 50, 100) = 75
clamp(0, 0, 10) = 0
clamp(10, 0, 10) = 10
```

**Instructor Note:**
Alternative ternary operator implementation:
```c
int clamp(int value, int minValue, int maxValue) {
    return (value < minValue) ? minValue : ((value > maxValue) ? maxValue : value);
}
```

This function is extremely useful in graphics programming, game development, and any system that needs to constrain values to a safe range. Clamp functions prevent errors like array out-of-bounds access or oversaturated color values.

---

### Task 3.3: Weighted Average

**Solution:**
```c
#include <stdio.h>

// Function to calculate weighted average of three scores
float weightedAverage(float score1, float score2, float score3,
                      float weight1, float weight2, float weight3) {
    // Weighted average = (score1 * weight1) + (score2 * weight2) + (score3 * weight3)
    return (score1 * weight1) + (score2 * weight2) + (score3 * weight3);
}

int main() {
    // Test case: Grades with different weights
    // Homework: 80 (weight 0.5)
    // Midterm: 90 (weight 0.3)
    // Final Exam: 70 (weight 0.2)
    float finalGrade = weightedAverage(80, 90, 70, 0.5, 0.3, 0.2);
    printf("Weighted Average: %.2f\n", finalGrade);

    // Test case 2: All scores are equal
    float avg2 = weightedAverage(85, 85, 85, 0.5, 0.3, 0.2);
    printf("Weighted Average: %.2f\n", avg2);

    // Test case 3: Different weights
    float avg3 = weightedAverage(100, 75, 60, 0.6, 0.3, 0.1);
    printf("Weighted Average: %.2f\n", avg3);

    return 0;
}
```

**Expected Output:**
```
Weighted Average: 81.00
Weighted Average: 85.00
Weighted Average: 89.50
```

**Instructor Note:**
Real-world application: This function mimics how many schools calculate final grades. The weights represent the importance of each assessment:
- If homework is heavily weighted (0.5), it has more impact than exams
- This teaches students why doing homework throughout the semester matters

Edge case to discuss: What if the weights don't sum to 1.0? The function will still work, but the result won't be a true "average." Have students add input validation if they want to extend this.

---

### Task 3.4: Grade Calculator

**Solution:**
```c
#include <stdio.h>

// Function to convert numeric score to letter grade
char getGrade(int score) {
    // Check ranges from highest to lowest
    if (score >= 90) {
        return 'A';
    }
    else if (score >= 80) {
        return 'B';
    }
    else if (score >= 70) {
        return 'C';
    }
    else if (score >= 60) {
        return 'D';
    }
    else {
        return 'F';
    }
}

int main() {
    // Test cases covering each grade range

    // Grade A
    int score1 = 95;
    printf("Score: %d, Grade: %c\n", score1, getGrade(score1));

    // Grade B
    int score2 = 85;
    printf("Score: %d, Grade: %c\n", score2, getGrade(score2));

    // Grade C
    int score3 = 75;
    printf("Score: %d, Grade: %c\n", score3, getGrade(score3));

    // Grade D
    int score4 = 65;
    printf("Score: %d, Grade: %c\n", score4, getGrade(score4));

    // Grade F
    int score5 = 50;
    printf("Score: %d, Grade: %c\n", score5, getGrade(score5));

    return 0;
}
```

**Expected Output:**
```
Score: 95, Grade: A
Score: 85, Grade: B
Score: 75, Grade: C
Score: 65, Grade: D
Score: 50, Grade: F
```

**Instructor Note:**
This is a great example of control flow. Key teaching points:
- Order matters: Check conditions from highest to lowest
- Use `>=` not `>` to include the boundary value
- A function can return different types (in this case, char)

Alternative implementation using a switch statement would be more cumbersome here because scores are ranges, not discrete values. However, you could use a switch on `score / 10` if you wanted to demonstrate switch statements.

---

## Exercise 4: Arrays and Loops

### Task 4.1: Find Maximum in Array

**Solution:**
```c
#include <stdio.h>

// Function to find the maximum value in an array
int findMax(int numbers[], int size) {
    // Start with the first element as the maximum
    int maxValue = numbers[0];

    // Loop through the rest of the elements
    for (int i = 1; i < size; i++) {
        // If current element is larger, update maxValue
        if (numbers[i] > maxValue) {
            maxValue = numbers[i];
        }
    }

    return maxValue;
}

int main() {
    // Create an array of integers
    int numbers[] = {15, 3, 42, 8, 23, 1, 99};

    // Calculate the size using the sizeof trick
    int size = sizeof(numbers) / sizeof(numbers[0]);

    // Find and print the maximum
    int max = findMax(numbers, size);
    printf("Maximum value: %d\n", max);

    return 0;
}
```

**Expected Output:**
```
Maximum value: 99
```

**Instructor Note:**
Key concepts:
1. Arrays decay to pointers when passed to functions, so we need a separate `size` parameter
2. The sizeof trick only works for arrays declared in the same scope (not for function parameters)
3. Loop starts at index 1 (not 0) since we already have the first element as maxValue

Common mistake: Starting the loop at 0 and comparing with uninitialized maxValue variable.

Alternative implementation with better comments for students:
```c
int findMax(int numbers[], int size) {
    // Assume the first number is the largest
    int maxValue = numbers[0];

    // Check all remaining numbers
    for (int i = 1; i < size; i++) {
        // Did we find a bigger number?
        if (numbers[i] > maxValue) {
            maxValue = numbers[i];  // Yes, update our maximum
        }
    }

    return maxValue;
}
```

---

### Task 4.2: Calculate Array Average

**Solution:**
```c
#include <stdio.h>

// Function to calculate the average of array elements
float calculateAverage(int numbers[], int size) {
    // Sum all the numbers
    int sum = 0;
    for (int i = 0; i < size; i++) {
        sum = sum + numbers[i];
    }

    // Divide sum by size to get average
    // Cast to float to ensure floating-point division
    float average = (float)sum / size;

    return average;
}

int main() {
    // Create an array of integers
    int numbers[] = {10, 20, 30, 40, 50};

    // Calculate the size
    int size = sizeof(numbers) / sizeof(numbers[0]);

    // Calculate and print the average
    float average = calculateAverage(numbers, size);
    printf("Average: %.2f\n", average);

    return 0;
}
```

**Expected Output:**
```
Average: 30.00
```

**Instructor Note:**
Critical teaching point: The cast to float!
- If you write `sum / size` with both as integers, you get integer division (150 / 5 = 30)
- Even though the function returns float, the division happens before the return
- By casting: `(float)sum / size`, we force floating-point division

Show students the difference:
```c
// Wrong: integer division
int sum = 150;
int size = 5;
float result = sum / size;  // 30.0 (wrong!)

// Right: floating-point division
float result = (float)sum / size;  // 30.0 (correct!)
```

Real-world analogy: This is like the difference between cutting a pie into 5 pieces and keeping one piece (integer) vs. actually measuring the weight of one piece (float).

---

### Task 4.3: Reverse an Array In Place

**Solution:**
```c
#include <stdio.h>

// Function to reverse an array in place
void reverseArray(int numbers[], int size) {
    // Use two pointers: one at the start, one at the end
    int left = 0;           // Start at beginning
    int right = size - 1;   // Start at end

    // Keep swapping elements while left < right
    while (left < right) {
        // Swap numbers[left] and numbers[right]
        int temp = numbers[left];
        numbers[left] = numbers[right];
        numbers[right] = temp;

        // Move pointers toward the middle
        left++;
        right--;
    }
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
    // Create an array
    int numbers[] = {1, 2, 3, 4, 5};
    int size = sizeof(numbers) / sizeof(numbers[0]);

    // Print original array
    printf("Original: ");
    printArray(numbers, size);

    // Reverse the array
    reverseArray(numbers, size);

    // Print reversed array
    printf("Reversed: ");
    printArray(numbers, size);

    return 0;
}
```

**Expected Output:**
```
Original: [1, 2, 3, 4, 5]
Reversed: [5, 4, 3, 2, 1]
```

**Instructor Note:**
This algorithm uses the two-pointer technique, which is fundamental in computer science:
- For an odd-length array, when left and right meet at the middle element, that element doesn't move (correct behavior)
- For an even-length array, left and right swap the middle two elements

Show the trace for array [1, 2, 3, 4, 5]:
```
Initial: left=0, right=4
Step 1: Swap numbers[0] and numbers[4] -> [5, 2, 3, 4, 1], left=1, right=3
Step 2: Swap numbers[1] and numbers[3] -> [5, 4, 3, 2, 1], left=2, right=2
Done: left >= right, exit loop
```

Important: The function modifies the array in place (using the pointer), rather than creating a new array. This is memory-efficient but means the original array is changed.

---

### Task 4.4: Multiplication Table

**Solution:**
```c
#include <stdio.h>

int main() {
    // Print header row (column labels)
    printf("   ");  // Indent for row labels
    for (int col = 1; col <= 10; col++) {
        printf("%4d", col);  // Each number takes 4 characters
    }
    printf("\n");

    // Print separator line (optional, for clarity)
    printf("    ");
    for (int col = 1; col <= 10; col++) {
        printf("----");
    }
    printf("\n");

    // Outer loop: rows (1 to 10)
    for (int row = 1; row <= 10; row++) {
        // Print row label
        printf("%2d |", row);

        // Inner loop: columns (1 to 10)
        for (int col = 1; col <= 10; col++) {
            // Print the product with 4-character width
            printf("%4d", row * col);
        }
        printf("\n");
    }

    return 0;
}
```

**Expected Output:**
```
    1   2   3   4   5   6   7   8   9  10
    --------------------------------------------
 1 |   1   2   3   4   5   6   7   8   9  10
 2 |   2   4   6   8  10  12  14  16  18  20
 3 |   3   6   9  12  15  18  21  24  27  30
 4 |   4   8  12  16  20  24  28  32  36  40
 5 |   5  10  15  20  25  30  35  40  45  50
 6 |   6  12  18  24  30  36  42  48  54  60
 7 |   7  14  21  28  35  42  49  56  63  70
 8 |   8  16  24  32  40  48  56  64  72  80
 9 |   9  18  27  36  45  54  63  72  81  90
10 |  10  20  30  40  50  60  70  80  90 100
```

**Instructor Note:**
Key teaching points:
1. Nested loops: The outer loop controls rows, the inner loop controls columns
2. Format specifiers: `%4d` means "print integer right-aligned in 4 characters"
3. The order of loops matters for output formatting

Common mistakes students make:
- Using `%d` instead of `%4d`, which produces misaligned output
- Printing the header and separator outside the loops (makes it harder to see the structure)
- Off-by-one errors with the loop bounds

Extension: Have students add up the entire sum of the multiplication table (should be 3025).

---

## Exercise 5: Strings and Memory

### Task 5.1: String Length Function

**Solution:**
```c
#include <stdio.h>

// Function to calculate string length
int myStrlen(char *s) {
    // Start with a count of 0
    int count = 0;

    // Walk through the string until we hit the null terminator
    while (s[count] != '\0') {
        count++;
    }

    return count;
}

int main() {
    // Test case 1: "Hello"
    char str1[] = "Hello";
    printf("String: \"%s\", Length: %d\n", str1, myStrlen(str1));

    // Test case 2: "C Programming"
    char str2[] = "C Programming";
    printf("String: \"%s\", Length: %d\n", str2, myStrlen(str2));

    // Test case 3: Empty string
    char str3[] = "";
    printf("String: \"%s\", Length: %d\n", str3, myStrlen(str3));

    return 0;
}
```

**Expected Output:**
```
String: "Hello", Length: 5
String: "C Programming", Length: 13
String: "", Length: 0
```

**Instructor Note:**
This exercise teaches a fundamental concept: strings in C are null-terminated.
- Every string ends with `\0` (the null character), even if it's not visible
- The null terminator is not counted in the length
- This is how C knows where a string ends (unlike languages like Python that store length explicitly)

Alternative implementation using pointer arithmetic:
```c
int myStrlen(char *s) {
    char *start = s;
    while (*s != '\0') {
        s++;
    }
    return s - start;
}
```

This is more "C-like" but harder for beginners to understand. The array indexing version is clearer.

---

### Task 5.2: Caesar Cipher

**Solution:**
```c
#include <stdio.h>
#include <ctype.h>

// Function to encode a string with Caesar cipher
void caesarCipher(char message[], int shift) {
    // Loop through each character in the message
    for (int i = 0; message[i] != '\0'; i++) {
        char c = message[i];

        // Handle uppercase letters
        if (isupper(c)) {
            // Shift within the range A-Z
            // Subtract 'A', add shift, use modulo 26 to wrap around, add 'A' back
            message[i] = (c - 'A' + shift) % 26 + 'A';
        }
        // Handle lowercase letters
        else if (islower(c)) {
            // Shift within the range a-z
            message[i] = (c - 'a' + shift) % 26 + 'a';
        }
        // Non-letters (spaces, punctuation) stay unchanged
    }
}

int main() {
    // Test the Caesar cipher
    char message[] = "Hello World!";
    int shift = 3;

    printf("Original: %s\n", message);

    // Apply the cipher
    caesarCipher(message, shift);

    printf("Encoded (shift=%d): %s\n", shift, message);

    return 0;
}
```

**Expected Output:**
```
Original: Hello World!
Encoded (shift=3): Khoor Zruog!
```

**Instructor Note:**
The modulo operation is crucial here:
- `(c - 'a' + shift) % 26` keeps the result within 0-25
- Without it, 'z' shifted by 1 would become '{' (ASCII 123), not 'a'

Example trace for 'H' with shift 3:
- 'H' - 'A' = 7
- 7 + 3 = 10
- 10 % 26 = 10
- 10 + 'A' = 'K'

Example trace for 'z' with shift 1:
- 'z' - 'a' = 25
- 25 + 1 = 26
- 26 % 26 = 0 (wraps around!)
- 0 + 'a' = 'a'

The Caesar cipher is one of the oldest encryption methods and illustrates:
1. Character encoding (ASCII/Unicode)
2. Modular arithmetic
3. The importance of understanding boundaries and wrapping

Real-world note: Caesar cipher is not secure (only 26 possible keys), but the concept leads to modern encryption algorithms.

---

## Common Student Mistakes and Teaching Tips

**Mistake 1: Forgetting to cast to float for division**
```c
// Wrong: integer division
float result = sum / size;

// Right: floating-point division
float result = (float)sum / size;
```

**Mistake 2: Array indexing confusion**
- Forgetting that arrays are 0-indexed
- Confusing array size with the last valid index (size-1)

**Mistake 3: String termination**
- Not realizing strings end with `\0`
- Trying to access elements beyond the null terminator

**Mistake 4: Loop boundaries**
- Off-by-one errors in nested loops
- Incorrect loop conditions for array traversal

**Mistake 5: Pointer and array confusion**
- Not understanding that array names decay to pointers
- Trying to use `sizeof()` on array parameters in functions

**Mistake 6: Modulo operator misunderstanding**
- Not understanding why `(value) % 26` keeps values in range 0-25
- Forgetting that modulo is needed for wrapping behavior

---

## Time Allocation Guide

- Task 3.1: 8-10 minutes
- Task 3.2: 10-12 minutes
- Task 3.3: 8-10 minutes
- Task 3.4: 10-12 minutes
- Task 4.1: 10-12 minutes
- Task 4.2: 12-15 minutes (emphasis on float casting)
- Task 4.3: 12-15 minutes (two-pointer technique)
- Task 4.4: 10-12 minutes
- Task 5.1: 8-10 minutes
- Task 5.2: 12-15 minutes (modulo arithmetic)

Total: approximately 110-130 minutes (allows for discussion and troubleshooting)

---

## Extensions for Advanced Students

If students finish early, assign these extensions:

**Extension 3.1:** Modify temperature converter to accept user input with `scanf()`:
```c
float fahrenheit;
printf("Enter temperature in Fahrenheit: ");
scanf("%f", &fahrenheit);
```

**Extension 4.1:** Implement a bubble sort function to sort an array.

**Extension 4.2:** Write a binary search function to find a value in a sorted array.

**Extension 5.1:** Write a function that reverses a string in place (similar to Task 4.3).

**Extension 5.2:** Extend Caesar cipher to accept shift values that wrap correctly with negative numbers.

