# prog02 Session A — Grayscale and Reflect
## Image Filters & Structs (~2 hours)

### Learning Objectives
- Work with C structs (RGBTRIPLE)
- Manipulate 2D arrays of structs
- Understand pixel representation in digital images
- Implement basic image processing algorithms

---

## Background: The BMP File Format & RGBTRIPLE

A **BMP (Bitmap)** image file stores pixel data as a grid of colors. Each pixel is represented by three values:
- **R** (Red): 0–255
- **G** (Green): 0–255
- **B** (Blue): 0–255

In C, we represent a single pixel using this struct:

```c
// In bmp.h
typedef struct
{
    BYTE rgbtBlue;
    BYTE rgbtGreen;
    BYTE rgbtRed;
} RGBTRIPLE;
```

Note: The order is **BGR**, not RGB, due to how BMP files store data!

An image is a **2D array** of RGBTRIPLE structs:

```c
RGBTRIPLE image[height][width];
```

To access a pixel at row `i`, column `j`, use: `image[i][j]`
To access the red channel: `image[i][j].rgbtRed`

---

## Helper Header Files

### bmp.h
```c
#include <stdint.h>

// Aliases for convenience
typedef uint8_t BYTE;
typedef uint32_t DWORD;
typedef int32_t LONG;

// BMP file header (14 bytes)
typedef struct
{
    BYTE bfType[2];
    DWORD bfSize;
    WORD bfReserved1;
    WORD bfReserved2;
    DWORD bfOffBits;
} BITMAPFILEHEADER;

// BMP info header (40 bytes)
typedef struct
{
    DWORD biSize;
    LONG biWidth;
    LONG biHeight;
    WORD biPlanes;
    WORD biBitCount;
    DWORD biCompression;
    DWORD biSizeImage;
    LONG biXPelsPerMeter;
    LONG biYPelsPerMeter;
    DWORD biClrUsed;
    DWORD biClrImportant;
} BITMAPINFOHEADER;

// Pixel struct (3 bytes per pixel)
typedef struct
{
    BYTE rgbtBlue;
    BYTE rgbtGreen;
    BYTE rgbtRed;
} RGBTRIPLE;
```

### helpers.h
```c
#include "bmp.h"

// Image processing functions
void grayscale(int height, int width, RGBTRIPLE image[height][width]);
void reflect(int height, int width, RGBTRIPLE image[height][width]);
```

---

## TASK A1: Grayscale Filter

### What is Grayscale?
Convert a color image to shades of gray by making each pixel's R, G, and B values **equal**.

### Algorithm
For each pixel in the image:
1. Calculate the **average** of the red, green, and blue values
2. **Round** the average to the nearest integer (use `round()`)
3. Set all three color channels (R, G, B) to this average value

### Why Average?
Averaging the three channels gives equal weight to each color, producing a neutral gray. This is the simplest grayscale conversion.

### Function Signature
```c
void grayscale(int height, int width, RGBTRIPLE image[height][width])
```

### Task
Implement the `grayscale()` function. Fill in the blanks marked `// YOUR CODE HERE`.

```c
// Convert image to grayscale
void grayscale(int height, int width, RGBTRIPLE image[height][width])
{
    // Loop through each row
    for (int i = 0; i < height; i++)
    {
        // Loop through each column
        for (int j = 0; j < width; j++)
        {
            // Get the current pixel
            RGBTRIPLE pixel = image[i][j];

            // Calculate the average of R, G, B
            // Hint: Use (int) cast or round() function
            int gray = // YOUR CODE HERE

            // Set R, G, B to the gray value
            image[i][j].rgbtRed = // YOUR CODE HERE
            image[i][j].rgbtGreen = // YOUR CODE HERE
            image[i][j].rgbtBlue = // YOUR CODE HERE
        }
    }
}
```

### Hints
- Use `round()` to round the average to the nearest integer
- Remember to `#include <math.h>` for the `round()` function
- All three channels must be set to the **same** value

---

## TASK A2: Reflect Filter

### What is Reflect?
Mirror the image **horizontally** — flip it left-to-right.

### Algorithm
For each row of pixels:
1. Swap the leftmost pixel with the rightmost pixel
2. Swap the second-leftmost with the second-rightmost
3. Continue until you reach the middle
4. The middle column (if odd width) stays in place

### Why Use a Temporary Variable?
When swapping two values, you need a temporary variable to hold one value while you move the other.

```c
// Example: swap two ints
int temp = a;
a = b;
b = temp;
```

For pixels, use a temp **RGBTRIPLE**:

```c
RGBTRIPLE temp = image[i][left];
image[i][left] = image[i][right];
image[i][right] = temp;
```

### Function Signature
```c
void reflect(int height, int width, RGBTRIPLE image[height][width])
```

### Task
Implement the `reflect()` function. Fill in the blanks marked `// YOUR CODE HERE`.

```c
// Reflect image horizontally
void reflect(int height, int width, RGBTRIPLE image[height][width])
{
    // Loop through each row
    for (int i = 0; i < height; i++)
    {
        // Loop from left to middle
        for (int j = 0; j < width / 2; j++)
        {
            // Calculate the mirror position from the right
            int mirror = width - 1 - j;

            // Create a temporary RGBTRIPLE to hold one pixel
            RGBTRIPLE temp = // YOUR CODE HERE

            // Swap: move left pixel to right position
            image[i][mirror] = // YOUR CODE HERE

            // Swap: move right pixel to left position
            image[i][j] = // YOUR CODE HERE
        }
    }
}
```

### Hints
- The mirror of pixel at index `j` is at index `width - 1 - j`
- Only loop from `0` to `width / 2` to avoid swapping twice
- Use a temporary RGBTRIPLE struct to hold one pixel during the swap

---

## Testing Your Code

Here's a simple test program to verify your functions work correctly on a 3×3 test image:

```c
#include <stdio.h>
#include "helpers.h"

int main(void)
{
    // Create a small 3x3 test image
    RGBTRIPLE testImage[3][3] = {
        {
            {100, 50, 200},   // Row 0: pixel (0,0) BGR
            {150, 100, 50},   // pixel (0,1)
            {200, 200, 100}   // pixel (0,2)
        },
        {
            {50, 150, 100},   // Row 1: pixel (1,0)
            {100, 100, 100},  // pixel (1,1)
            {200, 50, 150}    // pixel (1,2)
        },
        {
            {75, 75, 75},     // Row 2: pixel (2,0)
            {125, 125, 125},  // pixel (2,1)
            {200, 100, 50}    // pixel (2,2)
        }
    };

    int height = 3;
    int width = 3;

    printf("Original pixel (0,0): R=%d G=%d B=%d\n",
           testImage[0][0].rgbtRed,
           testImage[0][0].rgbtGreen,
           testImage[0][0].rgbtBlue);

    // Test grayscale
    grayscale(height, width, testImage);
    printf("After grayscale (0,0): R=%d G=%d B=%d\n",
           testImage[0][0].rgbtRed,
           testImage[0][0].rgbtGreen,
           testImage[0][0].rgbtBlue);

    // Reset image
    testImage[0][0].rgbtRed = 200;
    testImage[0][0].rgbtGreen = 50;
    testImage[0][0].rgbtBlue = 100;

    // Test reflect
    printf("\nBefore reflect (0,0): R=%d G=%d B=%d\n",
           testImage[0][0].rgbtRed,
           testImage[0][0].rgbtGreen,
           testImage[0][0].rgbtBlue);
    printf("Before reflect (0,2): R=%d G=%d B=%d\n",
           testImage[0][2].rgbtRed,
           testImage[0][2].rgbtGreen,
           testImage[0][2].rgbtBlue);

    reflect(height, width, testImage);

    printf("After reflect (0,0): R=%d G=%d B=%d\n",
           testImage[0][0].rgbtRed,
           testImage[0][0].rgbtGreen,
           testImage[0][0].rgbtBlue);
    printf("After reflect (0,2): R=%d G=%d B=%d\n",
           testImage[0][2].rgbtRed,
           testImage[0][2].rgbtGreen,
           testImage[0][2].rgbtBlue);

    return 0;
}
```

### Expected Output
After grayscale: all three channels should be equal (the average, rounded)
After reflect: pixel (0,0) and (0,2) should swap, as should (1,0) and (1,2), etc.

---

## Checklist
- [ ] Grayscale: loops through all pixels
- [ ] Grayscale: calculates average correctly and rounds
- [ ] Grayscale: sets R, G, B to the same value
- [ ] Reflect: swaps left and right pixels correctly
- [ ] Reflect: uses temporary RGBTRIPLE for swap
- [ ] Reflect: only loops to width/2 to avoid double-swap
- [ ] Test code compiles and runs without errors
- [ ] Output makes sense (grayscale pixels have equal R,G,B; reflect swaps pixels)
