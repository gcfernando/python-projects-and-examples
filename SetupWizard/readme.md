# PySimpleGUI Image Viewer with PyInstaller Packaging — Fruit Wiki (Python)

A Python desktop GUI that displays fruit images and descriptions in a paginated viewer, built with **PySimpleGUI** and **Pillow**, with a `resource_path()` helper that makes bundled assets work when the app is packaged into a Windows executable with **PyInstaller**.

<a id="overview"></a>

## 🔎 Overview

Fruit Wiki is a simple desktop image browser for fruits. It reads image files from an `Images/` folder and matching text files from a `Data/` folder, then displays the fruit image and exposes its description as an image tooltip. Users can browse entries using Previous and Next buttons.

<a id="features"></a>

## ✨ Features

- Paginated image viewer with Previous / Next navigation
- Loads images (`.png`, `.jpg`, `.jpeg`) from an `Images/` folder
- Reads corresponding description text from a `Data/` folder (matched by filename)
- Images are automatically resized to fit a 300×300 display area
- Custom font loaded from a `Fonts/` folder (`Futura.ttf`)
- Dark teal theme (`DarkTeal10`)
- Resource helper for development working-directory paths and PyInstaller extraction paths

<a id="requirements"></a>

## 📦 Prerequisites and installation

```text
PySimpleGUI
Pillow
pyglet
pyinstaller
```

Install dependencies:

```bash
python -m pip install PySimpleGUI Pillow pyglet pyinstaller
```

<a id="usage"></a>

## 💡 Usage

### Running the script directly

When not packaged, `resource_path()` resolves `Fonts`, `Images`, and `Data` relative to the **current working directory**, so run the script from the `GUI_Code` folder:

```bash
cd GUI_Code
python fruitWiki.py
```

### Building a standalone executable with PyInstaller

In a one-file build, `resource_path()` looks for assets in PyInstaller's temporary extraction folder (`sys._MEIPASS`), so the asset folders must be bundled into the executable with `--add-data` (on Windows the separator is `;`). From the `GUI_Code` folder:

```bash
pyinstaller --onefile --windowed --icon icon.ico --add-data "Fonts;Fonts" --add-data "Images;Images" --add-data "Data;Data" fruitWiki.py
```

The executable is created in `dist/`.

<a id="folder-structure"></a>

## 🏗️ Architecture

```text
SetupWizard/
└── GUI_Code/
    ├── fruitWiki.py    # Main application
    ├── icon.ico        # Application icon
    ├── Fonts/
    │   └── Futura.ttf  # Custom font
    ├── Images/         # Apple, Banana, Cherry, Grapes, Mango, Papaya (.png)
    └── Data/           # Matching descriptions (Apple.txt, Banana.txt, ...)
```

Each `.txt` file in `Data/` must have the same base name as its matching image file. Six fruits are included.

<a id="notes"></a>

## 🛠️ Troubleshooting and limitations

- The `resource_path()` helper chooses the working directory during development and `sys._MEIPASS` in a bundle. Start from `GUI_Code` or bundle the folders as shown above; the helper does not include assets automatically.
- Sentence formatting is applied to description text: periods followed by a space are replaced with a newline.
- The Previous button starts disabled. After navigation, `button_control()` disables Previous or Next at the respective end; initial state is not recalculated after loading entries. The default six-entry set has a next item.
- Image order follows `os.listdir()` and is not sorted. An unreadable description can fail at `.replace()` before the later empty-content check.
- The custom font is registered with `pyglet.font.add_file`, which is why `pyglet` is a dependency.
- The repository does not pin a PySimpleGUI release. Check the installation instructions, terms and API compatibility of the release you choose; this sample has not established compatibility with every release or alternative package.

<a id="related-projects"></a>

## 🔗 Related documentation

- [Text2Audio — customtkinter text-to-speech app](../Text2Audio/readme.md)
- [Contact Book — ttkbootstrap and SQL Server](../GUI_Apps/README.md)
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python_codes/documentation/) · [Project overview](https://gcfernando.github.io/python_codes/) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
