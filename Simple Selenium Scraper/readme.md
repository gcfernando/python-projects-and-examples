# Python Selenium Scraper with Headless Chrome

A short **Selenium web scraping example in Python** that runs Chrome in headless mode, opens the ESPN Cricinfo news page, and prints the page header and news headlines found by CSS class.

[Python projects](../README.md) · **Browser automation**

<a id="python-selenium-web-scraping-example--headless-chrome-headline-scraper"></a>

## Start here

Read the requirements and any configuration below, then follow the usage example. Source paths below are relative to the repository root; run commands from the working directory stated in Usage. This example’s source is in `Simple Selenium Scraper/Console_Code/`. Install any third-party packages in an isolated Python environment.

<a id="overview"></a>

<a id="-overview"></a>

## Overview

This script launches a headless Chrome browser, navigates to the ESPN Cricinfo news page, and extracts the page header and all news feed article titles. Results are printed to the console.

<a id="features"></a>

<a id="guide-features"></a>

<a id="-features"></a>

## Features

- Runs Chrome in headless mode (no visible browser window)
- Scrapes the page header and news article titles
- GPU acceleration disabled for compatibility in server environments
- Console cleared before displaying results

<a id="requirements"></a>

<a id="guide-prerequisites-and-installation"></a>

<a id="-prerequisites-and-installation"></a>

## Prerequisites and installation

```text
selenium
```

Install the dependency:

```bash
python -m pip install selenium
```

You also need:
- **Google Chrome** installed on your system
- **ChromeDriver** matching your Chrome version — available from [Chrome for Testing](https://googlechromelabs.github.io/chrome-for-testing/)

> **Source adaptation required:** the script passes the driver path as the first positional argument, `webdriver.Chrome(chromedriver_path, options=chrome_options)`. Current Selenium uses a `Service` for an explicit driver path. Update your local copy as described in the [official Selenium migration guide](https://www.selenium.dev/documentation/webdriver/troubleshooting/upgrade_to_selenium_4/):
>
> ```python
> from selenium.webdriver.chrome.service import Service
> driver = webdriver.Chrome(service=Service(chromedriver_path), options=chrome_options)
> ```
>
> With Selenium 4.6 or later you can also omit the path entirely and let Selenium Manager download a matching driver: `webdriver.Chrome(options=chrome_options)`.

<a id="configuration"></a>

<a id="-configuration"></a>

## Configuration

Open `Web_Scrape.py` and update the ChromeDriver path:

```python
chromedriver_path = "path/to/chromedriver.exe"
```

The target URL is set to:
```text
https://www.espncricinfo.com/cricket-news
```

You can change this to any URL and update the CSS class selectors (`ds-text-title-xl`, `ds-text-title-s`) to match the structure of your target page.

<a id="usage"></a>

<a id="guide-usage"></a>

<a id="-usage"></a>

## Usage

From the `Console_Code` folder:

```bash
python Web_Scrape.py
```

### Output Format

```text
Looking for : <page header text>
	<headline 1>
	<headline 2>
	...
```

Headlines change daily, and the CSS classes used by the site can change at any time; if nothing is printed, inspect the page and update the selectors.

<a id="file-structure"></a>

<a id="-architecture"></a>

## Architecture

```text
Simple Selenium Scraper/
└── Console_Code/
    └── Web_Scrape.py    # Main script
```

<a id="notes"></a>

<a id="guide-troubleshooting-and-limitations"></a>

<a id="-troubleshooting-and-limitations"></a>

## Troubleshooting and limitations

- The first two items from the news feed list are skipped (`news_feeds[2:]`) to avoid navigation elements.
- ChromeDriver must be version-compatible with the installed Chrome browser.
- The console is cleared with `os.system('cls')`, which is Windows-specific; use `clear` on macOS or Linux.
- Check a website's terms of use and `robots.txt` before scraping it, and keep request rates low.

<a id="related-projects"></a>

<a id="-related-documentation"></a>

## Related documentation

- [Tag Clouds — word cloud from scraped web pages](../TagClouds/readme.md)
- [Simple WhatsApp Sender — browser automation](../Simple%20WhatApp%20Sender/readme.md)
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python-projects-and-examples/documentation/) · [Project overview](../README.md) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
