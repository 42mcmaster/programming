# prog01a — Variables, Printing, If/Else, and Loops

**Programming — Medina County Career Center**
**Standards: ODE 5.1.7, 5.2.1**

---

## Before You Start

You'll be writing C programs in **VS Code** and compiling them in the **MinGW64 shell**. For each program:

1. Create a new `.c` file in VS Code
2. Write (or paste) the code
3. Save the file
4. In MinGW64, compile with: `gcc filename.c -o filename.exe`
5. Run with: `./filename.exe`

**Keep the Study Guide open** — it has syntax reference and examples you'll need.

---

## Part 1: Walkthrough Examples

These examples get you comfortable with the workflow. Follow the instructions for each one.

---

### Walkthrough 1: Hello World (Copy-Paste)

**Copy and paste** this program into a new file called `hello.c`:

```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    printf("I am learning C!\n");
    printf("This is program number %d\n", 1);
    return 0;
}
```

Compile and run it:
```
gcc hello.c -o hello.exe
./hello.exe
```

**Question:** What was the exact output? Write it here:

```
YOUR ANSWER:


```

**What to notice:**
- `#include <stdio.h>` is required for `printf` to work
- `\n` creates a new line in the output
- `%d` gets replaced by the number after the comma
- Every line of code ends with `;`

---

### Walkthrough 2: Variables and Math (Type This One)

**Type this program yourself** into a new file called `variables.c`. Typing it helps you learn the syntax:

```c
#include <stdio.h>

int main() {
    int apples = 12;
    int eaten = 5;
    int remaining = apples - eaten;

    printf("Started with %d apples\n", apples);
    printf("Ate %d apples\n", eaten);
    printf("Apples left: %d\n", remaining);

    float price = 0.75;
    float totalCost = apples * price;
    printf("Total cost at $%.2f each: $%.2f\n", price, totalCost);

    return 0;
}
```

Compile and run it:
```
gcc variables.c -o variables.exe
./variables.exe
```

**Question:** What was the total cost printed? Write it here:

```
YOUR ANSWER:


```

**What to notice:**
- `int` is for whole numbers, `float` is for decimals
- `%d` prints integers, `%.2f` prints floats with 2 decimal places
- You can do math with variables just like in JavaScript or Python

---

### Walkthrough 3: If/Else and a Loop (Type This One)

**Type this program** into a new file called `weather.c`:

```c
#include <stdio.h>

int main() {
    int temps[5] = {45, 62, 78, 55, 90};

    for (int i = 0; i < 5; i++) {
        printf("Day %d: %d degrees - ", i + 1, temps[i]);

        if (temps[i] >= 80) {
            printf("Hot!\n");
        } else if (temps[i] >= 60) {
            printf("Nice.\n");
        } else {
            printf("Cold.\n");
        }
    }

    return 0;
}
```

Compile and run it:
```
gcc weather.c -o weather.exe
./weather.exe
```

**Question:** Which days were "Hot!", which were "Nice.", and which were "Cold."? Write the full output:

```
YOUR ANSWER:


```

**What to notice:**
- `int temps[5]` creates an array of 5 integers
- `for (int i = 0; i < 5; i++)` loops through indices 0, 1, 2, 3, 4
- The if/else chain checks conditions from top to bottom and stops at the first match
- `i + 1` turns 0-based index into 1-based day number for display

---

## Part 2: Your Tasks

Now it's your turn. Use the Study Guide and the walkthrough examples above as reference. For each task, create a new `.c` file, write the code, compile, and run it.

---

### Task 1: Personal Info Printer

Create a file called `myinfo.c`.

**What to do:**
Declare variables for your name, your age, and your GPA (make them up if you want). Print all three on separate lines using the correct format specifiers.

**Here's how the same thing looks in JavaScript and Python:**

**JavaScript:**
```javascript
var name = "Alex";
var age = 17;
var gpa = 3.5;
console.log("Name: " + name);
console.log("Age: " + age);
console.log("GPA: " + gpa);
```

**Python:**
```python
name = "Alex"
age = 17
gpa = 3.5
print(f"Name: {name}")
print(f"Age: {age}")
print(f"GPA: {gpa}")
```

**Your C starter code:**
```c
#include <stdio.h>

int main() {
    // Declare a char array for name, an int for age, a float for GPA
    // Print each one using printf with the right format specifier
    // Hint: %s for strings, %d for int, %.1f for float with 1 decimal

    return 0;
}
```

**Expected output format:**
```
Name: Alex
Age: 17
GPA: 3.5
```

---

### Task 2: Number Checker

Create a file called `checker.c`.

**What to do:**
Declare an integer variable called `num` and set it to any value you choose. Use if/else statements to print whether the number is positive, negative, or zero. Then also print whether it is even or odd.

**Hint:** The modulo operator `%` gives the remainder. `num % 2 == 0` means the number is even.

**Here's how it looks in JavaScript:**
```javascript
var num = 7;
if (num > 0) {
    console.log("Positive");
} else if (num < 0) {
    console.log("Negative");
} else {
    console.log("Zero");
}

if (num % 2 == 0) {
    console.log("Even");
} else {
    console.log("Odd");
}
```

**Your C starter code:**
```c
#include <stdio.h>

int main() {
    int num = 7;

    // Check if positive, negative, or zero and print the result
    // Then check if even or odd and print the result

    return 0;
}
```

**Expected output (for num = 7):**
```
7 is Positive
7 is Odd
```

---

### Task 3: Countdown Timer

Create a file called `countdown.c`.

**What to do:**
Use a for loop to count down from 10 to 1, printing each number. After the loop, print "Liftoff!"

**Your C starter code:**
```c
#include <stdio.h>

int main() {
    // Use a for loop that starts at 10 and counts down to 1
    // Hint: for (int i = 10; i >= 1; i--)
    // Print each number
    // After the loop, print "Liftoff!"

    return 0;
}
```

**Expected output:**
```
10
9
8
7
6
5
4
3
2
1
Liftoff!
```

---

### Task 4: Times Table Printer

Create a file called `timestable.c`.

**What to do:**
Ask the user to enter a number using `scanf`. Then use a for loop to print the multiplication table for that number, from 1 to 10.

**Your C starter code:**
```c
#include <stdio.h>

int main() {
    int num;
    printf("Enter a number: ");
    scanf("%d", &num);

    // Use a for loop from 1 to 10
    // For each iteration, print: num x i = result
    // Example: "5 x 1 = 5"

    return 0;
}
```

**Expected output (if user enters 5):**
```
Enter a number: 5
5 x 1 = 5
5 x 2 = 10
5 x 3 = 15
5 x 4 = 20
5 x 5 = 25
5 x 6 = 30
5 x 7 = 35
5 x 8 = 40
5 x 9 = 45
5 x 10 = 50
```

---

## Compilation Reminder

```
gcc filename.c -o filename.exe
./filename.exe
```

If you get errors, read them carefully — they tell you the line number. Common issues:
- Missing semicolon `;`
- Missing `#include <stdio.h>`
- Using `=` instead of `==` in comparisons
- Forgetting `\n` in printf (output looks smashed together)
- Forgetting `&` in scanf

---

## Submission Checklist

- [ ] All walkthrough questions answered
- [ ] `myinfo.c` — compiles, runs, prints your info
- [ ] `checker.c` — compiles, runs, correctly identifies positive/negative/zero and even/odd
- [ ] `countdown.c` — compiles, runs, counts down and prints "Liftoff!"
- [ ] `timestable.c` — compiles, runs, prints correct times table based on user input
- [ ] All code has comments explaining what it does
