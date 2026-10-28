[Python projects](../README.md) · **CLI and databases**

<a id="python-bookmark-manager-cli--save-and-search-links-with-sqlite-and-rich"></a>

# Python Bookmark Manager with SQLite and Rich

A lightweight **command-line bookmark manager written in Python** for saving, searching, opening, editing, and deleting links with notes. It stores data in SQLite (no server needed) and uses `rich` for coloured terminal output — a compact example of a CRUD console app.

> **In this guide:** [Get started](#guide-prerequisites-and-installation) · [Walk through the example](#guide-usage) · [Understand the details](#guide-features) · [Check the limits](#guide-troubleshooting-and-limitations)

<a id="overview"></a>

## 🔎 Overview

Bookmark stores your important URLs in a local SQLite database (`links.db`) alongside a title and a short summary note. All operations are done through a simple interactive prompt. The `rich` library provides colored, readable output in the terminal.

<a id="features"></a>

<a id="guide-features"></a>

## ✨ Features

- **Add** links with a title, URL, and summary note
- **Search** links by keyword matching the title
- **Open** a saved link directly in your default web browser
- **Edit** the title, URL, and note of an existing bookmark
- **Delete** a bookmark by ID
- Data persisted in a local SQLite database (`links.db`)
- Color-coded terminal output via `rich`
- Graceful exit with `Ctrl+C`

<a id="requirements"></a>

<a id="guide-prerequisites-and-installation"></a>

## 📦 Prerequisites and installation

```text
rich
```

`sqlite3` and `webbrowser` are part of the Python standard library.

Install the dependency:

```bash
python -m pip install rich
```

<a id="usage"></a>

<a id="guide-usage"></a>

## 💡 Usage

From the `Console_Code` folder:

```bash
python book_marks.py
```

At the prompt, type one of the following commands:

| Command | Description |
|---|---|
| `ADD` | Add a new bookmark |
| `SEARCH` | Search bookmarks by title keyword |
| `EDIT` | Search and then edit a bookmark |
| `DELETE` | Search and then delete a bookmark |
| `OPEN` | Search and then open a bookmark in the browser |
| `HELP` | Show the list of available commands |

### Example Session

```text
COMMAND >> add
Title: Python Docs
URL: https://docs.python.org
Summary: Official Python documentation

COMMAND >> search
Keyword (Title): python
[1] Python Docs → https://docs.python.org
    Official Python documentation

COMMAND >> open
Keyword (Title): python
[1] Python Docs → https://docs.python.org
Choose ID: 1
Opening...
```

<a id="file-structure"></a>

## 🏗️ Architecture

```text
Bookmark/
└── Console_Code/
    └── book_marks.py    # Main script (also creates links.db in the working directory)
```

<a id="notes"></a>

<a id="guide-troubleshooting-and-limitations"></a>

## 🛠️ Troubleshooting and limitations

- `links.db` is created automatically in the directory where the script is run.
- The database schema adds the `note` column automatically if it's missing (for backwards compatibility with older databases).
- Commands are case-insensitive (`add`, `ADD`, and `Add` all work), and the search matches part of the title (`LIKE '%keyword%'`).

<a id="related-projects"></a>

## 🔗 Related documentation

- [Python dbm key-value database example](../Database/README.md)
- [Contact Book — Python GUI with SQL Server](../GUI_Apps/README.md)
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python-projects-and-examples/documentation/) · [Project overview](../README.md) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
