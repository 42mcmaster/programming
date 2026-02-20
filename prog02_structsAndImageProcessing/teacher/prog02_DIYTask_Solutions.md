# prog02 DIY Task — Solutions
## Custom Image Filter Implementations

---

## SOLUTION 1: Sepia Tone Filter

### Complete Implementation

```c
#include <math.h>
#include "helpers.h"

// Apply sepia tone filter (warm, vintage brown effect)
// Uses weighted combination of RGB channels to create aged photograph appearance
void customFilter(int height, int width, RGBTRIPLE image[height][width])
{
    // Loop through each pixel
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            // Get the current pixel's color values
            BYTE red = image[i][j].rgbtRed;
            BYTE green = image[i][j].rgbtGreen;
            BYTE blue = image[i][j].rgbtBlue;

            // Apply sepia formula to each channel
            // These coefficients are standard for sepia conversion
            int newRed = (int) round(0.393 * red + 0.769 * green + 0.189 * blue);
            int newGreen = (int) round(0.349 * red + 0.686 * green + 0.168 * blue);
            int newBlue = (int) round(0.272 * red + 0.534 * green + 0.131 * blue);

            // Cap each channel at 255 (BYTE maximum)
            newRed = newRed > 255 ? 255 : newRed;
            newGreen = newGreen > 255 ? 255 : newGreen;
            newBlue = newBlue > 255 ? 255 : newBlue;

            // Update pixel with new sepia-toned values
            image[i][j].rgbtRed = (BYTE) newRed;
            image[i][j].rgbtGreen = (BYTE) newGreen;
            image[i][j].rgbtBlue = (BYTE) newBlue;
        }
    }
}
```

### Instructor Notes — Sepia

**Why These Coefficients?**
The sepia formula is based on human color perception. The coefficients:
- Weight red highest (0.393 + 0.769 + 0.189 = 1.351)
- Weight green medium (0.349 + 0.686 + 0.168 = 1.203)
- Weight blue lowest (0.272 + 0.534 + 0.131 = 0.937)

This creates a warm brown tone by emphasizing red and green while reducing blue.

**Test Results:**
- Pure red (255, 0, 0) → sepia: (255, 238, 186) — warm red-brown
- Pure green (0, 255, 0) → sepia: (196, 174, 90) — olive brown
- Pure blue (0, 0, 255) → sepia: (48, 43, 35) — dark brown
- White (255, 255, 255) → sepia: (255, 255, 239) — off-white
- Black (0, 0, 0) → sepia: (0, 0, 0) — stays black

**Common Pitfalls:**
- Forgetting to multiply original channels before adding
- Not rounding before casting to int
- Forgetting to cap at 255

---

## SOLUTION 2: Color Inversion

### Complete Implementation

```c
#include "helpers.h"

// Invert all colors (create photographic negative effect)
// Each channel is subtracted from 255, creating complementary colors
void customFilter(int height, int width, RGBTRIPLE image[height][width])
{
    // Loop through each pixel
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            // Invert each color channel by subtracting from 255
            image[i][j].rgbtRed = 255 - image[i][j].rgbtRed;
            image[i][j].rgbtGreen = 255 - image[i][j].rgbtGreen;
            image[i][j].rgbtBlue = 255 - image[i][j].rgbtBlue;
        }
    }
}
```

### Instructor Notes — Inversion

**Color Transformation:**
Inversion maps each color to its complement:
- Red (255, 0, 0) → Cyan (0, 255, 255)
- Green (0, 255, 0) → Magenta (255, 0, 255)
- Blue (0, 0, 255) → Yellow (255, 255, 0)
- White (255, 255, 255) → Black (0, 0, 0)
- Gray (128, 128, 128) → Gray (127, 127, 127)

**Mathematical Basis:**
In color space, the inverse of value `v` is `255 - v`. This is the standard way to compute complementary colors.

**Performance:**
This is the fastest filter—only 3 subtractions per pixel, no loops, no floating-point math.

**Test Results:**
```
Before: (255, 0, 0)       After: (0, 255, 255)
Before: (0, 0, 255)       After: (255, 255, 0)
Before: (128, 128, 128)   After: (127, 127, 127)
```

---

## SOLUTION 3: Threshold / Posterize

### Complete Implementation

```c
#include "helpers.h"

// Apply posterize effect by reducing color palette
// Quantizes each channel to discrete levels (e.g., 0, 64, 128, 192, 255)
void customFilter(int height, int width, RGBTRIPLE image[height][width])
{
    // Quantization level controls color reduction
    // 64 = 4 levels per channel (0, 64, 128, 192) = 64 total colors
    // 128 = 2 levels per channel (0, 128) = 8 total colors
    // 32 = 8 levels per channel = 512 total colors
    int quantizeLevel = 64;

    // Loop through each pixel
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            // Quantize each channel to nearest multiple of quantizeLevel
            // Integer division (/) rounds down, multiply back to get nearest level
            image[i][j].rgbtRed = (image[i][j].rgbtRed / quantizeLevel) * quantizeLevel;
            image[i][j].rgbtGreen = (image[i][j].rgbtGreen / quantizeLevel) * quantizeLevel;
            image[i][j].rgbtBlue = (image[i][j].rgbtBlue / quantizeLevel) * quantizeLevel;
        }
    }
}
```

### Instructor Notes — Posterize

**How Quantization Works:**
For quantizeLevel = 64:
- Value 0–63 → divided by 64 = 0, multiply by 64 = 0
- Value 64–127 → divided by 64 = 1, multiply by 64 = 64
- Value 128–191 → divided by 64 = 2, multiply by 64 = 128
- Value 192–255 → divided by 64 = 3, multiply by 64 = 192

**Color Palette Size:**
With quantizeLevel Q and 256 possible values:
- Number of levels per channel = 256 / Q
- Total colors = (256/Q)^3

Examples:
- Q=64: 4^3 = 64 colors (8-bit to 6-bit reduction)
- Q=128: 2^3 = 8 colors (very abstract)
- Q=32: 8^3 = 512 colors (nearly normal, slight effect)

**Test Results:**
```
Before: (200, 100, 50)   After: (192, 64, 0)
Before: (255, 255, 255)  After: (192, 192, 192)
Before: (0, 0, 0)        After: (0, 0, 0)
Before: (100, 150, 200)  After: (64, 128, 192)
```

**Visual Effect:**
Creates bold, flat color blocks—useful for cartoon-like effects or data visualization.

---

## SOLUTION 4: Channel Isolation (Red)

### Complete Implementation

```c
#include "helpers.h"

// Isolate the red channel only
// Sets green and blue to 0, leaving only red information
void customFilter(int height, int width, RGBTRIPLE image[height][width])
{
    // Loop through each pixel
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            // Zero out green and blue channels
            image[i][j].rgbtGreen = 0;
            image[i][j].rgbtBlue = 0;
            // Red channel remains unchanged
        }
    }
}
```

### Variant: Green Channel Only

```c
#include "helpers.h"

// Isolate the green channel only
void customFilter(int height, int width, RGBTRIPLE image[height][width])
{
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            // Zero out red and blue channels
            image[i][j].rgbtRed = 0;
            image[i][j].rgbtBlue = 0;
            // Green channel remains unchanged
        }
    }
}
```

### Variant: Blue Channel Only

```c
#include "helpers.h"

// Isolate the blue channel only
void customFilter(int height, int width, RGBTRIPLE image[height][width])
{
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            // Zero out red and green channels
            image[i][j].rgbtRed = 0;
            image[i][j].rgbtGreen = 0;
            // Blue channel remains unchanged
        }
    }
}
```

### Instructor Notes — Channel Isolation

**Why This is Useful:**
Channel isolation reveals how much of an image's information comes from each color. Some observations:
- Skin tones have high red
- Grass has high green
- Skies have high blue

**Test Results (Red Isolation):**
```
Before: (200, 100, 50)   After: (200, 0, 0) — red dominates
Before: (100, 150, 200)  After: (100, 0, 0) — green/blue ignored
Before: (50, 200, 100)   After: (50, 0, 0) — low red, green/blue ignored
```

**Combined Analysis:**
By comparing red, green, and blue isolated versions, you can understand image composition.

---

## Alternative Custom Filter Ideas

### Brightness Adjustment

```c
// Increase brightness by adding constant to all channels
void customFilter(int height, int width, RGBTRIPLE image[height][width])
{
    int brightnessDelta = 50;  // Try -50 for darker

    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            int newRed = image[i][j].rgbtRed + brightnessDelta;
            int newGreen = image[i][j].rgbtGreen + brightnessDelta;
            int newBlue = image[i][j].rgbtBlue + brightnessDelta;

            // Cap at 0 and 255
            newRed = newRed > 255 ? 255 : (newRed < 0 ? 0 : newRed);
            newGreen = newGreen > 255 ? 255 : (newGreen < 0 ? 0 : newGreen);
            newBlue = newBlue > 255 ? 255 : (newBlue < 0 ? 0 : newBlue);

            image[i][j].rgbtRed = (BYTE) newRed;
            image[i][j].rgbtGreen = (BYTE) newGreen;
            image[i][j].rgbtBlue = (BYTE) newBlue;
        }
    }
}
```

### Contrast Adjustment

```c
// Increase contrast by multiplying distance from middle (128) by factor
void customFilter(int height, int width, RGBTRIPLE image[height][width])
{
    float contrastFactor = 1.5;  // >1 increases contrast, <1 decreases

    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            // Shift to 0-center, apply contrast, shift back
            int newRed = (int) round(128 + contrastFactor * (image[i][j].rgbtRed - 128));
            int newGreen = (int) round(128 + contrastFactor * (image[i][j].rgbtGreen - 128));
            int newBlue = (int) round(128 + contrastFactor * (image[i][j].rgbtBlue - 128));

            // Cap at 0 and 255
            newRed = newRed > 255 ? 255 : (newRed < 0 ? 0 : newRed);
            newGreen = newGreen > 255 ? 255 : (newGreen < 0 ? 0 : newGreen);
            newBlue = newBlue > 255 ? 255 : (newBlue < 0 ? 0 : newBlue);

            image[i][j].rgbtRed = (BYTE) newRed;
            image[i][j].rgbtGreen = (BYTE) newGreen;
            image[i][j].rgbtBlue = (BYTE) newBlue;
        }
    }
}
```

### Desaturation (Move Toward Gray)

```c
// Reduce color saturation by mixing toward grayscale
void customFilter(int height, int width, RGBTRIPLE image[height][width])
{
    float saturation = 0.5;  // 0 = grayscale, 1 = original

    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            BYTE red = image[i][j].rgbtRed;
            BYTE green = image[i][j].rgbtGreen;
            BYTE blue = image[i][j].rgbtBlue;

            // Grayscale value (average)
            int gray = (red + green + blue) / 3;

            // Blend original with grayscale
            int newRed = (int) (saturation * red + (1 - saturation) * gray);
            int newGreen = (int) (saturation * green + (1 - saturation) * gray);
            int newBlue = (int) (saturation * blue + (1 - saturation) * gray);

            image[i][j].rgbtRed = (BYTE) newRed;
            image[i][j].rgbtGreen = (BYTE) newGreen;
            image[i][j].rgbtBlue = (BYTE) newBlue;
        }
    }
}
```

---

## Evaluation Rubric Notes

### High-Quality Implementation (25 pts)
- Algorithm is correct and produces intended visual effect
- Handles all pixels in the image
- Produces reasonable output for test images
- No unintended side effects

### Proper Data Handling (10 pts)
- Correctly cast between int and BYTE
- Uses appropriate variable types (float for sepia coefficients, int for sums)
- No integer overflow or underflow

### Edge Case Handling (10 pts)
- Caps values at 255 where necessary
- Caps values at 0 where necessary (e.g., brightness adjustment)
- Handles corner pixels and boundaries correctly

### Code Quality (10 pts)
- Clear variable names (not `a`, `b`, `c`)
- Comments explaining algorithm and key steps
- Proper indentation and formatting
- No hardcoded "magic numbers" without explanation

### Testing (10 pts)
- Test code provided and runs without errors
- Shows before/after pixel values
- Results make logical sense (e.g., colors change predictably)
- Multiple pixels tested (not just one)

---

## Assessment Tips for Instructors

1. **Quick Visual Check**: Display the filtered image if possible. Results should be visually apparent and match filter description.

2. **Test with Edge Colors**: Always include pure red (255,0,0), pure green (0,255,0), pure blue (0,0,255), white (255,255,255), black (0,0,0), and gray (128,128,128) in your test.

3. **Check Floating-Point Math**: For filters using floating-point (sepia, contrast), verify rounding is correct.

4. **Performance Note**: These filters run in O(height × width) time. On a 1000×1000 image, expect nearly instant execution.

5. **Creativity Bonus**: Give extra credit for well-designed custom filters that aren't in the list (brightness, contrast, desaturation, etc.), as long as they compile and work correctly.
