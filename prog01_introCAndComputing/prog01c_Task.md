# prog01c — Arrays, Strings, and Encoding

**Programming — Medina County Career Center**
**Standards: ODE 5.2.1, 5.3.8, 2.3.1, 2.3.2**

---

## Before You Start

This is the most advanced task file in Lesson 01. You'll work with arrays, strings (which are just arrays of characters), ASCII encoding, and number systems. If something feels unfamiliar, check the **Study Guide** — it has examples for all of these topics.

For each program:
1. Create a new `.c` file in VS Code
2. Write (or paste) the code
3. Compile with: `gcc filename.c -o filename.exe`
4. Run with: `./filename.exe`

---

## Part 1: Walkthrough Examples

---

### Walkthrough 1: Working with an Array (Copy-Paste)

**Copy and paste** this program into a new file called `scores.c`:

```c
#include <stdio.h>

int main() {
    int scores[6] = {88, 72, 95, 64, 81, 90};
    int size = 6;
    int sum = 0;

    // Calculate the sum
    for (int i = 0; i < size; i++) {
        sum = sum + scores[i];
    }

    // Calculate the average (cast to float for decimal result)
    float average = (float)sum / size;

    printf("Scores: ");
    for (int i = 0; i < size; i++) {
        printf("%d ", scores[i]);
    }
    printf("\n");
    printf("Sum: %d\n", sum);
    printf("Average: %.2f\n", average);

    return 0;
}
```

Compile and run it:
```
gcc scores.c -o scores.exe
./scores.exe
```

**Question:** What was the sum and average?

```
YOUR ANSWER:


```

**What to notice:**
- `int scores[6]` creates an array that holds 6 integers
- Array indices go from `0` to `5` (not 1 to 6!)
- `scores[i]` accesses the element at position `i`
- `(float)sum / size` forces float division so the average has decimals

---

### Walkthrough 2: Strings and ASCII (Type This One)

**Type this program** into a new file called `ascii.c`:

```c
#include <stdio.h>

int main() {
    char word[] = "Hello";

    printf("Examining the string \"%s\":\n\n", word);

    // Loop until we hit the null terminator
    for (int i = 0; word[i] != '\0'; i++) {
        printf("  word[%d] = '%c'  ASCII value: %d\n", i, word[i], word[i]);
    }

    printf("\nFun fact: 'A' = %d, 'a' = %d, difference = %d\n",
           'A', 'a', 'a' - 'A');

    // Convert uppercase to lowercase using arithmetic
    char upper = 'H';
    char lower = upper + 32;
    printf("'%c' + 32 = '%c'\n", upper, lower);

    return 0;
}
```

Compile and run it:
```
gcc ascii.c -o ascii.exe
./ascii.exe
```

**Question:** What ASCII value does 'H' have? What about 'e'?

```
YOUR ANSWER:


```

**What to notice:**
- A string in C is an array of `char` values ending with `'\0'` (the null terminator)
- `word[i] != '\0'` — the loop stops when it reaches the end of the string
- Printing a char with `%c` shows the character; printing with `%d` shows its ASCII number
- Adding 32 to an uppercase letter gives you the lowercase version (because of how ASCII is laid out)

---

### Walkthrough 3: Integer Overflow (Type This One)

**Type this program** into a new file called `overflow.c`:

```c
#include <stdio.h>

int main() {
    unsigned char x = 250;

    printf("unsigned char can hold 0 to 255\n");
    printf("Starting at %d, adding 1 each time:\n\n", x);

    for (int i = 0; i < 8; i++) {
        printf("  x = %d\n", x);
        x = x + 1;
    }

    printf("\nNotice: after 255, it wraps back to 0!\n");
    printf("This is called INTEGER OVERFLOW.\n");

    return 0;
}
```

Compile and run it:
```
gcc overflow.c -o overflow.exe
./overflow.exe
```

**Question:** At what value did the overflow happen? What did it wrap to?

```
YOUR ANSWER:


```

**What to notice:**
- `unsigned char` stores values from 0 to 255 (1 byte = 8 bits)
- When you go past 255, it wraps around to 0 — it doesn't crash or give an error
- This is important in real programming: bugs from overflow can cause security vulnerabilities

---

## Part 2: Your Tasks

---

### Task 1: Find the Maximum

Create a file called `findmax.c`.

**What to do:**
Write a function called `findMax` that takes an integer array and its size, and returns the largest value in the array.

In `main()`, create an array with these values: `{15, 3, 42, 8, 23, 1, 99, 7}` and use your function to find and print the maximum.

**Here's how it looks in Python:**
```python
def find_max(numbers):
    max_val = numbers[0]
    for num in numbers:
        if num > max_val:
            max_val = num
    return max_val
```

**The approach in C:**
1. Start by assuming the first element is the max
2. Loop through the rest of the array
3. If you find a bigger value, update your max
4. Return the max after the loop

**Your C starter code:**
```c
#include <stdio.h>

// Write your findMax function here
// It takes: int numbers[], int size
// It returns: int (the maximum value)
// Hint: start with int maxValue = numbers[0];

int main() {
    int numbers[] = {15, 3, 42, 8, 23, 1, 99, 7};
    int size = sizeof(numbers) / sizeof(numbers[0]);

    // Call findMax and print the result
    // Expected output: "Maximum value: 99"

    return 0;
}
```

**Expected output:**
```
Maximum value: 99
```

---

### Task 2: ASCII Explorer

Create a file called `asciiexplore.c`.

**What to do:**
Write a program that does two things:

**Part A:** Print the ASCII values for all uppercase letters A through Z. Use a for loop with a `char` variable.

**Part B:** Write a function called `toUpper` that takes a lowercase character and returns the uppercase version using ASCII arithmetic (subtract 32). Test it with the letters 'h', 'e', 'l', 'p'.

**Hint for Part A:**
```c
for (char c = 'A'; c <= 'Z'; c++) {
    // Print the character and its ASCII value
}
```

**Your C starter code:**
```c
#include <stdio.h>

// Write your toUpper function here
// Takes a char, returns a char
// Subtract 32 from the lowercase letter to get uppercase

int main() {
    // Part A: Print A-Z with ASCII values
    printf("=== ASCII Table: A-Z ===\n");
    // Your loop here

    printf("\n");

    // Part B: Test your toUpper function
    printf("=== toUpper Tests ===\n");
    // Test with 'h', 'e', 'l', 'p'
    // Print like: "'h' -> 'H'"

    return 0;
}
```

**Expected output (partial):**
```
=== ASCII Table: A-Z ===
'A' = 65
'B' = 66
'C' = 67
...
'Z' = 90

=== toUpper Tests ===
'h' -> 'H'
'e' -> 'E'
'l' -> 'L'
'p' -> 'P'
```

---

### Task 3: Decimal to Binary Converter

Create a file called `binary.c`.

**What to do:**
Write a program that converts the decimal number 13 to binary using the division-by-2 method:
1. Divide the number by 2
2. Store the remainder (0 or 1)
3. Repeat with the quotient until it reaches 0
4. Print the remainders in reverse order — that's the binary number

The Study Guide has a step-by-step example of this process.

**Your C starter code:**
```c
#include <stdio.h>

int main() {
    int num = 13;
    int binary[32];  // Array to store binary digits (32 is more than enough)
    int count = 0;   // How many binary digits we've collected

    int temp = num;
    // Use a while loop:
    // while (temp > 0)
    //   binary[count] = temp % 2;   (get the remainder)
    //   temp = temp / 2;            (divide by 2)
    //   count++;

    // Print the result
    printf("Decimal: %d\n", num);
    printf("Binary: ");
    // Print the binary array in REVERSE order (from count-1 down to 0)

    printf("\n");

    return 0;
}
```

**Expected output:**
```
Decimal: 13
Binary: 1101
```

**Bonus:** After you get 13 working, try changing `num` to other values (like 8, 255, or 42) and verify the output is correct.

---

### Task 4: String Length Counter

Create a file called `mystrlen.c`.

**What to do:**
Write a function called `myStrlen` that takes a string (a `char` pointer or `char` array) and returns its length — the number of characters before the null terminator `\0`. Do NOT use the built-in `strlen()` function.

Test it with these strings: `"Hello"`, `"C Programming"`, and `""` (empty string).

**Here's how it looks in Python:**
```python
def my_strlen(s):
    count = 0
    for char in s:
        count += 1
    return count
```

**The approach in C:**
1. Start a counter at 0
2. Loop through the string: `while (s[count] != '\0')`
3. Increment the counter each time
4. Return the counter

**Your C starter code:**
```c
#include <stdio.h>

// Write your myStrlen function here
// Takes: char *s (or char s[])
// Returns: int (the length)
// Do NOT use the built-in strlen()

int main() {
    // Test with "Hello" (should be 5)
    // Test with "C Programming" (should be 13)
    // Test with "" (should be 0)
    // Print like: "\"Hello\" has length 5"

    return 0;
}
```

**Expected output:**
```
"Hello" has length 5
"C Programming" has length 13
"" has length 0
```

---

## Compilation Reminder

```
gcc filename.c -o filename.exe
./filename.exe
```

Common issues at this level:
- **Array out of bounds:** Accessing `numbers[10]` when the array only has 10 elements (indices 0-9)
- **Off-by-one in loops:** Using `<=` when you should use `<` (or vice versa)
- **Forgetting the null terminator:** Strings always have a hidden `\0` at the end
- **Printing binary backwards:** Remember to loop from `count-1` down to `0`

---

## Submission Checklist

- [ ] All walkthrough questions answered
- [ ] `findmax.c` — compiles, runs, correctly finds the maximum value
- [ ] `asciiexplore.c` — compiles, runs, prints ASCII table and toUpper results
- [ ] `binary.c` — compiles, runs, correctly converts 13 to binary (1101)
- [ ] `mystrlen.c` — compiles, runs, correctly counts string lengths
- [ ] All code has comments explaining what it does
