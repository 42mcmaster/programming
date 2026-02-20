# CS50 Filter: Image Processing with Structs and 2D Arrays
## Medina County Career Center — CTE Programming Course
### Step-by-Step Walkthrough for Windows with GCC

---

## Part 1: Understanding the Scaffold

### File Structure Overview

When you unzip the CS50 filter project, you will see these key files:

- **bmp.h** — Contains BMP file format definitions and struct definitions (read-only reference)
- **helpers.h** — Function prototypes that YOU will implement (do not modify)
- **filter.c** — Main program logic that loads/processes images (DO NOT MODIFY)
- **helpers.c** — YOUR CODE GOES HERE (only file you edit for the core functions)

### The RGBTRIPLE Struct

This is the fundamental building block. Look at bmp.h:

```c
typedef struct
{
    BYTE rgbtBlue;
    BYTE rgbtGreen;
    BYTE rgbtRed;
}
RGBTRIPLE;
```

What you need to know:
- **BYTE** is defined as `unsigned char` — values range 0 to 255
- Each pixel is ONE RGBTRIPLE containing three BYTE values
- Order is BGR (Blue, Green, Red), not RGB — this is BMP format
- When we do grayscale, all three values become the same number

### How Images Are Stored in Memory

- Images are stored as a **2D array of RGBTRIPLE**
- If the image is 800 pixels wide and 600 pixels tall:
  - You have a 2D array: `RGBTRIPLE image[600][800]`
  - `image[row][col]` gives you one pixel
  - Each pixel has `.rgbtBlue`, `.rgbtGreen`, `.rgbtRed` attributes

Accessing a pixel:
```c
RGBTRIPLE pixel = image[50][100];  // Row 50, column 100
int blueValue = pixel.rgbtBlue;
image[50][100].rgbtRed = 200;      // Modify red component
```

### Compiling Your Code on Windows

Open Command Prompt in your project directory and type:

```
gcc -o filter filter.c helpers.c -lm
```

Explanation:
- `gcc` — the compiler
- `-o filter` — output file named "filter"
- `filter.c helpers.c` — source files to compile
- `-lm` — link the math library (needed for round(), sqrt(), etc.)

Run your program:
```
filter.exe input.bmp output.bmp
```

---

## Part 2: Structs Warm-Up (Try This)

Create a new file called `struct_warmup.c` and write the following code. This will help you understand how structs work before tackling RGBTRIPLE.

**Task:** Define a Student struct and practice with an array of students.

```c
#include <stdio.h>

// Define Student struct
typedef struct
{
    char name[50];
    int gradeLevel;
    float gpa;
}
Student;

int main(void)
{
    // Create an array of 3 students
    Student roster[3];

    // Fill in student data
    // YOUR CODE HERE: Set up the three students
    // For example: roster[0].name = "Alice", roster[0].gradeLevel = 11, etc.

    // Loop through and print each student
    // YOUR CODE HERE: Use a for loop from i = 0 to 2
    // Inside the loop, print: "Name: Alice, Grade: 11, GPA: 3.85"

    return 0;
}
```

**Challenge:** Write a helper function `isHonorRoll()` that takes a Student and returns 1 (true) if GPA >= 3.5, otherwise 0 (false).

```c
// YOUR CODE HERE: Define the function
```

After you finish, compile and test it:
```
gcc -o struct_warmup struct_warmup.c
struct_warmup.exe
```

---

## Part 3: 2D Array Warm-Up (Try This)

Create a file called `array2d_warmup.c`. This prepares you for working with the 2D pixel array.

**Task:** Work with a 3x3 grid of integers.

```c
#include <stdio.h>

int main(void)
{
    // Declare and initialize a 3x3 grid
    int grid[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    // Print the grid in a formatted table
    printf("Grid:\n");
    for (int row = 0; row < 3; row++)
    {
        for (int col = 0; col < 3; col++)
        {
            printf("%d ", grid[row][col]);
        }
        printf("\n");
    }

    // Find and print the sum of all elements
    int sum = 0;
    // YOUR CODE HERE: Use nested loops to add all grid values to sum

    printf("Sum: %d\n", sum);

    return 0;
}
```

Expected output:
```
Grid:
1 2 3
4 5 6
7 8 9
Sum: 45
```

---

## Part 4: Grayscale Filter (Code Together)

This is the first filter you will implement in helpers.c.

### Understanding the Logic

Grayscale means converting a color image to black and white shades. The formula is:
- Average the three color values: (Red + Green + Blue) / 3
- Set all three values to this average

Example:
- Original pixel: Red=200, Green=100, Blue=50
- Average: (200 + 100 + 50) / 3 = 116.67
- Rounded: 117
- Result: Red=117, Green=117, Blue=117

### The Grayscale Function Header

In helpers.c, you will find:

```c
void grayscale(int height, int width, RGBTRIPLE image[height][width])
{
    // YOUR CODE HERE
}
```

### Step-by-Step Implementation

**Step 1:** Understand the parameters
- `height` — number of rows
- `width` — number of columns
- `image[height][width]` — 2D array of RGBTRIPLE

**Step 2:** Write the nested loop structure

```c
void grayscale(int height, int width, RGBTRIPLE image[height][width])
{
    for (int row = 0; row < height; row++)
    {
        for (int col = 0; col < width; col++)
        {
            // YOUR CODE HERE: Process image[row][col]
        }
    }
}
```

**Step 3:** Inside the inner loop, calculate and apply grayscale

```c
            // Get the current pixel
            RGBTRIPLE pixel = image[row][col];

            // Calculate average of the three colors
            // YOUR CODE HERE: Compute avg = (red + green + blue) / 3.0

            // Round the average to nearest integer
            // Hint: Use round() from math.h
            // int grayValue = round(avg);

            // Set all three color values to the gray value
            // YOUR CODE HERE: Set image[row][col].rgbtRed to grayValue
            // YOUR CODE HERE: Set image[row][col].rgbtGreen to grayValue
            // YOUR CODE HERE: Set image[row][col].rgbtBlue to grayValue
```

### Tips for Getting It Right

- Make sure to cast to float when dividing: `(red + green + blue) / 3.0`
- Use `round()` from math.h to round to nearest integer
- Modify the struct members directly: `image[row][col].rgbtRed = newValue;`
- Check the order: BGR not RGB (but for grayscale it does not matter)

---

## Part 5: Reflect Filter (Try This)

This filter flips the image horizontally (left-right mirror).

### Understanding the Logic

Imagine looking at a photograph in a mirror. The left side becomes the right side.

For each row, you swap:
- Column 0 with Column (width - 1)
- Column 1 with Column (width - 2)
- And so on...

Example for a 5-pixel-wide row:
```
Before:  [A] [B] [C] [D] [E]
After:   [E] [D] [C] [B] [A]
```

### The Reflect Function Header

```c
void reflect(int height, int width, RGBTRIPLE image[height][width])
{
    // YOUR CODE HERE
}
```

### Swap Algorithm with Temporary Variable

To swap two values:

```c
RGBTRIPLE temp = image[row][left];
image[row][left] = image[row][right];
image[row][right] = temp;
```

### Step-by-Step Implementation

**Step 1:** Outer loop for each row

```c
void reflect(int height, int width, RGBTRIPLE image[height][width])
{
    for (int row = 0; row < height; row++)
    {
        // Process one row at a time
        // YOUR CODE HERE: Inner loop for swapping columns
    }
}
```

**Step 2:** Inner loop for swapping columns

```c
        // Start from left = 0, right = width - 1
        // Loop while left < right (swap pairs)
        // YOUR CODE HERE: Decrement right or increment left each iteration
        {
            // YOUR CODE HERE: Swap image[row][left] with image[row][right]
            // Use the temp variable swap method
        }
```

### Tips for Getting It Right

- The loop condition should be `left < right` (stop when you reach the middle)
- After each swap, move left forward and right backward
- You only need to go halfway across the row
- Make sure you understand why we stop at the middle

---

## Code Style Guidelines for This Course

Follow these standards in all your code:

- **Naming:** Use camelCase for variable names (pixelValue, imageHeight, rgbComponent)
- **Comments:** Add comments above every function and complex section
- **Spacing:** Use consistent indentation (4 spaces)
- **Clarity:** Write code that is easy to read and understand
- **No shortcuts:** Avoid using emojis or non-standard abbreviations in code

---

## Compilation and Testing Checklist

Before submitting your helpers.c:

- [ ] Code compiles without warnings: `gcc -o filter filter.c helpers.c -lm`
- [ ] No errors when linking the math library
- [ ] Each function is properly implemented
- [ ] Variable names are in camelCase
- [ ] Code is properly commented
- [ ] Test with provided sample images (if available)

---

## Next Steps

Once you complete the four filters (grayscale, reflect, blur, edges):

1. Test each filter individually
2. Review your code for clarity and comments
3. Ensure all compilation warnings are resolved
4. Submit helpers.c with all four filters implemented

Good luck with the assignment!
