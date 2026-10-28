[Python projects](../README.md) · **Audio processing**

<a id="re-encode-mp3-files-in-python--change-bitrate-channels-and-sample-rate-with-pydub"></a>

# Re-encode MP3 Files with Python, pydub and FFmpeg

A command-line tool written in Python that **re-encodes MP3 files** with a chosen bitrate, channel option, and sample rate using `pydub` and FFmpeg (`libmp3lame`), for a single file or a whole folder.

> **In this guide:** [Get started](#guide-prerequisites-and-installation) · [Walk through the example](#guide-usage) · [Understand the details](#guide-features) · [Check the limits](#guide-troubleshooting-and-limitations)

> Re-encoding cannot add detail that a lower-quality MP3 has already lost; a higher bitrate mainly makes the file larger. Use it to standardize settings or reduce file size.

<a id="overview"></a>

## 🔎 Overview

This script uses `pydub` (backed by FFmpeg) to re-encode one or more MP3 files. The original file is replaced in-place with the optimized version. ID3 tags from the original file are preserved in the output. It can process a single MP3 file or an entire folder of MP3s in one run.

<a id="features"></a>

<a id="guide-features"></a>

## ✨ Features

- Process a single MP3 file or a whole folder at once
- 7 bitrate menu options: `32k`, `64k`, `96k`, `128k`, `192k`, `256k`, `320k`
- 4 channel options: `mono`, `stereo`, `joint_stereo`, `dual_mono` (see [Channel options](#channel-options))
- 11 sample rate options: `8000` Hz to `192000` Hz
- ID3 tags are read from the original and written to the re-encoded output
- Original file is replaced in-place after encoding

<a id="requirements"></a>

<a id="guide-prerequisites-and-installation"></a>

## 📦 Prerequisites and installation

```text
pydub
```

You also need **FFmpeg** installed and available on your system PATH. Windows builds of `ffmpeg.exe`, `ffplay.exe`, and `ffprobe.exe` are included in the `Common/` folder, but the script does not point `pydub` at them automatically — add that folder to your PATH or install FFmpeg separately.

Install the Python dependency:

```bash
python -m pip install pydub
```

Install FFmpeg:

- **Windows:** Download from [ffmpeg.org](https://ffmpeg.org/download.html) and add to PATH
- **macOS:** `brew install ffmpeg`
- **Linux:** `sudo apt install ffmpeg`

<a id="usage"></a>

<a id="guide-usage"></a>

## 💡 Usage

From the `Console_Code` folder:

```bash
python QualityModifier.py
```

The script prompts for:

1. **File or folder path** — path to a single `.mp3` file or a folder containing `.mp3` files
2. **Bitrate** — one of: `32k`, `64k`, `96k`, `128k`, `192k`, `256k`, `320k`
3. **Mode** — one of: `mono`, `stereo`, `joint_stereo`, `dual_mono`
4. **Frequency (Hz)** — one of: `8000`, `11025`, `12000`, `16000`, `22050`, `24000`, `32000`, `44100`, `48000`, `96000`, `192000`

### Example Session

```text
Enter the file path or folder path: C:\Music\album

BitRates (Kbps) => 32k, 64k, 96k, 128k, 192k, 256k, 320k
Select BitRate (Kbps): 320k

Modes => mono, stereo, joint_stereo, dual_mono
Select Mode: stereo

Frequencies => 8000, 11025, 12000, 16000, 22050, 24000, 32000, 44100, 48000, 96000, 192000
Select Frequency: 44100

song1.mp3 successfully optimized
song2.mp3 successfully optimized
```

## Channel options

The channel options are applied by `pydub` before encoding; they are not LAME's joint-stereo or dual-channel encoder modes:

| Option | What the script does |
|---|---|
| `mono` | Converts stereo input to one channel |
| `stereo` | Keeps the existing channels |
| `joint_stereo` | Mono input becomes two channels; stereo input is remixed by overlaying the left and right channels with panning onto a silent base track |
| `dual_mono` | Mono input becomes two channels; stereo input keeps **one randomly chosen channel**, so the output is mono |

<a id="file-structure"></a>

## 🏗️ Architecture

```text
Improve MP3 Quality/
├── Common/
│   ├── ffmpeg.exe            # Bundled Windows FFmpeg binaries
│   ├── ffplay.exe
│   └── ffprobe.exe
└── Console_Code/
    └── QualityModifier.py    # Main script
```

<a id="notes"></a>

<a id="guide-troubleshooting-and-limitations"></a>

## 🛠️ Troubleshooting and limitations

- The original file is overwritten. Back up your files before running if needed.
- Only `.mp3` files are processed when a folder path is given.
- The `libmp3lame` encoder is used for all output files.
- The selected bitrate is not always the final encoder argument. `scale_qality()` appends a second `-b:a` value: `256k` maps to `245k`, `192k` to `225k`, `128k` to `130k`, `96k` to `100k`, `64k` to `65k`, and `32k` falls back to `65k`. The `320k` option appends `320k`. Treat the menu as the current implementation, not a guarantee of the requested output bitrate.
- The menu includes `96000` and `192000` Hz, but listing a sample rate does not establish that the MP3 encoder can produce it. Encoding failures are caught and only a generic failure message is printed.
- Each file is first written to `<name>_temp.mp3` and then moved over the original with `os.replace`.

<a id="related-projects"></a>

## 🔗 Related documentation

- [MP3 Tags — read ID3 metadata](https://gcfernando.github.io/python-projects-and-examples/MP3%20Tags/)
- [MP3 Player with crossfade](https://gcfernando.github.io/python-projects-and-examples/MP3%20Player/)
- [Audio8D — FFmpeg 8D audio converter](https://github.com/gcfernando/8d-audio-converter)
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python-projects-and-examples/documentation/) · [Project overview](../README.md) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
