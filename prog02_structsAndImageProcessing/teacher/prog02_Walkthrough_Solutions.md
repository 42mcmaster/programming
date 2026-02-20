# CS50 Filter: Image Processing with Structs and 2D Arrays
## INSTRUCTOR SOLUTIONS — DO NOT DISTRIBUTE TO STUDENTS
### Medina County Career Center — CTE Programming Course

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

## Part 2: Structs Warm-Up (Solution)

### Instructor Note:
This exercise typically takes 10-15 minutes. Students should understand:
- How to define structs with typedef
- How to create arrays of structs
- How to access struct members with dot notation
- How to write functions that accept structs as parameters

Common mistakes:
- Using incorrect array indexing: `roster.name` instead of `roster[0].name`
- Forgetting to cast name assignment (char arrays need strcpy or direct string assignment in initialization)
- Off-by-one errors in the loop condition

### Complete Solution for struct_warmup.c

```c
#include <stdio.h>
#include <string.h>

// Define Student struct
typedef struct
{
    char name[50];
    int gradeLevel;
    float gpa;
}
Student;

// Helper function to check honor roll status
int isHonorRoll(Student student)
{
    if (student.gpa >= 3.5)
    {
        return 1;  // true
    }
    return 0;  // false
}

int main(void)
{
    // Create an array of 3 students
    Student roster[3];

    // Fill in student data
    strcpy(roster[0].name, "Alice");
    roster[0].gradeLevel = 11;
    roster[0].gpa = 3.85;

    strcpy(roster[1].name, "Bob");
    roster[1].gradeLevel = 10;
    roster[1].gpa = 3.20;

    strcpy(roster[2].name, "Charlie");
    roster[2].gradeLevel = 12;
    roster[2].gpa = 3.95;

    // Loop through and print each student
    for (int i = 0; i < 3; i++)
    {
        printf("Name: %s, Grade: %d, GPA: %.2f", roster[i].name, roster[i].gradeLevel, roster[i].gpa);

        if (isHonorRoll(roster[i]))
        {
            printf(" (Honor Roll)\n");
        }
        else
        {
            printf("\n");
        }
    }

    return 0;
}
```

### Expected Output:

```
Name: Alice, Grade: 11, GPA: 3.85 (Honor Roll)
Name: Bob, Grade: 10, GPA: 3.20
Name: Charlie, Grade: 12, GPA: 3.95 (Honor Roll)
```

### Instructor Note:
- Compile: `gcc -o struct_warmup struct_warmup.c`
- Some students may struggle with strcpy. Alternative: use string initialization in a struct initializer list (though strcpy is cleaner for beginners to understand)
- The %.2f format specifier prints 2 decimal places for GPA
- Point out that the isHonorRoll function demonstrates passing structs to functions — a key pattern they will use in the actual filter functions

---

## Part 3: 2D Array Warm-Up (Solution)

### Instructor Note:
This exercise typically takes 10-12 minutes. Students should understand:
- How to declare and initialize 2D arrays
- Nested loop structure for traversing 2D arrays
- Indexing with [row][col]
- Accumulating values with nested loops

Common mistakes:
- Incorrect loop bounds (using width for both dimensions, or starting at 1 instead of 0)
- Confusing row and column order
- Not initializing sum to 0 before the loop
- Trying to use single-loop operations on 2D arrays

### Complete Solution for array2d_warmup.c

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
    for (int row = 0; row < 3; row++)
    {
        for (int col = 0; col < 3; col++)
        {
            sum += grid[row][col];
        }
    }

    printf("Sum: %d\n", sum);

    return 0;
}
```

### Expected Output:

```
Grid:
1 2 3
4 5 6
7 8 9
Sum: 45
```

### Instructor Note:
- Compile: `gcc -o array2d_warmup array2d_warmup.c`
- After students complete this, ask them: "What would change if the grid were 4x4?" (Better: let them try to generalize with height and width variables)
- Advanced extension: Have them print only the diagonal: 1, 5, 9 (where row == col)
- Pacing: If students struggle with nested loops, spend extra time walking through the loop order before the assignment

---

## Part 4: Grayscale Filter (Solution)

### Instructor Note:
This is the core assignment. Expected completion: 15-20 minutes of coding after warm-ups.

Key concepts to emphasize:
- Casting to float to avoid integer division
- Why we round() instead of truncating
- The BGR color order in BMP format (but doesn't matter for grayscale since all three values become identical)
- Modifying struct members directly: image[row][col].rgbtRed = value

Common mistakes:
- Integer division: avg = (red + green + blue) / 3 yields wrong results
- Forgetting to round: leaves fractional values in unsigned char (gets truncated)
- Only modifying one color channel instead of all three
- Off-by-one loop errors

### Complete Solution for grayscale() in helpers.c

```c
#include <math.h>
#include "helpers.h"

void grayscale(int height, int width, RGBTRIPLE image[height][width])
{
    for (int row = 0; row < height; row++)
    {
        for (int col = 0; col < width; col++)
        {
            // Get the current pixel
            RGBTRIPLE pixel = image[row][col];

            // Calculate average of the three colors using float division
            float avg = (pixel.rgbtRed + pixel.rgbtGreen + pixel.rgbtBlue) / 3.0;

            // Round the average to nearest integer
            int grayValue = (int) round(avg);

            // Set all three color values to the gray value
            image[row][col].rgbtRed = grayValue;
            image[row][col].rgbtGreen = grayValue;
            image[row][col].rgbtBlue = grayValue;
        }
    }
}
```

### Alternative (More Compact) Solution:

```c
void grayscale(int height, int width, RGBTRIPLE image[height][width])
{
    for (int row = 0; row < height; row++)
    {
        for (int col = 0; col < width; col++)
        {
            // Calculate and set gray value in one step
            int gray = (int) round((image[row][col].rgbtRed +
                                     image[row][col].rgbtGreen +
                                     image[row][col].rgbtBlue) / 3.0);

            image[row][col].rgbtRed = gray;
            image[row][col].rgbtGreen = gray;
            image[row][col].rgbtBlue = gray;
        }
    }
}
```

### Instructor Note:
- Both solutions are correct. The first is more readable for beginners.
- The cast to (int) before round() is technically redundant since round() returns a double, but explicit casting is good practice.
- Test with a sample image to verify correct output
- This filter is fundamental — don't move on until students understand it deeply
- Walk through one pixel by hand with students if needed (e.g., pixel with R=100, G=150, B=200 → avg=150)

---

## Part 5: Reflect Filter (Solution)

### Instructor Note:
This exercise typically takes 15-20 minutes. Students often struggle with the swap logic.

Key concepts:
- Why we need a temporary variable for swapping
- Understanding why we only loop to the middle of the row (left < right)
- Off-by-one errors in the swap loop

Common mistakes:
- Forgetting the temp variable and trying: a = b; b = a; (both end up the same)
- Using left <= right instead of left < right (leads to improper behavior or no change)
- Incrementing/decrementing by wrong amount
- Confusing left and right indices

### Complete Solution for reflect() in helpers.c

```c
void reflect(int height, int width, RGBTRIPLE image[height][width])
{
    for (int row = 0; row < height; row++)
    {
        for (int left = 0, right = width - 1; left < right; left++, right--)
        {
            // Swap the pixel at [row][left] with the pixel at [row][right]
            RGBTRIPLE temp = image[row][left];
            image[row][left] = image[row][right];
            image[row][right] = temp;
        }
    }
}
```

### Alternative (Using Separate Variables):

```c
void reflect(int height, int width, RGBTRIPLE image[height][width])
{
    for (int row = 0; row < height; row++)
    {
        int left = 0;
        int right = width - 1;

        while (left < right)
        {
            // Swap the pixel at [row][left] with the pixel at [row][right]
            RGBTRIPLE temp = image[row][left];
            image[row][left] = image[row][right];
            image[row][right] = temp;

            left++;
            right--;
        }
    }
}
```

### How It Works (Example with 5-pixel row):

```
Initial:   [A] [B] [C] [D] [E]    (left=0, right=4)
Swap 0,4:  [E] [B] [C] [D] [A]    (left=1, right=3)
Swap 1,3:  [E] [D] [C] [B] [A]    (left=2, right=2)
Stop: left is not < right anymore
```

### Instructor Note:
- The first solution using comma operators in the for loop is more concise but can confuse beginners
- The while loop approach is easier to understand initially
- Strongly recommend walking through the swap algorithm with a simple example first
- Test with a sample image to verify correct output
- Have students trace through the loop manually before coding
- Pacing: This is where students start to struggle. Allow adequate time and be prepared to reteach the swap pattern
- After they finish, ask: "Why do we use a temp variable?" and "Why does left < right work?"

---

## Summary of All Solutions

Students should implement four filters total in helpers.c:

1. **grayscale()** — Convert to shades of gray (see Part 4)
2. **reflect()** — Mirror horizontally (see Part 5)
3. **blur()** — Smooth pixels with neighbors (not in this walkthrough; use box blur)
4. **edges()** — Detect edges using Sobel operator (not in this walkthrough; advanced)

For blur and edges, refer to the CS50 course materials.

---

## Teaching Tips

### Pacing Recommendations:
- **Part 1 (Scaffold):** 5 minutes of lecture
- **Part 2 (Struct Warm-Up):** 15-20 minutes hands-on
- **Part 3 (2D Array Warm-Up):** 10-15 minutes hands-on
- **Part 4 (Grayscale):** 20-25 minutes hands-on
- **Part 5 (Reflect):** 20-25 minutes hands-on
- **Total:** 70-90 minutes (fits in one class period with some spillover)

### Common Student Issues:

1. **Loop Bounds Confusion:** Students often use wrong dimensions for nested loops. Solution: Have them print "Starting row: [row], width: [width]" before the inner loop to verify.

2. **Pointer vs. Array Notation:** Students confuse image[row][col] with other notations. Reinforce that RGBTRIPLE image[height][width] is a 2D array, not a pointer.

3. **Struct Member Access:** Some students try image->rgbtRed instead of image[row][col].rgbtRed. Review the difference between pointers and arrays.

4. **Compilation Errors:** If students forget `-lm` flag, the math.h round() function won't link. Common error: "undefined reference to round"

5. **Understanding BMP Format:** Not all students understand why order is BGR. You can explain it's a historical quirk of Windows BMP format, but for grayscale it's irrelevant.

### Discussion Questions:

- "Why must we cast to float when calculating the average?"
- "What would happen if we used integer division instead of float division?"
- "Why do we use a temporary variable in the swap? What goes wrong without it?"
- "How would the reflect filter change if the image were rotated 90 degrees?"
- "Can you optimize reflect to use less memory?"

### Assessment:

Check these criteria when reviewing student helpers.c:

- [ ] All four filters implemented (grayscale, reflect, blur, edges)
- [ ] Correct algorithm logic for each filter
- [ ] Proper use of nested loops with correct bounds
- [ ] Correct struct member access syntax
- [ ] Code compiles without warnings with `-lm` flag
- [ ] Code is properly commented
- [ ] Variable names follow camelCase convention
- [ ] Consistent indentation (4 spaces)
- [ ] No hardcoded values (height/width passed as parameters)

---

## Answer Key for Warm-Ups

### Part 2 Expected Output:
```
Name: Alice, Grade: 11, GPA: 3.85 (Honor Roll)
Name: Bob, Grade: 10, GPA: 3.20
Name: Charlie, Grade: 12, GPA: 3.95 (Honor Roll)
```

### Part 3 Expected Output:
```
Grid:
1 2 3
4 5 6
7 8 9
Sum: 45
```

### Part 4 Expected Behavior:
- Any color image should become grayscale (all colors appear as shades of gray)
- No artifacts, no crashes, clean processing of all pixels
- Output file should be same dimensions as input

### Part 5 Expected Behavior:
- Image is flipped horizontally (left-right mirror)
- All pixels shifted correctly
- No damage to image or color data
- Output file should be same dimensions as input

---

## References

- **CS50 Filter Project:** https://cs50.harvard.edu/
- **GCC Documentation:** https://gcc.gnu.org/
- **C Struct Documentation:** https://en.cppreference.com/w/c/language/struct
- **BMP File Format:** Wikipedia article on BMP file format

---

## Version Information

- **Date Created:** 2026-02-20
- **Course Level:** High School CTE (Career Technical Education)
- **Prerequisite Knowledge:** Basic C syntax, loops, functions
- **Typical Grade Level:** 11-12

---

*End of Instructor Solutions Document*
