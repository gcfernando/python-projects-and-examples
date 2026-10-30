# Graphite CLI — Photo to Pencil Sketch with Python

**Graphite CLI** is a small Python command-line tool that converts a photograph into a **black-and-white graphite pencil sketch**. It uses OpenCV, NumPy, and Pillow, chooses its rendering settings automatically from each photo, and needs no GUI, network connection, AI model weights, or manual tuning. The output keeps the original pixel dimensions, and the result is deterministic for the same input and dependency versions.

[Python projects](../README.md) · **Images and OpenCV**

![Before-and-after example: a colour portrait of a woman holding a latte, and a black-and-white pencil-sketch version of the same photo](https://gcfernando.github.io/python-projects-and-examples/Graphite_CLI/Console_Code/Before%20and%20After.png)

*Before-and-after example image included in the project folder.*

<a id="photo-to-graphite-pencil-sketch--automatic-python-cli-opencv"></a>

## Start here

Read the requirements and any configuration below, then follow the usage example. Source paths below are relative to the repository root; run commands from the working directory stated in Usage. This example’s source is in `Graphite_CLI/Console_Code/`. Install any third-party packages in an isolated Python environment.

<a id="developer-installation-one-time"></a>

<a id="guide-prerequisites-and-installation"></a>

<a id="-prerequisites-and-installation"></a>

## Prerequisites and installation

Python 3.10+ is required. From the `Graphite_CLI/Console_Code` directory, install the dependencies:

```bash
python -m pip install -r requirements_portrait_graphite.txt
```

The requirements file (in `Console_Code/`) constrains compatible version ranges for `numpy>=1.26,<3`, `opencv-python>=4.8,<5`, and `Pillow>=10,<13`.

Install the dependencies as part of deployment so the end user only runs the two-argument command. An executable distribution would need to be built separately for each target operating system if users must not install Python or packages.

<a id="end-user-usage"></a>

<a id="guide-usage"></a>

<a id="-usage"></a>

## Usage

From the `Console_Code` folder:

```bash
python portrait_graphite_cli.py photo.jpg sketch.png
```

That's the complete command. The tool reads the photo, chooses rendering settings automatically, converts it to a black-and-white graphite-style image, preserves the input pixel dimensions, validates the saved bytes, and writes `sketch.png`. If you run the command again, `sketch.png` is replaced. **The input photo is never overwritten.** The tool will refuse when the input and output reference the same file.

On success it prints the saved file and its size, for example `Saved 'sketch.png' (1920 x 1080)`. Processing failures print `Error: <reason>` and exit with status code `1`. Invalid command-line arguments are handled by `argparse`, which prints usage and exits with status code `2`.

## How it works

1. **Load** — the photo is opened with Pillow, rotated according to its EXIF orientation, composited onto white (for transparent images), and converted to 8-bit grayscale. Images larger than 20 million pixels or smaller than 16 pixels on a side are rejected.
2. **Choose parameters** — percentiles of a downscaled preview measure exposure and contrast, then tone, gamma, line strength, and texture strength are adapted so dark photos are not muddy and flat photos get stronger strokes.
3. **Render** — an edge-preserving bilateral filter smooths the image, a tone curve keeps meaningful midtones, multi-scale difference-of-Gaussian detail draws dark lines (hair, eyebrows, lips, clothing), local variance suppresses speckle on smooth skin, and a subtle diagonal pencil hatch is added to darker textured areas.
4. **Validate** — the result is rejected if its dimensions changed, it lost almost all contrast, or it is overwhelmingly black.
5. **Save safely** — the image is encoded as PNG (or high-quality JPEG), decoded again to verify it, and written atomically through a temporary file, so a failed run never leaves a half-written output.

## Input and output formats

Supports common Pillow-readable image files as input and PNG/JPEG as output (`.png`, `.jpg`, `.jpeg`). EXIF rotation can swap width and height; dimension preservation is relative to the oriented image. For best lossless output, use `.png`.

<a id="project-structure"></a>

<a id="guide-architecture"></a>

<a id="-architecture"></a>

## Architecture

```text
Graphite_CLI/
└── Console_Code/
    ├── portrait_graphite_cli.py            # Command-line tool
    ├── requirements_portrait_graphite.txt  # Dependency version ranges
    └── Before and After.png                # Example result
```

<a id="guide-verification-limits"></a>

## Verification limits

This repository does not include an automated test module for Graphite CLI. The runtime validation described above checks output integrity and basic image properties; it does not verify artistic quality. Inspect the saved image when deciding whether a conversion meets your needs.

<a id="limitations"></a>

<a id="-troubleshooting-and-limitations"></a>

## Troubleshooting and limitations

This is a deterministic OpenCV renderer, not a neural image-to-image model or a human artist. It cannot guarantee a specific reference style, 100% identity preservation in perceptual terms, or perfect results on arbitrary photos. Automatic validation detects corrupted output, wrong dimensions, and obvious failures, not subjective artistic quality. For a strict artistic acceptance target, use a validated trained model or a human-in-the-loop quality-review process.

<a id="related-projects"></a>

<a id="-related-documentation"></a>

## Related documentation

- [Image2Cartoon](../Image2Cartoon/readme.md) — cartoon-style image effects with OpenCV
- [Image to ASCII](../Image%20to%20ASCII/readme.md) — turn an image into ASCII art
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python-projects-and-examples/documentation/) · [Project overview](../README.md) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
