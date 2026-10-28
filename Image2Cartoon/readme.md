[Python projects](../README.md) · **Images and OpenCV**

<a id="cartoonify-an-image-with-python-and-opencv--image2cartoon"></a>

# Turn Photos into Cartoons with Python and OpenCV

A short Python script that shows **how to cartoonify a photo with OpenCV**: median blur, adaptive-threshold edge detection, and a bilateral filter are combined to turn a regular photograph into a cartoon-style image.

> **In this guide:** [Get started](#guide-prerequisites-and-installation) · [Walk through the example](#guide-usage) · [Understand the details](#guide-architecture)

<a id="overview"></a>

## 🔎 Overview

This script applies a series of computer vision operations to transform an input image into a cartoon-like rendering. The original and cartoon images are displayed side by side for comparison.

<a id="requirements"></a>

<a id="guide-prerequisites-and-installation"></a>

## 📦 Prerequisites and installation

```text
opencv-python
```

Install the dependency:

```bash
python -m pip install opencv-python
```

<a id="usage"></a>

<a id="guide-usage"></a>

## 💡 Usage

Open `CartoonImage.py` and set the input image path:

```python
input_image_path = 'path/to/your/image.jpg'
```

Then run the script:

```bash
python CartoonImage.py
```

Two windows will open — one showing the original resized image and one showing the cartoon version. Press any key to close them.

The result is only displayed, not saved. To keep it, add `cv2.imwrite('cartoon.jpg', cartoon_image)` after the conversion.

## How It Works

The cartoon effect is produced in five steps:

1. **Grayscale conversion** — the image is converted from BGR to grayscale
2. **Median blur** — a 5×5 median blur reduces noise
3. **Edge detection** — adaptive mean thresholding identifies edges
4. **Bilateral filter** — the color image is smoothed while sharp edges are preserved
5. **Bitwise AND** — the smoothed color image is combined with the edge mask to produce the cartoon effect

The output is resized to 500×500 pixels.

## Tips

- Both images are resized to a fixed 500×500, which stretches photos that are not square. Resize by a scale factor instead to keep the aspect ratio.
- `cv2.adaptiveThreshold(..., 9, 9)` controls edge detection (block size and constant); `cv2.bilateralFilter(image, 9, 250, 250)` controls how flat the colour areas become. Adjust them to make lines thicker or colours smoother.

<a id="file-structure"></a>

<a id="guide-architecture"></a>

## 🏗️ Architecture

```text
Image2Cartoon/
└── Console_Code/
    └── CartoonImage.py    # Main script
```

<a id="related-projects"></a>

## 🔗 Related documentation

- [Photo to graphite pencil sketch CLI](../Graphite_CLI/README.md)
- [Remove Background](https://gcfernando.github.io/python-projects-and-examples/Remove%20Background/)
- [Image to ASCII](https://gcfernando.github.io/python-projects-and-examples/Image%20to%20ASCII/)
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python-projects-and-examples/documentation/) · [Project overview](../README.md) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
