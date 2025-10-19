# Hands-on Notebook - Color Pixel Theory and Image Representation

This section explains how color pixels are modeled, stored, and manipulated in code. It focuses on practical concepts useful for computer-vision notebooks and quick examples using Pillow + NumPy.

## Goals

- Understand what a pixel represents and common color formats.
- Know how images map to arrays (shape, dtype, ordering).
- Show practical Python snippets for reading, inspecting, and converting images.

## Key concepts

- Pixel: the smallest addressable element in an image representing color and optionally alpha (transparency).
- Channel: one component of color (e.g., R, G, B). Multi-channel images store values per channel per pixel.
- Bit-depth / dtype: number of bits per channel—common types: uint8 (0–255), uint16 (0–65535), float32 (normalized 0–1).
- Spatial resolution: image width × height (number of pixels).
- Color space: interpretation of channel values (e.g., RGB, HSV, YCbCr). Converting changes interpretation, not raw storage.

## Common color formats

- Grayscale (L): one channel, intensity only.
- RGB / RGBA: 3 or 4 channels for red, green, blue (+ alpha).
- BGR: same data as RGB but channel order differs (used by OpenCV).
- HSV / HSL / YCbCr: perceptual or luminance-chrominance representations for specific operations.

## Image representation in memory

- Typical array shape: H × W × C (height, width, channels). For color images with Pillow/NumPy: (height, width, 3).
- Channel ordering: channel-last (HWC) is common in Python tools. Some frameworks (PyTorch) prefer channel-first (CHW).
- Row-major ordering: images are laid out row by row (scanlines).
- Example dtypes: uint8 for images saved from cameras, float32 for normalized/processed images.

## Simple conversions & formulas

- Grayscale (luminance) approximation (ITU-R BT.601):
    Y = 0.299 R + 0.587 G + 0.114 B
- Alpha compositing (over operator) for premultiplied alpha:
    C_out = C_a + C_b * (1 - A_a), where C are premultiplied colors.

## Practical examples (Pillow + NumPy)

Load image, inspect, and convert:

```python
from PIL import Image
import numpy as np

# Load image
img = Image.open("image.jpg")       # PIL Image
print(img.mode, img.size)          # e.g., "RGB", (width, height)

# Convert to NumPy
arr = np.array(img)                 # shape: (H, W, C) for color, dtype: uint8
print(arr.shape, arr.dtype)

# Convert to grayscale
gray = img.convert("L")             # PIL grayscale
arr_gray = np.array(gray)           # shape: (H, W)
```

Extract channels and reorder:

```python
r, g, b = arr[..., 0], arr[..., 1], arr[..., 2]   # channel-last
bgr = arr[..., ::-1]                              # RGB -> BGR (for OpenCV interop)
```

Normalize to float in [0, 1]:

```python
arr_float = arr.astype("float32") / 255.0
```

Convert RGB to luminance using weights:

```python
lum = (0.299 * arr[..., 0] + 0.587 * arr[..., 1] + 0.114 * arr[..., 2]).astype("uint8")
```

Save modified image:

```python
out = Image.fromarray(arr)  # arr must have a compatible dtype and shape
out.save("out.png")
```

## Notes on color conversions and precision

- Converting between color spaces (RGB↔HSV, RGB↔YCbCr) may be lossy in integer dtypes; use float for accurate transforms then quantize if needed.
- When performing math, convert to a higher-precision dtype to avoid overflow/rounding errors.

## Practical tips / best practices

- Always be explicit about dtype and channel order in interfaces (e.g., HWC uint8 RGB).
- For computer vision models, normalize images consistently (mean/std or 0–1) and document the expectation.
- Prefer using existing, tested libraries for color-space conversion (Pillow, OpenCV, scikit-image) rather than hand-rolling complex transforms unless needed.
- Remember metadata (EXIF orientation) — some image files require orientation correction after loading.

## Typical file-storage formats

- PNG: lossless, supports alpha, good for computed images.
- JPEG: lossy, widely used for photographs; no alpha.
- TIFF: flexible, supports many bit-depths and channels.
- RAW formats: camera-specific, higher bit-depth and sensor metadata.

Further reading and references are in the References section below this notebook’s header.

## References

- [Python Imaging Library](https://pillow.readthedocs.io/en/stable/)
- [Image Processing With the Python Pillow Library](https://realpython.com/image-processing-with-the-python-pillow-library/)
