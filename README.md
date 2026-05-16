# 🖼️ Image Processing Application

A **pure C++** image processing application that applies various transformations and filters to images using matrix-based pixel manipulation — with no external libraries required.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [How It Works](#how-it-works)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Compilation](#compilation)
  - [Running](#running)
- [Operations](#operations)
- [Output Files](#output-files)
- [Image Format](#image-format)
- [Example Output](#example-output)

---

## Overview

This project implements fundamental image processing operations from scratch in C++. Images are represented internally as **3D matrices** (`[height][width][channel]`) and stored in the **PPM (P3)** format. A built-in 4×4 test image is generated automatically at runtime to demonstrate all supported operations.

---

## ✨ Features

| Operation              | Description                                              |
|------------------------|----------------------------------------------------------|
| 🎨 Grayscale Conversion | Converts RGB image to single-channel grayscale           |
| ↔️ Horizontal Flip      | Mirrors the image left-to-right                          |
| ↕️ Vertical Flip        | Mirrors the image top-to-bottom                          |
| ☀️ Brightness Adjustment | Increases or decreases pixel intensity                   |
| 🔲 Contrast Adjustment  | Enhances or reduces the difference between light and dark|
| 🌫️ Blur Filter          | Smooths the image using a 3×3 averaging kernel           |
| 🔄 90° Rotation         | Rotates the image 90 degrees clockwise                   |

---

## 🧠 How It Works

### Image Representation

The `Image` class stores pixel data as a 3D vector:

```
data[y][x][channel]
```

- `y` → row (height)
- `x` → column (width)
- `channel` → 0=Red, 1=Green, 2=Blue (or 0 for grayscale)

### Pixel Access

Pixels are accessed via overloaded `operator()`:

```cpp
image(y, x, channel) = value;
```

---

## 📁 Project Structure

```
Image_Processing_Application/
│
├── main.cpp              # All source code (Image class + processing functions + main)
├── ImageProcessing.exe   # Compiled Windows executable
├── .gitignore
│
└── Output Files (generated at runtime):
    ├── test_image.ppm
    ├── gray_image.ppm
    ├── flipped_horizontal.ppm
    ├── flipped_vertical.ppm
    ├── bright_image.ppm
    ├── contrast_image.ppm
    ├── blurred_image.ppm
    └── rotated90_image.ppm
```

---

## 🚀 Getting Started

### Prerequisites

- A C++ compiler supporting **C++11 or later** (e.g., `g++`, `clang++`, MSVC)
- No external libraries needed — uses only the C++ Standard Library

### Compilation

**Linux / macOS:**
```bash
g++ -std=c++11 -o ImageProcessing main.cpp
```

**Windows (MinGW):**
```bash
g++ -std=c++11 -o ImageProcessing.exe main.cpp
```

**Windows (MSVC):**
```bash
cl /EHsc /std:c++11 main.cpp /Fe:ImageProcessing.exe
```

> **Note:** A pre-compiled `ImageProcessing.exe` for Windows is included in the repository.

### Running

```bash
./ImageProcessing        # Linux / macOS
ImageProcessing.exe      # Windows
```

The program will:
1. Generate a 4×4 test image (`test_image.ppm`)
2. Apply all seven transformations
3. Save each result as a separate PPM file
4. Print pixel data to the console for each operation

---

## ⚙️ Operations

### 1. Grayscale Conversion
Uses the standard luminance formula:

```
gray = 0.299 × R + 0.587 × G + 0.114 × B
```

### 2. Horizontal Flip
Maps each pixel `(y, x)` → `(y, width-1-x)`

### 3. Vertical Flip
Maps each pixel `(y, x)` → `(height-1-y, x)`

### 4. Brightness Adjustment
Adds a constant value to each channel, clamped to `[0, 255]`:

```
new_pixel = clamp(pixel + value, 0, 255)
```

Default adjustment used: **+50**

### 5. Contrast Adjustment
Centers pixel around 0, scales, then re-centers:

```
new_pixel = clamp(factor × (pixel - 128) + 128, 0, 255)
```

Default factor used: **1.5**

### 6. Blur Filter
Applies a 3×3 box blur (average of 9 neighboring pixels):

```
output(y, x) = sum of 3×3 neighborhood / 9
```

> Note: Border pixels (1-pixel border) are left as zero.

### 7. 90° Clockwise Rotation
Remaps pixel `(y, x)` → `(x, height-1-y)` in the transposed output image.

---

## 📄 Output Files

After running the program, the following PPM files are created in the working directory:

| File                     | Contents                          |
|--------------------------|-----------------------------------|
| `test_image.ppm`         | Original generated 4×4 test image |
| `gray_image.ppm`         | Grayscale version                 |
| `flipped_horizontal.ppm` | Left-right mirror                 |
| `flipped_vertical.ppm`   | Top-bottom mirror                 |
| `bright_image.ppm`       | Brightness increased by 50        |
| `contrast_image.ppm`     | Contrast scaled by factor 1.5     |
| `blurred_image.ppm`      | 3×3 box blur applied              |
| `rotated90_image.ppm`    | Rotated 90° clockwise             |

To view `.ppm` files, use:
- [GIMP](https://www.gimp.org/)
- [IrfanView](https://www.irfanview.com/)
- [ImageMagick](https://imagemagick.org/) — to convert: `magick image.ppm image.png`
- Linux: `eog image.ppm` or `display image.ppm`

---

## 🗂️ Image Format

The project uses the **PPM P3** (Portable Pixmap) format — a simple, human-readable image format:

```
P3
<width> <height>
<max_value>
R G B  R G B  R G B ...
```

- Plain text, no compression
- Supports RGB color (3 channels)
- Max pixel value: **255**

---

## 💡 Example Output (Console)

```
Image Processing with Matrices - Student Project
================================================

Created 4x4 test image: test_image.ppm

Applying image transformations...
- Grayscale conversion completed
- Horizontal flip completed
- Vertical flip completed
- Brightness adjustment completed
- Contrast adjustment completed
- Blur filter completed
- 90-degree rotation completed

All operations completed successfully!
Check the generated PPM files to see the results.
```

---

## 👩‍💻 Author

**Rowida El** — [@rowidaEl](https://github.com/rowidaEl)
