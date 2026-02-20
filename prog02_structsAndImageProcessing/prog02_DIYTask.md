# prog02 DIY Task — Design Your Own Image Filter
## Creative Image Processing Challenge

### Overview
You have now implemented four image filters: grayscale, reflect, blur, and edge detection. For this task, you will **design and implement your own custom image filter**.

Choose one of the four filters described below, or design your own with instructor approval.

---

## Requirements

1. **Function Signature**: Your filter must follow this format:
   ```c
   void customFilter(int height, int width, RGBTRIPLE image[height][width])
   ```

2. **Documentation**: Include a comment explaining what your filter does and how it works

3. **Correct Implementation**: Your filter must compile and produce the intended visual effect

4. **Testing**: Test your filter on a sample image and describe the results

---

## Suggested Filters

### Option 1: Sepia Tone

**What it does:** Applies a warm, brown vintage photograph effect by weighting color channels differently.

**Algorithm:**
For each pixel, calculate:
```
newRed = 0.393 * red + 0.769 * green + 0.189 * blue
newGreen = 0.349 * red + 0.686 * green + 0.168 * blue
newBlue = 0.272 * red + 0.534 * green + 0.131 * blue
```

Then cap each channel at 255 if it exceeds the maximum.

**Starter Code:**
```c
// Apply sepia tone filter (warm, vintage effect)
void customFilter(int height, int width, RGBTRIPLE image[height][width])
{
    // Loop through each pixel
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            // Get the current pixel
            BYTE red = image[i][j].rgbtRed;
            BYTE green = image[i][j].rgbtGreen;
            BYTE blue = image[i][j].rgbtBlue;

            // Apply sepia formula to each channel
            int newRed = (int) round(// YOUR CODE HERE);
            int newGreen = (int) round(// YOUR CODE HERE);
            int newBlue = (int) round(// YOUR CODE HERE);

            // Cap at 255
            newRed = newRed > 255 ? 255 : newRed;
            newGreen = newGreen > 255 ? 255 : newGreen;
            newBlue = newBlue > 255 ? 255 : newBlue;

            // Update pixel
            image[i][j].rgbtRed = (BYTE) newRed;
            image[i][j].rgbtGreen = (BYTE) newGreen;
            image[i][j].rgbtBlue = (BYTE) newBlue;
        }
    }
}
```

**Why it works:** The sepia coefficients weight the red channel highest and the blue channel lowest, mimicking the chemical process of aged film.

---

### Option 2: Color Inversion

**What it does:** Inverts all colors, creating a photographic negative. Red becomes cyan, white becomes black, etc.

**Algorithm:**
For each pixel:
```
newRed = 255 - red
newGreen = 255 - green
newBlue = 255 - blue
```

**Starter Code:**
```c
// Invert all colors (create photographic negative)
void customFilter(int height, int width, RGBTRIPLE image[height][width])
{
    // Loop through each pixel
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            // Invert each color channel
            image[i][j].rgbtRed = 255 - // YOUR CODE HERE;
            image[i][j].rgbtGreen = 255 - // YOUR CODE HERE;
            image[i][j].rgbtBlue = 255 - // YOUR CODE HERE;
        }
    }
}
```

**Why it works:** Subtracting each channel from 255 flips the color space, creating complementary colors.

---

### Option 3: Threshold (Posterize)

**What it does:** Reduces the number of colors by quantizing each channel to discrete levels, creating a bold, poster-like effect.

**Algorithm:**
Choose a quantization level (e.g., 64 colors). For each channel:
```
quantized = (value / 64) * 64
```

This rounds each channel to the nearest multiple of 64 (0, 64, 128, 192, 255).

**Starter Code:**
```c
// Reduce colors for posterize effect
void customFilter(int height, int width, RGBTRIPLE image[height][width])
{
    // Quantization level (lower = fewer colors, higher = more colors)
    int quantizeLevel = 64;  // Try 32, 64, 128, etc.

    // Loop through each pixel
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            // Quantize each channel
            image[i][j].rgbtRed = (// YOUR CODE HERE) * quantizeLevel;
            image[i][j].rgbtGreen = (// YOUR CODE HERE) * quantizeLevel;
            image[i][j].rgbtBlue = (// YOUR CODE HERE) * quantizeLevel;
        }
    }
}
```

**Hint:** Use integer division: `(value / quantizeLevel) * quantizeLevel`

**Why it works:** Integer division rounds down to the nearest multiple, reducing the color palette drastically.

---

### Option 4: Channel Isolation

**What it does:** Isolate a single color channel (red, green, or blue), setting the other two to 0, to see how much of an image is made from one color.

**Algorithm:**
For red channel isolation:
```
newRed = red
newGreen = 0
newBlue = 0
```

Repeat for green and blue channels if desired (or switch between them).

**Starter Code:**
```c
// Isolate the red channel only
void customFilter(int height, int width, RGBTRIPLE image[height][width])
{
    // Loop through each pixel
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            // Keep red, zero out green and blue
            image[i][j].rgbtGreen = 0;
            image[i][j].rgbtBlue = 0;
            // Red channel stays unchanged: image[i][j].rgbtRed
        }
    }
}
```

**Why it works:** Removing two channels isolates the contribution of one color, useful for analyzing image composition.

---

## Design Your Own Filter

If you prefer, propose your own custom filter:

**Examples:**
- **Brightness adjustment**: Add a constant to all channels (with capping)
- **Desaturation**: Reduce color intensity by moving toward gray
- **Color shift**: Rotate hue in color space
- **Dithering**: Add noise to simulate lower bit depth
- **Chromatic aberration**: Separate color channels spatially
- **Vignette**: Darken edges while keeping center bright

**Requirements for custom filter:**
1. Submit a brief description (2–3 sentences) of your filter
2. Explain the algorithm
3. Get instructor approval before coding
4. Implement and test

---

## Testing Template

After implementing your filter, test it with this code:

```c
#include <stdio.h>
#include "helpers.h"

int main(void)
{
    // Create a small test image (3x3)
    RGBTRIPLE testImage[3][3] = {
        {
            {255, 0, 0},      // Pure red
            {0, 255, 0},      // Pure green
            {0, 0, 255}       // Pure blue
        },
        {
            {255, 255, 0},    // Yellow (red + green)
            {255, 255, 255},  // White (all channels)
            {0, 0, 0}         // Black (no channels)
        },
        {
            {128, 128, 128},  // Gray
            {200, 100, 50},   // Mixed brown
            {100, 200, 150}   // Mixed cyan
        }
    };

    printf("BEFORE filter:\n");
    printf("Pixel (0,0) Red: R=%d G=%d B=%d\n",
           testImage[0][0].rgbtRed,
           testImage[0][0].rgbtGreen,
           testImage[0][0].rgbtBlue);
    printf("Pixel (1,2) White: R=%d G=%d B=%d\n",
           testImage[1][2].rgbtRed,
           testImage[1][2].rgbtGreen,
           testImage[1][2].rgbtBlue);

    // Apply your filter
    customFilter(3, 3, testImage);

    printf("\nAFTER filter:\n");
    printf("Pixel (0,0): R=%d G=%d B=%d\n",
           testImage[0][0].rgbtRed,
           testImage[0][0].rgbtGreen,
           testImage[0][0].rgbtBlue);
    printf("Pixel (1,2) White: R=%d G=%d B=%d\n",
           testImage[1][2].rgbtRed,
           testImage[1][2].rgbtGreen,
           testImage[1][2].rgbtBlue);

    return 0;
}
```

---

## Submission Checklist

- [ ] Filter function compiles without errors
- [ ] Filter has a descriptive comment explaining the algorithm
- [ ] Test code runs and shows before/after pixel values
- [ ] Results make visual sense (e.g., sepia produces warm tones, inversion produces complementary colors)
- [ ] All channels are properly cast to BYTE
- [ ] Values are capped at 255 if necessary
- [ ] Code is well-commented and readable

---

## Evaluation Rubric

| Criterion | Points |
|-----------|--------|
| Correct algorithm implementation | 25 |
| Proper data types and casting | 10 |
| Handles edge cases (values > 255, < 0) | 10 |
| Clear, descriptive comments | 10 |
| Test code and results | 10 |
| Overall code quality and clarity | 10 |
| **Total** | **75** |

---

## Tips

1. **Start simple**: Choose the simplest filter (color inversion) if you're unsure
2. **Test incrementally**: Verify your formula on paper first with sample values
3. **Debug with print statements**: Print before/after values for a single pixel
4. **Don't over-engineer**: A 10-line filter is fine; complex doesn't mean better
5. **Watch for overflow**: If adding large numbers, cast to int before capping

---

## Interesting Extensions

Once you finish your filter:

1. **Chain filters**: Apply grayscale AFTER your custom filter
2. **Combine effects**: Apply sepia THEN blur for a vintage photo
3. **Performance**: Time your filter on a large image (e.g., 1000×1000 pixels)
4. **Comparison**: Apply your filter to the same image as a classmate's and compare results
