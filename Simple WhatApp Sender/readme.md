# Send a Scheduled WhatsApp Message with Python — pywhatkit Example

A short Python script that shows **how to schedule and send a WhatsApp message from Python** with the `pywhatkit` library, which automates WhatsApp Web in your browser.

<a id="overview"></a>

## 🔎 Overview

This script automates sending a WhatsApp message via WhatsApp Web. It opens the WhatsApp Web interface in a browser at the scheduled time and sends the message automatically.

<a id="features"></a>

## ✨ Features

- Sends a WhatsApp message to any phone number with a country code
- Schedules the message for a specific hour and minute (24-hour format)
- Automatically closes the browser tab after sending (`tab_close=True`)

<a id="requirements"></a>

## 📦 Prerequisites and installation

```text
pywhatkit
```

Install the dependency:

```bash
python -m pip install pywhatkit
```

> WhatsApp Web must be open and logged in in your default browser before running the script. The script will open a new tab when it is time to send.

<a id="configuration"></a>

## ⚙️ Configuration

Open `WhatAppMessage.py` and update the following variables:

| Variable | Description | Example |
|---|---|---|
| `phone_number` | Recipient's phone number in international format, starting with `+` and the country code | `"+46123456789"` |
| `message` | Text of the message to send | `"Hello from Python!"` |
| `hour` | Hour to send the message (24-hour format) | `21` |
| `min` | Minute to send the message | `5` |

<a id="usage"></a>

## 💡 Usage

From the `Cosole_Code` folder:

```bash
python WhatAppMessage.py
```

The script will wait until the specified time, then open WhatsApp Web and send the message automatically.

## How It Works

In `pywhatkit` 5.4, `sendwhatmsg`:

1. Checks that the number contains a `+` country code (otherwise it raises `CountryCodeException`).
2. Calculates the time until the scheduled minute and sleeps until 15 seconds before it (`wait_time=15`).
3. Opens a WhatsApp Web chat link in your **default browser**, waits for it to load, clicks the centre of the screen, and presses **Enter** with `pyautogui`.
4. With `tab_close=True`, closes the tab a few seconds after sending.

Because it simulates mouse and keyboard input, keep the computer unlocked, the browser window visible, and avoid typing while it sends. The scheduled time must be at least 15 seconds in the future; a time that has already passed today is treated as that time tomorrow.

<a id="file-structure"></a>

## 🏗️ Architecture

```text
Simple WhatApp Sender/
└── Cosole_Code/
    └── WhatAppMessage.py    # Main script
```

<a id="notes"></a>

## 🛠️ Troubleshooting and limitations

- WhatsApp Web must be logged in before the scheduled send time.
- Phone number format: include the country code with `+` (e.g., `+46` for Sweden, `+1` for USA).
- Only send messages to people who expect them; automated bulk messaging can breach WhatsApp's terms of service.

<a id="related-projects"></a>

## 🔗 Related documentation

- [Use Twilio — send SMS and WhatsApp messages through an API](../Use%20Twilio/readme.md)
- [Simple Selenium Scraper — browser automation](../Simple%20Selenium%20Scraper/readme.md)
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python_codes/documentation/) · [Project overview](https://gcfernando.github.io/python_codes/) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
