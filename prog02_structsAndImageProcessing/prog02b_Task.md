# prog02 Session B — Blur and Edge Detection
## Advanced Image Filters (~2 hours)

### Learning Objectives
- Apply convolution kernels (blur and edge detection)
- Handle boundary cases in 2D array processing
- Understand image manipulation at the pixel level
- Implement the Sobel edge detection operator (stretch challenge)

---

## Background: Convolution and Kernels

**Convolution** is a mathematical operation that applies a small matrix (called a **kernel**) to each pixel and its neighbors.

### Box Blur Kernel
The simplest blur uses a 3×3 kernel where each value is 1/9:

```
[ 1/9  1/9  1/9 ]
[ 1/9  1/9  1/9 ]
[ 1/9  1/9  1/9 ]
```

For each pixel, calculate the average of it and its 8 neighbors (3×3 neighborhood).

### Sobel Edge Detection Kernels
Edge detection uses two kernels, Gx and Gy, to measure horizontal and vertical edges:

**Gx (horizontal edges):**
```
[ -1   0   1 ]
[ -2   0   2 ]
[ -1   0   1 ]
```

**Gy (vertical edges):**
```
[ -1  -2  -1 ]
[  0   0   0 ]
[  1   2   1 ]
```

Apply both kernels to compute the gradient magnitude: `sqrt(Gx^2 + Gy^2)`

---

## TASK B1: Blur Filter

### What is Blur?
Apply a **box blur** — each pixel becomes the average of itself and its 8 neighbors.

### Algorithm
For each pixel at (i, j):
1. Sum the values of all pixels in the 3×3 neighborhood centered at (i, j)
2. Handle **boundaries**: pixels on edges/corners have fewer neighbors
3. Divide by the count of neighbors (not always 9)
4. Round to the nearest integer
5. **IMPORTANT**: Write the result to a **copy** of the image; read from the original

### Why a Copy?
If you read and write to the same array, you'll read blurred values instead of original values. Example:
- Original: [10, 20, 30]
- If you blur pixel 1 using original[0]=10 and already-modified original[2], you get wrong results
- **Solution**: Read from original, write to a copy, then copy back

### Function Signature
```c
void blur(int height, int width, RGBTRIPLE image[height][width])
```

### Task
Implement the `blur()` function. Fill in the blanks marked `// YOUR CODE HERE`.

```c
// Blur image
void blur(int height, int width, RGBTRIPLE image[height][width])
{
    // Create a copy of the image to read from
    RGBTRIPLE copy[height][width];
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            copy[i][j] = image[i][j];
        }
    }

    // Loop through each pixel in the original image
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            // Variables to accumulate color values and count neighbors
            int sumRed = 0, sumGreen = 0, sumBlue = 0;
            int count = 0;

            // Loop through the 3x3 neighborhood
            for (int di = -1; di <= 1; di++)
            {
                for (int dj = -1; dj <= 1; dj++)
                {
                    // Calculate neighbor coordinates
                    int ni = i + di;
                    int nj = j + dj;

                    // Check if neighbor is within bounds
                    if (ni >= 0 && ni < height && nj >= 0 && nj < width)
                    {
                        // Add neighbor's colors to the sum
                        sumRed += // YOUR CODE HERE
                        sumGreen += // YOUR CODE HERE
                        sumBlue += // YOUR CODE HERE

                        // Increment the neighbor count
                        count++;  // YOUR CODE HERE (or just: count += 1;)
                    }
                }
            }

            // Calculate the average for each color channel
            image[i][j].rgbtRed = // YOUR CODE HERE (sum divided by count, rounded)
            image[i][j].rgbtGreen = // YOUR CODE HERE
            image[i][j].rgbtBlue = // YOUR CODE HERE
        }
    }
}
```

### Hints
1. **Boundary Checking**: The condition `ni >= 0 && ni < height && nj >= 0 && nj < width` ensures the neighbor is inside the image
2. **Access the Copy**: Read colors from `copy[ni][nj]`, not `image[ni][nj]`
3. **Averaging**: Divide sumRed by count, use `round()` to round to the nearest integer
4. **Loop Variables**: Use `di` and `dj` (delta i, delta j) to iterate through offsets (-1, 0, 1)

### Example: Corner Pixel (0, 0)
- A corner has only 4 neighbors (including itself)
- Neighbors: (0,0), (0,1), (1,0), (1,1)
- Average the 4 pixels, divide by 4

---

## TASK B2: Edge Detection — Sobel Operator (STRETCH CHALLENGE)

### What is Edge Detection?
Identify **boundaries** in an image where color changes sharply. The Sobel operator detects both horizontal (Gx) and vertical (Gy) edges.

### Algorithm
For each pixel at (i, j):

1. **Apply Gx kernel** — measure horizontal edge strength:
   ```
   Gx = (-1*pixel[i-1][j-1] + 0*pixel[i-1][j] + 1*pixel[i-1][j+1]
        -2*pixel[i][j-1]   + 0*pixel[i][j]   + 2*pixel[i][j+1]
        -1*pixel[i+1][j-1] + 0*pixel[i+1][j] + 1*pixel[i+1][j+1])
   ```

2. **Apply Gy kernel** — measure vertical edge strength:
   ```
   Gy = (-1*pixel[i-1][j-1] -2*pixel[i-1][j] -1*pixel[i-1][j+1]
        +0*pixel[i][j-1]   +0*pixel[i][j]   +0*pixel[i][j+1]
        +1*pixel[i+1][j-1] +2*pixel[i+1][j] +1*pixel[i+1][j+1])
   ```

3. **Compute magnitude**: `magnitude = sqrt(Gx^2 + Gy^2)`

4. **Cap at 255**: If magnitude > 255, set to 255 (BYTEs cannot exceed 255)

5. **Grayscale**: Set R, G, B to the magnitude value

### Function Signature
```c
void edges(int height, int width, RGBTRIPLE image[height][width])
```

### Task
Implement the `edges()` function. This is more complex, so heavy scaffolding is provided.

```c
// Detect edges in image using Sobel operator
void edges(int height, int width, RGBTRIPLE image[height][width])
{
    // Create a copy of the image
    RGBTRIPLE copy[height][width];
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            copy[i][j] = image[i][j];
        }
    }

    // Gx kernel (detects vertical edges / horizontal gradients)
    int gxKernel[3][3] = {
        { -1,  0,  1 },
        { -2,  0,  2 },
        { -1,  0,  1 }
    };

    // Gy kernel (detects horizontal edges / vertical gradients)
    int gyKernel[3][3] = {
        { -1, -2, -1 },
        {  0,  0,  0 },
        {  1,  2,  1 }
    };

    // Loop through each pixel
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            // Variables to accumulate Gx and Gy for each channel
            int gxRed = 0, gyRed = 0;
            int gxGreen = 0, gyGreen = 0;
            int gxBlue = 0, gyBlue = 0;

            // Apply kernels to the 3x3 neighborhood
            for (int di = -1; di <= 1; di++)
            {
                for (int dj = -1; dj <= 1; dj++)
                {
                    // Neighbor coordinates
                    int ni = i + di;
                    int nj = j + dj;

                    // Check bounds: treat out-of-bounds as 0
                    // (Alternatively: skip out-of-bounds pixels)
                    if (ni >= 0 && ni < height && nj >= 0 && nj < width)
                    {
                        // Get the kernel values (convert di, dj to kernel indices)
                        int kernelI = di + 1;  // converts -1,0,1 to 0,1,2
                        int kernelJ = dj + 1;

                        int gxWeight = gxKernel[kernelI][kernelJ];
                        int gyWeight = gyKernel[kernelI][kernelJ];

                        // Get the neighbor pixel's color values
                        BYTE neighborRed = copy[ni][nj].rgbtRed;
                        BYTE neighborGreen = copy[ni][nj].rgbtGreen;
                        BYTE neighborBlue = copy[ni][nj].rgbtBlue;

                        // Accumulate weighted sums for each color
                        gxRed += // YOUR CODE HERE (gxWeight * neighborRed)
                        gyRed += // YOUR CODE HERE (gyWeight * neighborRed)

                        gxGreen += // YOUR CODE HERE
                        gyGreen += // YOUR CODE HERE

                        gxBlue += // YOUR CODE HERE
                        gyBlue += // YOUR CODE HERE
                    }
                }
            }

            // Calculate magnitude for each channel: sqrt(Gx^2 + Gy^2)
            // Use <math.h> sqrt() function
            int magRed = (int) round(sqrt(gxRed * gxRed + gyRed * gyRed));
            int magGreen = (int) round(sqrt(gxGreen * gxGreen + gyGreen * gyGreen));
            int magBlue = (int) round(sqrt(gxBlue * gxBlue + gyBlue * gyBlue));

            // Cap values at 255 (BYTE max)
            magRed = magRed > 255 ? 255 : magRed;
            magGreen = magGreen > 255 ? 255 : magGreen;
            magBlue = magBlue > 255 ? 255 : magBlue;

            // Set the pixel to the edge magnitude
            image[i][j].rgbtRed = (BYTE) magRed;
            image[i][j].rgbtGreen = (BYTE) magGreen;
            image[i][j].rgbtBlue = (BYTE) magBlue;
        }
    }
}
```

### Hints
1. **Kernel Index Conversion**: The kernel is indexed 0–2, but di and dj are -1–1. Use `kernelI = di + 1` and `kernelJ = dj + 1` to convert.
2. **Out-of-Bounds Handling**: Pixels on edges have missing neighbors. The scaffold treats them as 0 (if not in bounds, skip). You could alternatively treat them as the edge pixel color.
3. **Magnitude Formula**: `sqrt(Gx^2 + Gy^2)` — use the `sqrt()` function from `<math.h>`
4. **Capping at 255**: Use a ternary operator: `value > 255 ? 255 : value`
5. **Type Casting**: The magnitude is an int; cast to BYTE when assigning to image

### Why Separate Channels?
Some image processing implementations compute a single grayscale value for edge magnitude. Here, we compute it separately for each channel, which can produce interesting colored edge effects.

---

## Testing Your Code

### Test Program for Blur

```c
#include <stdio.h>
#include "helpers.h"

int main(void)
{
    // Create a 3x3 test image
    RGBTRIPLE testImage[3][3] = {
        {
            {100, 100, 100},
            {150, 150, 150},
            {200, 200, 200}
        },
        {
            {120, 120, 120},
            {150, 150, 150},
            {180, 180, 180}
        },
        {
            {100, 100, 100},
            {150, 150, 150},
            {200, 200, 200}
        }
    };

    printf("Before blur - center pixel (1,1): R=%d\n", testImage[1][1].rgbtRed);
    blur(3, 3, testImage);
    printf("After blur - center pixel (1,1): R=%d\n", testImage[1][1].rgbtRed);
    printf("(Should be average of all 9 pixels)\n");

    return 0;
}
```

**Expected Output:**
Center pixel should be the average of all 9 pixels: (100+150+200+120+150+180+100+150+200)/9 ≈ 147

---

## Checklist — Session B

### Blur Implementation
- [ ] Creates a copy of the image before processing
- [ ] Reads from copy, writes to original
- [ ] Loops through all pixels
- [ ] Loops through 3×3 neighborhood with boundary checking
- [ ] Accumulates color values correctly
- [ ] Counts neighbors correctly
- [ ] Divides by count and rounds
- [ ] Compiles without errors

### Edge Detection Implementation (Stretch)
- [ ] Creates a copy of the image
- [ ] Defines Gx and Gy kernels correctly
- [ ] Loops through 3×3 neighborhood
- [ ] Applies kernels to each color channel
- [ ] Converts kernel indices (di, dj) to (kernelI, kernelJ) correctly
- [ ] Computes magnitude: sqrt(Gx^2 + Gy^2)
- [ ] Caps values at 255
- [ ] Sets all three channels to magnitude
- [ ] Compiles without errors

---

## Debugging Tips

### Blur
1. Print the center pixel before and after blur on a uniform image (should not change)
2. Add debug output showing the sum and count for one pixel
3. Verify the 3×3 loop is accessing the correct neighbors
4. Test with edge and corner pixels separately

### Edge Detection
1. Print Gx and Gy values for one pixel to verify kernel application
2. Check magnitude calculation: should be non-negative and ≤ 255 after capping
3. Test on a simple gradient image (intensity increases left-to-right)
4. Verify kernel indices: a pixel at (0,0) should use kernel indices (0,0) through (2,2)

---

## Challenge Extensions

1. **Gaussian Blur**: Use a different kernel with higher weights at center
   ```
   [ 1   2   1 ]
   [ 2   4   2 ] * (1/16)
   [ 1   2   1 ]
   ```

2. **Sharpen Filter**: Use negative center value to amplify edges
   ```
   [ -1  -1  -1 ]
   [ -1   9  -1 ]
   [ -1  -1  -1 ] * (1/1)
   ```

3. **Custom Kernel**: Let students define their own kernel and apply it

4. **Combine Filters**: Apply blur to the edges output to create interesting effects

5. **Performance Optimization**: How can you reduce redundant calculations? (Separable kernels, etc.)
