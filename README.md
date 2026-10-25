# 🐍 Python Projects and Code Examples

**Read online:** [Documentation website](https://gcfernando.github.io/python-projects-and-examples/) · [All guides](documentation.md)

<a id="-python-projects-and-code-examples--automation-networking-desktop-gui-media-and-machine-learning"></a>

Independent Python examples for automation, networking, desktop interfaces, image and audio processing, and machine learning.

![Language: Python](https://img.shields.io/badge/Language-Python-3776AB?logo=python&logoColor=white)

<a id="a-colorful-collection-of-python-experiments-utilities-and-applications"></a>

## Open in your browser

| HTML source | View page | Setup guide |
|---|---|---|
| [Wifi Radar/index.html](https://github.com/gcfernando/python-projects-and-examples/blob/main/Wifi%20Radar/index.html) | [Open WiFi Radar — static dashboard preview](https://gcfernando.github.io/python-projects-and-examples/Wifi%20Radar/index.html) | [Run the local Flask scanner](https://gcfernando.github.io/python-projects-and-examples/Wifi%20Radar/guide.html) |

The filename opens the HTML source on GitHub. The hosted preview can display and export simulated data. Live scanning and export of real scan results require the local Flask server; GitHub Pages does not run the scanner.

## 🔎 Overview

Choose a small project to study a concrete task: an asynchronous HTTP client, a SQLite bookmark manager, a TCP port scanner, an OpenCV image converter, or a scikit-learn training pipeline. The collection is for Python learners and developers looking for focused source examples.

Each project has its own dependencies and operating-system requirements. Some examples need configuration or have documented defects; read the project's guide before running it. There is no repository-wide installer or Python version guarantee.

## ✨ Features

- CLI examples using the standard library, asyncio, Rich, and external APIs.
- Desktop interfaces with Tkinter variants and a SQL Server contact manager.
- Image, MP3, QR code, steganography, and text-to-speech examples.
- Local Flask and Streamlit dashboards, plus regression and time-series exercises.

<a id="-getting-started"></a>

## 🚀 Quick start

Try a standard-library example first. From your terminal:

```bash
git clone https://github.com/gcfernando/python-projects-and-examples.git
cd python-projects-and-examples
python "Custom Exception/Console_Code/CustomException.py"
```

Expected output: `Something went wrong`. For an independent copy example:

```bash
python "Object Clone/Console_Code/CloneObject.py"
```

Expected output is `20` followed by `10` on separate lines. These examples need no packages, accounts, network requests, or local asset changes.

## 📦 Prerequisites and installation

Install Python 3 and Git to clone the collection. Check the selected guide for its Python version, third-party packages, platform tools, and required services. Port Scanner and Graphite CLI document Python 3.10+; that is not a tested minimum for every other project.

For examples with packages, create an isolated environment from the repository root:

```bash
python -m venv .venv
```

Use its interpreter directly, without changing shell execution policy:

```powershell
# Windows PowerShell: install Bookmark's dependency
.\.venv\Scripts\python.exe -m pip install rich
.\.venv\Scripts\python.exe "Bookmark/Console_Code/book_marks.py"
```

```bash
# macOS / Linux: the equivalent commands
.venv/bin/python -m pip install rich
.venv/bin/python "Bookmark/Console_Code/book_marks.py"
```

Bookmark creates `links.db` in the current working directory. Other scripts resolve assets from their own documented working directory. There is no repository-wide `requirements.txt`; install only the packages needed by your selected example.

## ⚙️ Configuration

Many scripts contain editable settings rather than CLI options. Check each guide for input/output paths, service endpoints, model files, credentials, and database setup. Environment-variable snippets in a guide are proposed adaptations unless its source already reads them.

Use your own credentials and keep them outside commits and copied terminal output. The SQL Server and API examples require particular care when replacing their embedded settings.

<a id="-project-index"></a>

## 💡 Usage

Open the project guide for its exact command, working directory, dependencies, and limitations.

### 🌐 Web, networking & automation

| Project | What it does |
|---|---|
| [Async HTTP](https://gcfernando.github.io/python-projects-and-examples/Async%20HTTP/) | Interactive asynchronous GET, POST, PUT, and DELETE requests to a sample REST API. |
| [Bookmark](Bookmark/readme.md) | Save, search, edit, delete, and open links stored in a local SQLite database. |
| [FixNetwork](FixNetwork/readme.md) | Windows network diagnostics and repair steps, including network-stack and adapter resets. |
| [Internet Speed Test](https://gcfernando.github.io/python-projects-and-examples/Internet%20Speed%20Test/) | Measure download, upload, and ping using Speedtest.net servers. |
| [Port Scanner](https://gcfernando.github.io/python-projects-and-examples/Port%20Scanner/) | Concurrent TCP connect scans with IPv4/IPv6, optional banners, and open-port JSON output. |
| [Simple Selenium Scraper](https://gcfernando.github.io/python-projects-and-examples/Simple%20Selenium%20Scraper/) | Use headless Chrome and Selenium to collect cricket-news headlines. |
| [Streamlit Demo](Streamlit/readme.md) | Explore Streamlit widgets, interactive data, and charts in a browser app. |
| [WiFi Radar setup](https://gcfernando.github.io/python-projects-and-examples/Wifi%20Radar/guide.html) · [Static dashboard preview](https://gcfernando.github.io/python-projects-and-examples/Wifi%20Radar/index.html) | Local Flask dashboard for nearby access points, with live scanning and CSV export. |
| [WiFi Scanner](https://gcfernando.github.io/python-projects-and-examples/Wifi%20Scanner/) | Scan nearby wireless networks and display signal, frequency, and security details. |
| [WiFi Profiles](https://gcfernando.github.io/python-projects-and-examples/Wifi%20Profiles/) | Manage saved Windows Wi-Fi profiles and inspect their stored connection details. |

### 🎧 Media, images & creative tools

| Project | What it does |
|---|---|
| [Graphite CLI](Graphite_CLI/README.md) | Convert a photo into a black-and-white graphite pencil sketch with a single OpenCV command. |
| [Image to ASCII](https://gcfernando.github.io/python-projects-and-examples/Image%20to%20ASCII/) | Convert an image into ASCII art saved as a text file. |
| [Image2Cartoon](Image2Cartoon/readme.md) | Apply OpenCV filters to create a cartoon-style image. |
| [Improve MP3 Quality](https://gcfernando.github.io/python-projects-and-examples/Improve%20MP3%20Quality/) | Re-encode MP3 files with configurable bitrate, channels, and sample rate. |
| [Lyrics](Lyrics/readme.md) | Search Genius for song metadata and a lyrics preview. |
| [MP3 Player](https://gcfernando.github.io/python-projects-and-examples/MP3%20Player/) | Shuffle a folder of MP3s with background preloading and crossfade transitions. |
| [MP3 Tags](https://gcfernando.github.io/python-projects-and-examples/MP3%20Tags/) | Read ID3 metadata and technical audio details from an MP3 file. |
| [QR Code](https://gcfernando.github.io/python-projects-and-examples/QR%20Code/) | Generate a styled QR code image from text or a URL. |
| [Remove Background](https://gcfernando.github.io/python-projects-and-examples/Remove%20Background/) | Remove an image background and composite the subject onto a solid backdrop. |
| [Steganography](Stenography/readme.md) | Hide and retrieve text in PNG images using least-significant-bit encoding. |
| [Story Reader](StoryReader/readme.md) | Extract text from a PDF and read it aloud with text-to-speech. |
| [Tag Clouds](TagClouds/readme.md) | Collect web-page text and render a word cloud using an image mask. |
| [Text2Audio](Text2Audio/readme.md) | Desktop text-to-speech app with selectable language and locale options. |

### 🖥️ Desktop apps & system utilities

| Project | What it does |
|---|---|
| [Contact Book](GUI_Apps/README.md) | Desktop contact manager backed by Microsoft SQL Server. |
| [Extract CPU Information](https://gcfernando.github.io/python-projects-and-examples/Extract%20CPU%20Information/) | Display CPU model, architecture, frequency, and core information. |
| [Health Monitor](https://gcfernando.github.io/python-projects-and-examples/Health%20Monitor/) | Live process-memory dashboard with heuristic growth warnings. |
| [Load Libraries](LoadLibraries/readme.md) | Call a compiled C#/.NET calculator library from Python using `pythonnet`. |
| [Password Utility](https://gcfernando.github.io/python-projects-and-examples/Password%20Utility/) | Explore password generation and a character-count rating heuristic. |
| [Setup Wizard — Fruit Wiki](SetupWizard/readme.md) | Browse fruit images and descriptions in a paginated desktop GUI. |
| [Simple WhatsApp Sender](https://gcfernando.github.io/python-projects-and-examples/Simple%20WhatApp%20Sender/) | Schedule a WhatsApp message through WhatsApp Web. |
| [Use Twilio](https://gcfernando.github.io/python-projects-and-examples/Use%20Twilio/) | Send SMS or WhatsApp messages and place calls through Twilio. |
| [Use Windows Login](https://gcfernando.github.io/python-projects-and-examples/Use%20Windows%20Login/) | Demonstrate checking the current Windows account credentials. |

### 🧠 Machine learning & data

| Project | What it does |
|---|---|
| [COVID Forecast](https://gcfernando.github.io/python-projects-and-examples/ML/COVID%20Forecast/) | Analyze and forecast daily COVID-19 case data with ARIMA/SARIMAX models. |
| [Salary Prediction](ML/Salary/readme.md) | Train a linear-regression salary model and use it for interactive predictions. |

### 🧩 Python fundamentals & persistence

| Project | What it does |
|---|---|
| [Custom Exception](https://gcfernando.github.io/python-projects-and-examples/Custom%20Exception/) | Define, raise, and catch a custom Python exception. |
| [Database](Database/README.md) | Store and retrieve key-value data using Python's built-in `dbm` module. |
| [Object Clone](https://gcfernando.github.io/python-projects-and-examples/Object%20Clone/) | Demonstrate independent object copies with `copy.deepcopy()`. |

<a id="-repository-layout"></a>

<a id="️-repository-layout"></a>

## 🏗️ Architecture

The projects are independent scripts rather than modules in a single application:

```mermaid
flowchart LR
    Index[Project index] --> Guide[Project guide]
    Guide --> Script[Console_Code or GUI_Code]
    Script --> Dependencies[Project-specific packages and tools]
    Script --> Inputs[Configured files or services]
```

`ML/` groups training and forecasting projects; `GUI_Apps/` contains Contact Book. [The documentation index](documentation.md) provides guide navigation and links to the existing Pages site. No application source layout has to change to use the guides.

## 🧪 Development and testing

There is no repository-wide automated test suite. Start with the two standard-library commands above, then verify one example at a time with disposable inputs and the setup in its guide. Do not import arbitrary scripts as a test: many execute prompts, GUI code, network operations, or file changes at module scope.

The tracked `audio8d-release.yml` workflow still refers to an absent `8D/` directory. It does not validate this collection. The separate [Audio8D repository](https://github.com/gcfernando/8d-audio-converter) contains that application; workflow repair is a code/configuration task outside these documentation changes.

<a id="-before-you-run-a-project"></a>
<a id="-faq"></a>

<a id="️-before-you-run-a-project"></a>

## 🛠️ Troubleshooting and limitations

| Symptom or task | Check first |
|---|---|
| `ModuleNotFoundError` | Install the selected guide's packages with the same interpreter used to run it. |
| Missing file or DLL | Replace hardcoded paths; use the working directory in the guide. |
| GUI, audio, or platform failure | Check desktop/audio availability and Windows-only dependencies; many examples have not been tested across all platforms. |
| HTTP or browser automation failure | External services, selectors, drivers, and unpinned library APIs can change. The Selenium guide documents required source adaptations. |
| Incorrect numerical or status output | Read the CPU temperature, speed-test units, Wi-Fi labels, MP3 bitrate, and memory-growth caveats in their guides. |

`FixNetwork` changes Windows networking settings. `Wifi Profiles` displays saved credentials and deletes profiles by default. The MP3 re-encoder replaces originals. Review those guides before execution and use appropriate test data. Messaging and API examples contact external services; use intended recipients and your own service configuration.

The [Database example](Database/README.md) documents an existing byte-key bug. The machine-learning examples are teaching exercises, with evaluation and dependency limits explained in their guides.

## 🤝 Contributing

Submit a focused issue or pull request in [this repository](https://github.com/gcfernando/python-projects-and-examples). Include the project path, operating system, Python/package versions, steps to reproduce, and redacted error output. When changing a script, update its guide with the exact command and working directory you verified.

## 🔒 Security

Avoid posting passwords, tokens, connection strings, saved Wi-Fi data, or private model/input files in public issues. This repository has no tracked security policy or private reporting channel; use GitHub's private vulnerability reporting option only if it is offered for the repository.

## 📄 Support and license

Use repository issues for setup questions, with the project name and reproducible details. No repository-level license file is tracked; do not infer reuse terms for the code, bundled binaries, fonts, images, or datasets. Third-party components have their own terms.

## 🔗 Related projects

- [Audio8D](https://github.com/gcfernando/8d-audio-converter) — a separate FFmpeg-based desktop and CLI audio converter.
- [Machine-learning datasets](https://github.com/gcfernando/machine-learning-practice-datasets) — CSV practice datasets.
- [Developer knowledge base](https://github.com/gcfernando/developer-guides-and-cheatsheets) — Python OOP and dunder-method references.
- [C# and .NET examples](https://github.com/gcfernando/csharp-dotnet-examples) — includes the reverse Python.NET bridge.

## Documentation links

[Guide index](documentation.md) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
