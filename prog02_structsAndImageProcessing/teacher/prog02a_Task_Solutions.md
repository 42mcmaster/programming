# prog02 Session A — Solutions & Instructor Notes
## Grayscale and Reflect Filters

---

## SOLUTION A1: Grayscale Filter

### Complete Implementation

```c
#include <math.h>
#include "helpers.h"

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

            // Calculate the average of R, G, B and round to nearest integer
            int gray = round((pixel.rgbtRed + pixel.rgbtGreen + pixel.rgbtBlue) / 3.0);

            // Set R, G, B to the gray value
            image[i][j].rgbtRed = gray;
            image[i][j].rgbtGreen = gray;
            image[i][j].rgbtBlue = gray;
        }
    }
}
```

### Instructor Notes

**Key Teaching Points:**

1. **Division by 3.0 (not 3)**: Using 3.0 ensures floating-point division, preserving decimals. If students use integer division (3), they lose precision and get wrong rounding.
   - Correct: `(100 + 150 + 200) / 3.0 = 150.0`
   - Wrong: `(100 + 150 + 200) / 3 = 150` (happens to match here, but test with values like 100, 100, 101)

2. **round() vs int cast**: The `round()` function properly rounds to the nearest integer (0.5 rounds up). A simple cast `(int)` truncates.
   - Example: average is 150.7
   - `round(150.7)` = 151
   - `(int)150.7` = 150

3. **All three channels must be equal**: This is the definition of grayscale—no color information.

4. **Common Student Mistakes:**
   - Forgetting to cast to 3.0 (integer division bug)
   - Only modifying one color channel
   - Forgetting `#include <math.h>`
   - Using the average as only one channel: `image[i][j].rgbtRed = (r + g + b) / 3;` then not setting the others

**Test Cases:**
- Pixel (255, 0, 0) red → grayscale: (85, 85, 85)
- Pixel (100, 100, 100) already gray → grayscale: (100, 100, 100)
- Pixel (100, 150, 200) mixed → grayscale: (150, 150, 150) after rounding (100+150+200)/3 = 150

---

## SOLUTION A2: Reflect Filter

### Complete Implementation

```c
#include "helpers.h"

// Reflect image horizontally
void reflect(int height, int width, RGBTRIPLE image[height][width])
{
    // Loop through each row
    for (int i = 0; i < height; i++)
    {
        // Loop from left to middle (only need to swap half the row)
        for (int j = 0; j < width / 2; j++)
        {
            // Calculate the mirror position from the right
            // For width=5: j=0 mirrors to index 4 (5-1-0=4), j=1 mirrors to 3, j=2 is middle
            int mirror = width - 1 - j;

            // Create a temporary RGBTRIPLE to hold the left pixel
            RGBTRIPLE temp = image[i][j];

            // Move right pixel to left position
            image[i][j] = image[i][mirror];

            // Move left pixel (stored in temp) to right position
            image[i][mirror] = temp;
        }
    }
}
```

### Instructor Notes

**Key Teaching Points:**

1. **Mirror Index Formula**: For a pixel at index `j`, its mirror is at `width - 1 - j`.
   - Example: width = 5 (indices 0, 1, 2, 3, 4)
   - j=0 mirrors to 4 (5-1-0=4) ✓
   - j=1 mirrors to 3 (5-1-1=3) ✓
   - j=2 mirrors to 2 (5-1-2=2) — middle pixel (stays same) ✓
   - j=3 would mirror to 1 (5-1-3=1) — but we don't process j=3 because loop stops at width/2=2

2. **Why Only Loop to width/2**: If we looped through all columns, we'd swap each pixel twice and end up back where we started.
   - Loop to width/2 = 2, so j={0, 1}
   - j=0: swap pixels at indices 0 and 4
   - j=1: swap pixels at indices 1 and 3
   - j=2 (middle) doesn't get swapped

3. **Temporary Variable is Essential**: In C (and most languages), you can't swap two variables without a temporary. This is a fundamental programming concept.
   ```c
   // WRONG: loses data
   image[i][j] = image[i][mirror];           // left becomes right
   image[i][mirror] = image[i][j];           // right tries to become left, but left is now a copy of right!

   // CORRECT: use temp
   RGBTRIPLE temp = image[i][j];             // save left
   image[i][j] = image[i][mirror];           // left becomes right
   image[i][mirror] = temp;                  // right becomes original left
   ```

4. **RGBTRIPLE is a Struct**: Students must understand that assigning a struct copies all three fields (r, g, b). This is different from pointers or arrays.

**Common Student Mistakes:**
- Off-by-one errors in the mirror formula
- Looping to `width` instead of `width / 2`, causing double-swaps
- Forgetting the temporary variable
- Not initializing the temp variable before use
- Using `width - j` instead of `width - 1 - j` (gets the wrong mirror)

**Test Cases:**
- 3-pixel row: indices (0, 1, 2)
  - Original: [A, B, C]
  - After reflect: [C, B, A]
  - Only swap j=0 (mirror to 2), j=1 is middle so width/2=1.5 truncates to 1

- 4-pixel row: indices (0, 1, 2, 3)
  - Original: [A, B, C, D]
  - After reflect: [D, C, B, A]
  - Swap j=0 (to 3) and j=1 (to 2), width/2=2

- 5-pixel row: indices (0, 1, 2, 3, 4)
  - Original: [A, B, C, D, E]
  - After reflect: [E, D, C, B, A]
  - Swap j=0 (to 4) and j=1 (to 3), j=2 is middle, width/2=2.5 truncates to 2

---

## Sample Test Output

Running the test program with the provided test image:

```
Original pixel (0,0): R=200 G=50 B=100
After grayscale (0,0): R=117 G=117 B=117

Before reflect (0,0): R=200 G=50 B=100
Before reflect (0,2): R=100 G=200 B=200
After reflect (0,0): R=100 G=200 B=200
After reflect (0,2): R=200 G=50 B=100
```

**Verification:**
- Grayscale: (200 + 50 + 100) / 3.0 = 350 / 3.0 = 116.67, rounds to 117 ✓
- Reflect: (0,0) and (0,2) swapped correctly ✓

---

## Debugging Tips for Students

### Grayscale Debugging
1. Print the original and grayscale values of a pixel
2. Check if division by 3 is happening with floating-point (should use 3.0)
3. Verify the rounded value is correct manually

### Reflect Debugging
1. Print pixel indices before and after to verify mirror formula
2. Add assertions: after reflect, image[i][j] should equal original image[i][mirror]
3. Test with odd and even widths
4. Use a small image (3×3 or 4×4) for manual verification

---

## Assessment Rubric

### Grayscale (10 points total)
- **Correct algorithm** (5 pts): Calculates average of R, G, B correctly
- **Proper rounding** (2 pts): Uses round() or equivalent; avoids integer division truncation
- **Sets all channels** (2 pts): R, G, B all set to the same value
- **No compilation errors** (1 pt): Code compiles cleanly

### Reflect (10 points total)
- **Correct loop structure** (3 pts): Loops through half the width, all rows
- **Correct mirror formula** (3 pts): Mirror index is width - 1 - j
- **Proper swapping** (3 pts): Uses temporary variable, swaps both pixels correctly
- **No compilation errors** (1 pt): Code compiles cleanly

---

## Extensions & Challenges

1. **Optimize Grayscale**: Use weighted average instead of simple average (human eye perceives green brighter): `0.299*R + 0.587*G + 0.114*B`

2. **Combine Filters**: Apply grayscale AFTER reflect (or vice versa) to show filters can chain

3. **Inverse Reflect**: Implement vertical reflect (flip top-to-bottom) as a bonus

4. **Performance**: Have students think about cache efficiency—accessing image data in row-major order vs column-major

5. **Bounds Checking**: What would happen if height or width is 0? Add error handling.
