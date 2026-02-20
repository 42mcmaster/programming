---
marp: true
theme: default
class: invert
paginate: true
---
# Lesson 02: Structs & Image Processing
## Programming
### Medina County Career Center
---

## Quick Review: Week 1

- Variables and data types (int, float, char)
- Arrays: collections of the same type
- Functions: reusable blocks of code
- Loops: for, while
- Conditionals: if, else

Today we extend arrays and create custom data types.

---

## Structs: Custom Data Types

A **struct** groups related data into one custom type.

```c
typedef struct {
    int red;
    int green;
    int blue;
} RGBTRIPLE;
```

- Each variable inside is a **member** or **field**
- Access members using **dot notation**: `pixel.red`
- `typedef` makes it easier to declare variables

---

## Arrays of Structs

Create an array of RGBTRIPLE pixels:

```c
RGBTRIPLE pixels[10];
pixels[0].red = 255;
pixels[0].green = 128;
pixels[0].blue = 64;
```

A function can operate on an array of structs:

```c
void printPixel(RGBTRIPLE p) {
    printf("RGB: %d, %d, %d\n", p.red, p.green, p.blue);
}
```

Next you'll see RGBTRIPLE in image processing. Same idea!

---

## 2D Arrays

A 2D array represents a grid:

```c
int grid[3][4];   // 3 rows, 4 columns
grid[0][1] = 5;   // Row 0, Column 1
```

**Row-Major Layout:**
```
grid[0][0] grid[0][1] grid[0][2] grid[0][3]
grid[1][0] grid[1][1] grid[1][2] grid[1][3]
grid[2][0] grid[2][1] grid[2][2] grid[2][3]
```

Traverse with nested loops:
```c
for (int i = 0; i < 3; i++) {
    for (int j = 0; j < 4; j++) {
        printf("%d ", grid[i][j]);
    }
}
```

---

## Images as 2D Arrays of Pixels

An image is a 2D array of pixels. Each pixel is a struct with three bytes (RGB).

```
+-------+-------+-------+
| PIXEL | PIXEL | PIXEL |  Row 0
+-------+-------+-------+
| PIXEL | PIXEL | PIXEL |  Row 1
+-------+-------+-------+
```

BMP files store:
- **BITMAPFILEHEADER**: file metadata
- **BITMAPINFOHEADER**: image dimensions, color depth
- **Pixel data**: row by row, RGB triples

We work with scaffold code that reads BMP files for us.

---

## Sub-Lesson 02b: Image Filter Exercise

You'll use the **CS50 Filter** project:
- `bmp.h`: BMP file format definitions
- `helpers.h`: function declarations
- `filter.c`: main program
- **You touch only `helpers.c`**

Three filters to code:
1. **Grayscale** - convert to black and white
2. **Blur** - smooth the image (3x3 box filter)
3. **Edge Detection** (stretch) - Sobel operator

---

## Grayscale Filter

Average the RGB values for each pixel:

```c
avg = (red + green + blue) / 3;
newPixel.red = newPixel.green = newPixel.blue = avg;
```

Round to nearest integer using `round()`.

Loop through every pixel with nested loops:
```c
for (int i = 0; i < height; i++) {
    for (int j = 0; j < width; j++) {
        // Process pixel at [i][j]
    }
}
```

---

## Blur Filter

A **3x3 box filter** averages each pixel and its 8 neighbors:

```
+---+---+---+
| X | X | X |  Neighbors (including center)
+---+---+---+
| X | P | X |
+---+---+---+
| X | X | X |
+---+---+---+
```

Challenge: Boundary pixels have fewer neighbors.
- Option 1: Skip boundaries
- Option 2: Use only available neighbors

Average the 3x3, round, assign to center pixel.

---

## Debugging Tips

Use `printf()` to inspect values:

```c
printf("Pixel at [%d][%d]: R=%d G=%d B=%d\n",
       i, j, image[i][j].red, image[i][j].green, image[i][j].blue);
```

Check loop boundaries:
- Do rows go from 0 to height-1?
- Do columns go from 0 to width-1?

Print intermediate calculations (sums, averages) before assigning.

---

## Key Takeaways

- **Structs** bundle related data (like RGB values)
- **2D arrays** represent grids (like images)
- **Nested loops** traverse 2D arrays
- **Images** are 2D arrays of pixel structs
- **Filters** transform pixels using math and loops
