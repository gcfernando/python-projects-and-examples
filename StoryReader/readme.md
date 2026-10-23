# Read a PDF Aloud with Python — PyPDF2 and pyttsx3 Offline Text-to-Speech

A short Python script that **reads a PDF aloud**, page by page: it extracts the text with `PyPDF2` and speaks it with `pyttsx3`, which uses your operating system's built-in (offline) text-to-speech voices.

<a id="overview"></a>

## 🔎 Overview

This script extracts text from a PDF file using `PyPDF2` and converts it to speech using `pyttsx3`. It reads each page sequentially, with a brief pause between pages for natural pacing. A preferred voice (female by default) is selected automatically if available.

<a id="features"></a>

## ✨ Features

- Reads all pages of a PDF aloud using the system's text-to-speech engine
- Tries to select a voice whose name or ID contains "female" (see the note on voice selection below)
- Configurable reading speed (words per minute) and volume
- Prints progress to the console as each page is read
- Short pause between pages for a more natural listening experience
- Error handling for missing files and unexpected issues

<a id="requirements"></a>

## 📦 Prerequisites and installation

```text
PyPDF2
pyttsx3
```

Install dependencies:

```bash
python -m pip install PyPDF2 pyttsx3
```

<a id="usage"></a>

## 💡 Usage

`Story.pdf` is not included in the repository. Place your own PDF named `Story.pdf` in the folder you run the script from (or update the path), then run:

```bash
python StoryReader.py
```

The entry point reads `Story.pdf` at rate 150 and volume 0.9. Voice selection searches installed voice names/IDs for the requested gender text, then falls back to the second installed voice; the resulting voice depends on the system.

### Changing the PDF File

Update the file path in the `__main__` block:

```python
read_pdf_aloud("path/to/your/file.pdf", voice_id=chosen_voice, rate=150, volume=0.9)
```

### Parameters

| Parameter | Entry-point value | Description |
|---|---|---|
| `file_path` | `"Story.pdf"` | Path to the PDF file |
| `voice_id` | Result of `select_voice()` | Installed system voice ID; gender is not guaranteed |
| `rate` | `150` | Speaking speed in words per minute |
| `volume` | `0.9` | Volume level (0.0 to 1.0) |

<a id="file-structure"></a>

## 🏗️ Architecture

```text
StoryReader/
└── Console_Code/
    └── StoryReader.py    # Main script
```

<a id="notes"></a>

## 🛠️ Troubleshooting and limitations

- `pyttsx3` uses the operating system's built-in TTS engine (SAPI5 on Windows, NSSpeechSynthesizer on macOS, eSpeak on Linux).
- Pages with no extractable text are silently skipped.
- Press `Ctrl+C` to interrupt playback.
- `PyPDF2` is no longer developed under that name; its successor is `pypdf`, which provides the same `PdfReader` class.

### Voice selection

`select_voice` looks for the requested gender text in each installed voice's name or ID. Names without that text do not match, even if the voice has the desired characteristics. The fallback is `voices[1]`, the second installed voice; it raises `IndexError` when fewer than two voices are installed. Choose an installed voice ID explicitly when adapting the sample.

Calling `read_pdf_aloud()` directly uses its function default volume of `1.0` unless supplied; the entry point explicitly passes `0.9`. Voice initialization and selection happen before the PDF-reading error handler. A system without a matching voice and with fewer than two installed voices can therefore fail before that handler runs. Image-only pages need OCR, which this script does not implement.

<a id="related-projects"></a>

## 🔗 Related documentation

- [Text2Audio — Google text-to-speech desktop app](../Text2Audio/readme.md)
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python_codes/documentation/) · [Project overview](https://gcfernando.github.io/python_codes/) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
