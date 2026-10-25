# Remove Image Background in Python with rembg — AI Background Removal Example

A short Python script that shows **how to remove the background from an image in Python** using the AI-based `rembg` library, then places the subject on a solid black background with Pillow.

<a id="overview"></a>

## 🔎 Overview

This script takes an input image, removes its background using the AI-powered `rembg` library, and composites the foreground onto a solid black canvas. The result is saved as a new image file.

<a id="features"></a>

## ✨ Features

- Automatic background removal through `rembg.remove()`; the installed dependency chooses its default model
- Composites the transparent result onto a solid black background
- Loads the configured image with Pillow and re-encodes it as PNG before background removal; unsupported PNG modes need conversion first
- The default input and output names differ; keep them distinct to preserve the source image

<a id="requirements"></a>

## 📦 Prerequisites and installation

```text
rembg[cpu]
Pillow
```

Install dependencies:

```bash
python -m pip install "rembg[cpu]" Pillow
```

The [upstream rembg installation guide](https://github.com/danielgatis/rembg#installation) documents backend extras and current Python requirements. This repository does not pin a rembg version or explicitly select a model. Its default model, download size, cache location, and model-weight license can therefore change with the installed version. A first run may download weights; later runs can reuse cached weights. Check upstream model terms before using the output commercially.

<a id="usage"></a>

## 💡 Usage

By default the script processes the included sample image `Elephant.jpg` and writes `Elephant_Modified.jpg`, so you can try it straight away from the `Console_Code` folder:

```bash
python Remove.py
```

To use your own image, set the input and output paths in `Remove.py`:

```python
orginal_image = 'path/to/input.jpg'
output_image  = 'path/to/output.jpg'
```

The processed image will be saved at the output path.

## How It Works

1. The input image is opened and converted to PNG bytes (required by `rembg`).
2. `rembg.remove()` applies the background removal model.
3. The resulting RGBA image (with transparent background) is pasted onto a new black RGB canvas.
4. The final image is saved to the output path.

<a id="file-structure"></a>

## 🏗️ Architecture

```text
Remove Background/
└── Console_Code/
    ├── Remove.py      # Main script
    └── Elephant.jpg   # Sample input image
```

<a id="notes"></a>

## 🛠️ Troubleshooting and limitations

- The output background color is currently set to black. Change `'black'` to `'white'` or any other color in `Image.new('RGB', result_img.size, 'black')` to use a different background.
- `rembg` works best on images with clear subject-background contrast.
- To keep a transparent background instead, save `result_img` (the RGBA image) as a `.png` file rather than compositing it onto a colour.
- The function's docstring and variable name mention a white background, but the code uses `'black'`.

<a id="related-projects"></a>

## 🔗 Related documentation

- [Image2Cartoon — cartoon effect with OpenCV](../Image2Cartoon/readme.md)
- [Photo to graphite pencil sketch CLI](../Graphite_CLI/README.md)
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python-projects-and-examples/documentation/) · [Project overview](../README.md) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
