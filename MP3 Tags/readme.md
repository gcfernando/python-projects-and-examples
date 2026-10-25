# Read MP3 ID3 Tags in Python — eyeD3 Metadata and Audio Info Example

A short Python script that shows **how to read MP3 metadata (ID3 tags) in Python** with `eyed3` — title, artist, album, genre, track number, and year — along with audio details such as sample rate, bitrate, duration, and channel mode.

<a id="overview"></a>

## 🔎 Overview

This script loads an MP3 file, extracts its ID3 tag information and audio stream properties, and prints them to the console. It covers both tag metadata (title, artist, genre, etc.) and technical audio details (bitrate, sample rate, duration, channels).

<a id="features"></a>

## ✨ Features

Extracts and displays the following information:

**ID3 Tags:**
- Title
- Artist
- Album
- Album Artist
- Genre
- Track Number
- Year (only if present in metadata)

**Audio Stream Properties:**
- Sample rate (Hz)
- Bitrate (kbps)
- Duration (seconds)
- Channel mode (stereo, mono, etc.)

**File Information:**
- File size (MB)

<a id="requirements"></a>

## 📦 Prerequisites and installation

```text
eyed3
```

Install the dependency:

```bash
python -m pip install eyed3
```

<a id="usage"></a>

## 💡 Usage

Open `ReadMP3File.py` and update the file path:

```python
mp3_file_path = "path/to/your/audio.mp3"
```

Then run the script from the `Console_Code` folder:

```bash
python ReadMP3File.py
```

### Output Format

```text
Title: <title>
Artist: <artist>
Album: <album>
Album Artist: <album artist>
Genre: <genre>
Track Number: (<track>, <total or None>)
Year: <year>
Sample Rate: <Hz>
Bitrate: <see known issue below>
Duration: <seconds>
Channels: <channel mode, e.g. Joint stereo>
File Size: <MB>
```

## Known issue: bitrate prints as 0 kbps

In `eyed3`, `audio_file.info.bit_rate` is a `(vbr, bitrate)` tuple whose bitrate is **already in kb/s**. The script divides it by 1000 again (`bit_rate[1] // 1000`), so a 320 kb/s file prints `Bitrate: 0 kbps`. Printing `audio_file.info.bit_rate[1]` — or `audio_file.info.bit_rate_str`, which also marks variable bitrates with `~` — shows the correct value.

<a id="file-structure"></a>

## 🏗️ Architecture

```text
MP3 Tags/
└── Console_Code/
    └── ReadMP3File.py    # Main script
```

<a id="notes"></a>

## 🛠️ Troubleshooting and limitations

- The file path is currently hardcoded in the script. Update it before running.
- Year is only printed if `getBestDate()` returns a valid date object.
- An untagged MP3 has `audio_file.tag` set to `None`; the existing `if audio_file.tag` guard skips tag output. The script does not guard `audio_file` itself: if `eyed3.load()` returns `None` for an unsupported input, the first attribute access fails.

<a id="related-projects"></a>

## 🔗 Related documentation

- [MP3 Player with crossfade](https://gcfernando.github.io/python-projects-and-examples/MP3%20Player/)
- [Improve MP3 Quality — re-encode MP3 files](https://gcfernando.github.io/python-projects-and-examples/Improve%20MP3%20Quality/)
- [Lyrics — Genius API song lookup](../Lyrics/readme.md)
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python-projects-and-examples/documentation/) · [Project overview](../README.md) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
