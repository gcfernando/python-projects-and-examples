# Generate a QR Code in Python — Custom Colours with the qrcode Library

A short Python script that shows **how to generate a QR code in Python** with the `qrcode` library, using custom fill and background colours and saving the result as a PNG image.

<a id="overview"></a>

## 🔎 Overview

This script uses the `qrcode` library to create a QR code that encodes a short text containing a LinkedIn profile address. The QR code is styled with a dark blue fill on a light gray background and saved to `profile.png`. A sample `profile.png` is included in the `Console_Code` folder.

<a id="features"></a>

## ✨ Features

- Encodes any text or URL into a QR code
- Configurable box size and border width
- Custom fill and background colors
- Output saved as a PNG image

<a id="requirements"></a>

## 📦 Prerequisites and installation

```text
qrcode[pil]
```

Install the dependency:

```bash
python -m pip install "qrcode[pil]"
```

> The `[pil]` extra installs Pillow, which is required for image generation.

<a id="configuration"></a>

## ⚙️ Configuration

| Parameter | Value | Description |
|---|---|---|
| `version` | `1` | Starting QR code size (1–40). Because `qr.make(fit=True)` is used, the version grows automatically if the data does not fit |
| `box_size` | `15` | Pixel size of each box in the QR code |
| `border` | `5` | Width of the quiet zone border (in boxes) |
| `fill_color` | `'darkblue'` | Color of the QR code modules |
| `back_color` | `'lightgray'` | Background color |

<a id="usage"></a>

## 💡 Usage

Open `qr_code.py` and update the `data` variable with your desired content:

```python
data = 'Your text or URL here'
```

Then run the script from the `Console_Code` folder:

```bash
python qr_code.py
```

To make the QR code open a website when scanned, encode a full URL including `https://`; plain text is shown as text by most scanner apps.

A file named `profile.png` will be created in the working directory.

<a id="file-structure"></a>

## 🏗️ Architecture

```text
QR Code/
└── Console_Code/
    ├── qr_code.py    # Main script
    └── profile.png   # Sample output
```

<a id="related-projects"></a>

## 🔗 Related documentation

- [Steganography — hide text inside a PNG](../Stenography/readme.md)
- [Image to ASCII](https://gcfernando.github.io/python-projects-and-examples/Image%20to%20ASCII/)
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python-projects-and-examples/documentation/) · [Project overview](../README.md) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
