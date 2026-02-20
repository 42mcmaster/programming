# Lesson 02: Structs & Image Processing
## Study Guide
Medina County Career Center | Guest Instructor: Jared Henderson

---

## Vocabulary

1. **Struct** - A composite data type that groups multiple members (variables) of different or same types under one name.

2. **Member/Field** - A variable inside a struct; accessed using dot notation.

3. **Dot Notation** - Syntax for accessing struct members: `variable.member`

4. **typedef** - Keyword that creates an alias for a data type, simplifying declarations.

5. **RGBTRIPLE** - A struct with three integer fields (red, green, blue) representing a single pixel color.

6. **BITMAPFILEHEADER** - A struct containing metadata about a BMP file (file size, header size, offset to pixel data).

7. **BITMAPINFOHEADER** - A struct containing image dimensions, color depth, and compression information.

8. **2D Array** - An array of arrays; data organized in rows and columns like a matrix or grid.

9. **Row-Major Order** - The standard layout in C where 2D array elements are stored row by row in memory.

10. **Nested Loop** - A loop inside another loop; used to traverse 2D arrays and multi-dimensional structures.

11. **Pixel** - A single point in a digital image; the smallest unit of an image.

12. **RGB** - Red, Green, Blue color model; each channel is an integer 0-255.

13. **Grayscale** - A color mode where all three RGB channels have the same value, producing shades of gray from black to white.

14. **Reflect** - An image filter that flips or mirrors an image.

15. **Blur** - An image filter that smooths an image by averaging neighboring pixel values.

16. **Box Filter** - A type of blur filter using a square grid (e.g., 3x3) of neighbors to compute an average.

17. **Kernel** - A small matrix (like 3x3) applied to each pixel to perform filtering or edge detection.

18. **Edge Detection** - An image processing technique that identifies boundaries between regions of different color or intensity.

19. **Sobel Operator** - A common edge detection filter using vertical and horizontal gradient kernels.

20. **BMP File Format** - A simple uncompressed image format with headers describing dimensions, color depth, and pixel data.

21. **Scaffold Code** - Pre-written template code provided to students; they complete the remaining functions.

22. **helpers.c** - The file where students implement filter functions in the CS50 Filter project.

---

## Quick Reference

### Struct Syntax

```c
typedef struct {
    int red;
    int green;
    int blue;
} RGBTRIPLE;

RGBTRIPLE pixel;
pixel.red = 255;
```

### Accessing Struct Members

```c
printf("%d\n", pixel.green);  // Read
pixel.blue = 100;              // Write
```

### 2D Array Declaration and Indexing

```c
int grid[5][5];           // 5x5 grid
grid[2][3] = 42;          // Row 2, Column 3
int value = grid[0][0];   // Access element
```

### Nested Loop Pattern for Image Traversal

```c
for (int i = 0; i < height; i++) {
    for (int j = 0; j < width; j++) {
        // Process image[i][j]
    }
}
```

### Grayscale Formula

```c
int avg = (r + g + b) / 3;
newPixel.red = newPixel.green = newPixel.blue = (int) round(avg);
```

### Box Blur Averaging Pattern

```c
int sumRed = 0, sumGreen = 0, sumBlue = 0;
int count = 0;

for (int di = -1; di <= 1; di++) {
    for (int dj = -1; dj <= 1; dj++) {
        int ni = i + di;
        int nj = j + dj;

        if (ni >= 0 && ni < height && nj >= 0 && nj < width) {
            sumRed   += image[ni][nj].red;
            sumGreen += image[ni][nj].green;
            sumBlue  += image[ni][nj].blue;
            count++;
        }
    }
}

newPixel.red   = (int) round((float) sumRed / count);
newPixel.green = (int) round((float) sumGreen / count);
newPixel.blue  = (int) round((float) sumBlue / count);
```

---

## ODE Competencies Addressed

| Competency | Topic |
|---|---|
| 5.2.1 | Demonstrates working knowledge of structured data types and arrays. |
| 5.2.3 | Creates programs that use algorithms to solve problems. |
| 5.3.8 | Understands concepts of binary image representation and manipulation. |
| 5.4.6 | Develops and debugs code to implement image processing filters. |
| 5.4.7 | Applies mathematical operations in programming contexts (averaging, rounding). |

---

## Key Concepts Summary

**Structs** allow you to bundle related data together. An RGBTRIPLE represents a pixel's color in one unit. Arrays of structs let you store many pixels efficiently.

**2D arrays** organize data in rows and columns, perfect for representing images. Nested loops traverse them systematically.

**Images are 2D arrays of structs.** Each cell contains an RGBTRIPLE. Filters transform pixels by applying math or logic across the grid.

**Boundary conditions matter.** When processing neighborhoods (like blur), edge pixels have fewer neighbors. Handle this explicitly.

**Debugging with printf** is your friend. Print pixel values, loop indices, and intermediate calculations to verify correctness.

---

## Study Tips

- Practice declaring and using structs with simple examples before working with images.
- Draw a 2D array on paper and trace through nested loops by hand.
- Start with grayscale (simple averaging) before attempting blur.
- Test your code on small images first.
- Use printf() liberally to inspect data and verify logic.
- Understand row-major order; it affects memory layout and loop traversal.
