# prog02 Session B — Solutions & Instructor Notes
## Blur and Edge Detection Filters

---

## SOLUTION B1: Blur Filter

### Complete Implementation

```c
#include <math.h>
#include "helpers.h"

// Apply box blur to image
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
                        // Add neighbor's colors to the sum (reading from copy)
                        sumRed += copy[ni][nj].rgbtRed;
                        sumGreen += copy[ni][nj].rgbtGreen;
                        sumBlue += copy[ni][nj].rgbtBlue;

                        // Increment the neighbor count
                        count++;
                    }
                }
            }

            // Calculate the average for each color channel
            image[i][j].rgbtRed = (BYTE) round(sumRed / (float) count);
            image[i][j].rgbtGreen = (BYTE) round(sumGreen / (float) count);
            image[i][j].rgbtBlue = (BYTE) round(sumBlue / (float) count);
        }
    }
}
```

### Instructor Notes

**Key Teaching Points:**

1. **Why Copy?** The copy is essential because:
   - We must read original pixel values for the entire pass
   - If we read and write to the same array, we'd use already-blurred values
   - Example: processing pixel (1,1) uses (0,0), (0,1), (0,2), (1,0), (1,1), (1,2), (2,0), (2,1), (2,2). If (0,0) was already blurred, the result would be wrong.

2. **Boundary Handling**: The `if` condition automatically skips out-of-bounds neighbors. Corner pixels end up averaging 4 neighbors (including themselves), edge pixels average 6, and interior pixels average 9.

3. **Floating-Point Division**: Use `(float) count` to ensure we don't lose precision. Integer division would truncate.

4. **Casting to BYTE**: The `round()` function returns a double; cast to BYTE when assigning.

5. **Neighbor Count Varies**:
   - Corner (0, 0): 4 neighbors (0,0), (0,1), (1,0), (1,1)
   - Edge (0, 1): 6 neighbors (0,0), (0,1), (0,2), (1,0), (1,1), (1,2)
   - Interior (1, 1): 9 neighbors (all 3×3)

**Test Case Walkthrough:**
Image:
```
100  150  200
120  150  180
100  150  200
```

Blur the center pixel (1,1):
- Neighbors: all 9 pixels
- Sum: 100+150+200+120+150+180+100+150+200 = 1330
- Count: 9
- Average: 1330 / 9 ≈ 147.78, rounds to 148
- Result: image[1][1] = (148, 148, 148)

**Common Student Mistakes:**
- Forgetting to create a copy (reads blurred values)
- Reading from `image` instead of `copy` (same problem)
- Not casting to float before division (integer truncation)
- Not casting back to BYTE (type mismatch)
- Using `count` without incrementing it (division by 0 or wrong value)
- Off-by-one errors in boundary checks

---

## SOLUTION B2: Edge Detection — Sobel Operator

### Complete Implementation

```c
#include <math.h>
#include "helpers.h"

// Detect edges using Sobel operator
void edges(int height, int width, RGBTRIPLE image[height][width])
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
                    if (ni >= 0 && ni < height && nj >= 0 && nj < width)
                    {
                        // Convert di, dj (-1,0,1) to kernel indices (0,1,2)
                        int kernelI = di + 1;
                        int kernelJ = dj + 1;

                        int gxWeight = gxKernel[kernelI][kernelJ];
                        int gyWeight = gyKernel[kernelI][kernelJ];

                        // Get the neighbor pixel's color values
                        BYTE neighborRed = copy[ni][nj].rgbtRed;
                        BYTE neighborGreen = copy[ni][nj].rgbtGreen;
                        BYTE neighborBlue = copy[ni][nj].rgbtBlue;

                        // Accumulate weighted sums for each color
                        gxRed += gxWeight * neighborRed;
                        gyRed += gyWeight * neighborRed;

                        gxGreen += gxWeight * neighborGreen;
                        gyGreen += gyWeight * neighborGreen;

                        gxBlue += gxWeight * neighborBlue;
                        gyBlue += gyWeight * neighborBlue;
                    }
                }
            }

            // Calculate magnitude for each channel: sqrt(Gx^2 + Gy^2)
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

### Instructor Notes

**Key Teaching Points:**

1. **Kernel Index Conversion**: This is the trickiest part for students.
   - `di` and `dj` range from -1 to 1 (3 values)
   - Kernel arrays are indexed 0 to 2 (3 values)
   - Convert with: `kernelI = di + 1` and `kernelJ = dj + 1`
   - Example: When processing the upper-left neighbor, di=-1, dj=-1 → kernelI=0, kernelJ=0 ✓

2. **What the Kernels Detect**:
   - **Gx**: Vertical edges (left-right transitions)
   - **Gy**: Horizontal edges (top-bottom transitions)
   - The combination detects edges in all directions

3. **Magnitude Formula**: `sqrt(Gx^2 + Gy^2)` gives the total edge strength. This is the standard Euclidean norm.

4. **Capping at 255**: Magnitude can exceed 255 (e.g., sqrt(200^2 + 200^2) ≈ 283). Cap it to fit in a BYTE.

5. **Separate Color Channels**: Computing edge magnitude separately for R, G, B produces colored edge effects. Some implementations convert to grayscale first, but this version keeps colors.

6. **Out-of-Bounds Handling**: Pixels on edges/corners have missing neighbors. Treating them as 0 (by skipping them) is standard. Alternative: replicate the edge pixel.

**Kernel Application Example:**
For pixel (1, 1) in a 3×3 image with all values = 100:

Gx application:
```
-1*100  0*100   1*100     -100     0    100
-2*100  0*100   2*100  =  -200     0    200
-1*100  0*100   1*100     -100     0    100
Sum = 0
```

Gy application:
```
-1*100 -2*100 -1*100     -100   -200  -100
 0*100  0*100  0*100   =    0      0     0
 1*100  2*100  1*100      100    200   100
Sum = 0
```

Magnitude = sqrt(0^2 + 0^2) = 0 (uniform image has no edges) ✓

**Common Student Mistakes:**
- Wrong kernel index: using di/dj directly instead of di+1/dj+1
- Forgetting to apply both kernels (Gx and Gy)
- Not casting magnitude to int before capping
- Using unsigned math (Gx/Gy can be negative, which doesn't work with unsigned ints)
- Forgetting the copy (same issue as blur)
- Integer overflow: avoid by using `int` for kernel values and sums

**Test Case:**
On an image with a sharp vertical edge (black-to-white transition):
- Left of edge: high Gx values (horizontal gradient)
- Right of edge: high Gx values (horizontal gradient)
- Result: white line where edge is detected

---

## Performance Comparison

| Operation | Time Complexity | Space Complexity |
|-----------|-----------------|------------------|
| Grayscale | O(height × width) | O(1) |
| Reflect | O(height × width) | O(1) |
| Blur | O(height × width × 9) | O(height × width) for copy |
| Edges | O(height × width × 9) | O(height × width) for copy |

The 9-pixel neighborhood lookup is done for every pixel, making blur and edges 9× slower than grayscale or reflect.

---

## Assessment Rubric

### Blur (10 points total)
- **Image copy** (2 pts): Creates and populates copy correctly
- **Neighborhood loop** (2 pts): Correctly iterates 3×3 area with boundary checking
- **Accumulation** (2 pts): Sums all in-bounds neighbors correctly
- **Averaging** (2 pts): Divides by count correctly, rounds properly
- **No compilation errors** (2 pts): Code compiles cleanly

### Edge Detection (15 points total — stretch challenge)
- **Image copy** (1 pt): Creates copy correctly
- **Kernels defined** (2 pts): Gx and Gy kernels are correct
- **Kernel application** (3 pts): Applies kernels to all neighbors correctly
- **Index conversion** (2 pts): Converts di/dj to kernel indices correctly
- **Magnitude calculation** (3 pts): Computes sqrt(Gx^2 + Gy^2) correctly
- **Capping and type casting** (2 pts): Caps at 255, casts to BYTE
- **No compilation errors** (2 pts): Code compiles cleanly

---

## Extensions & Challenges

1. **Gaussian Blur**: Replace box blur kernel with Gaussian weights
   ```c
   int gaussianKernel[3][3] = {
       { 1,  2,  1 },
       { 2,  4,  2 },
       { 1,  2,  1 }
   };
   // Divide by sum of weights (16) instead of count
   ```

2. **Sharpen Filter**: Amplifies edges by subtracting the blurred version
   ```c
   int sharpenKernel[3][3] = {
       { -1, -1, -1 },
       { -1,  9, -1 },
       { -1, -1, -1 }
   };
   ```

3. **Laplacian Edge Detection**: Simpler edge detector
   ```c
   int laplacianKernel[3][3] = {
       {  0, -1,  0 },
       { -1,  4, -1 },
       {  0, -1,  0 }
   };
   ```

4. **Prewitt Operator**: Similar to Sobel but with equal weights
   ```c
   int prewittGx[3][3] = {
       { -1,  0,  1 },
       { -1,  0,  1 },
       { -1,  0,  1 }
   };
   ```

5. **Custom Kernel**: Let students define their own 3×3 kernel and see the results

6. **Separable Kernels**: Optimize by applying 1D kernels horizontally then vertically (reduces from O(9) to O(6) per pixel)

---

## Debugging Walkthroughs

### Blur Debugging Session
```c
// Add to blur() for debugging center pixel
if (i == 1 && j == 1)
{
    printf("Center pixel blur:\n");
    printf("sumRed=%d, count=%d, avg=%d\n", sumRed, count, sumRed/count);
}
```

### Edge Detection Debugging Session
```c
// Add to edges() for debugging corner pixel
if (i == 0 && j == 0)
{
    printf("Corner pixel edges (0,0):\n");
    printf("gxRed=%d, gyRed=%d, mag=%d\n", gxRed, gyRed, magRed);
    printf("Kernel indices: i+1=%d, j+1=%d\n", i+1, j+1);
}
```

---

## Real-World Applications

- **Medical Imaging**: Detect tumors or abnormalities using edge detection
- **Autonomous Vehicles**: Lane detection using edge detection on road images
- **Photo Editing**: Blur (bokeh effect), sharpen (unsharp mask)
- **Document Scanning**: Detect text edges for OCR preprocessing
- **Geology/Satellite**: Edge detection to identify geographic features
