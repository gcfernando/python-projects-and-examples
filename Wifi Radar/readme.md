<a id="manual-any-platform"></a>

# WiFi Radar — Python Wi-Fi Scanner with a Live Flask Web Dashboard

A real-time, cross-platform **Wi-Fi scanner written in Python** with a military-style radar web interface served by Flask. Displays nearby access points as live radar blips with signal strength, security info, vendor lookup, and CSV export.

<a id="overview"></a>

## 🔎 Overview

WiFi Radar runs a local Flask web server that continuously scans nearby Wi-Fi networks using native OS tools. The results are displayed in a browser-based radar UI that refreshes automatically. Vendor lookup is done via the macvendors.com API and cached locally.

<a id="features"></a>

## ✨ Features

| Feature | Description |
|---|---|
| Live radar sweep | Periodically refreshes the UI with results from native scan commands |
| Native scan inputs | Uses OS tools — `netsh`, `airport`, `nmcli`, `iwlist`; available fields vary by platform |
| Vendor identification | Manufacturer resolved via macvendors.com API, cached in `vendor_cache.json` |
| Color-coded security | Visual security level (WPA3, WPA2, WPA, WEP, OPEN) |
| Signal strength | dBm and percentage, with noise floor and SNR on supported platforms |
| Radio generation | WiFi 4/5/6/7 detection (802.11n/ac/ax/be) |
| Cipher detection | CCMP vs TKIP per access point |
| Network type | Infrastructure vs Ad-Hoc |
| New AP alerts | Alert when a new unknown network appears |
| CSV export | Download a full metadata snapshot |
| Platform branches | Implements Windows, macOS, and Linux scanning paths; hardware, permissions, tools, and OS output affect results |
| ETag caching | 304 Not Modified support to avoid wasted bandwidth |
| Auto-install | Flask and Flask-CORS are installed automatically if missing |

<a id="quick-start"></a>

## 🚀 Quick start

Run these commands from the `Wifi Radar` directory. The launchers install packages into the selected Python environment; the Unix launcher can retry with `--break-system-packages`. For controlled setup, prefer the manual route in a virtual environment.

### Windows

```bat
START_WINDOWS.bat
```

### macOS

```bash
bash START_UNIX.sh
```

### Linux

```bash
sudo bash START_UNIX.sh
```

### Manual

With your virtual environment activated, from `Wifi Radar`:

```bash
python -m pip install -r requirements.txt
python server.py
```

If Linux reports permission errors, review the native scanner's permissions before choosing to elevate the whole server.

Then open your browser at: **http://localhost:5000**

> **Network exposure:** `server.py` starts Flask with `host='0.0.0.0'` and enables CORS, so the dashboard and API are reachable from other devices on the same network, not only from `localhost`. Change the host to `127.0.0.1` in `app.run(...)` if you want it to be local-only, and do not run it on untrusted networks.

<a id="requirements"></a>

## 📦 Prerequisites and installation

- Python 3.8+
- Flask and Flask-CORS (auto-installed by launcher scripts)
- Wi-Fi adapter enabled in OS settings
- Any modern web browser
- Internet access for uncached vendor lookups. A lookup sends a full BSSID (MAC address) to `api.macvendors.com`; the result is cached by its vendor prefix (OUI), so not every access point needs a separate request. Cached vendors remain available offline.

## API Endpoints

| Endpoint | Description |
|---|---|
| `GET /` | Radar UI (index.html) |
| `GET /api/scan` | Live scan data as JSON (ETag supported) |
| `GET /api/export/csv` | Download current networks as a CSV file |
| `GET /api/debug` | Raw scan output and diagnostics |
| `GET /api/vendor_cache` | Vendor cache stats and contents |

## Platform Details

| OS | Primary Tool | Fallback |
|---|---|---|
| Windows | `netsh wlan show networks mode=Bssid` | State machine parser |
| macOS | `airport -s` | `system_profiler SPAirPortDataType` |
| Linux | `nmcli dev wifi list --rescan yes` | `iwlist scan` |

Linux scan permissions depend on NetworkManager/PolicyKit configuration and the selected tool; the `iwlist` fallback may require elevated privileges. Try the manual setup in an isolated environment first. The launcher suggests `sudo`, which also runs the Flask server with elevated privileges.

## Data Fields Per Network

| Field | Description |
|---|---|
| SSID | Network name |
| BSSID | MAC address |
| Vendor | Manufacturer (from macvendors.com, cached) |
| Signal (dBm / %) | Signal strength |
| Noise floor / SNR | Available on macOS and Linux |
| Channel / Band | 2.4 GHz / 5 GHz / 6 GHz |
| Security | OPEN / WEP / WPA / WPA2 / WPA3 / WPA2/WPA3 |
| Cipher | CCMP (strong) or TKIP (weak) |
| Radio type | WiFi 4/5/6/7 |
| Network type | Infrastructure or Ad-Hoc |

## Troubleshooting and limitations

- If backend requests fail, `index.html` can display generated demo networks with a `SERVER OFFLINE` / `Showing simulated data` banner. Those blips do not establish a successful native scan. Check server status and the banner before interpreting the display.
- Radar angle and radius come from `stable_pos(bssid)`, a hash of the MAC address. They are visual placement, not measured direction, physical distance, or device location.
- dBm can be estimated from signal percentage when the OS does not return it; missing platform fields and fallback defaults are not measurements. The macOS fallback includes a hardcoded security label.
- `/api/debug` exposes raw scan output. There is no authentication layer around the dashboard or API.
- Scan command output parsing is platform-dependent. A successful server start does not prove every field is available or accurate. Check native tool output and permissions if the network list is empty.

## Disclaimer

This tool is intended for educational and network diagnostic purposes only. Only scan networks you own or have explicit permission to scan.

---

<a id="file-structure"></a>

## 🏗️ Architecture

```text
Wifi Radar/
├── server.py              # Python backend — Wi-Fi scanner + Flask API
├── index.html             # Radar UI — pure HTML/CSS/JS
├── requirements.txt       # Python dependencies (flask, flask-cors)
├── vendor_cache.json      # Auto-generated vendor lookup cache
├── START_WINDOWS.bat      # Windows one-click launcher
└── START_UNIX.sh          # macOS / Linux launcher
```

<a id="related-projects"></a>

## 🔗 Related documentation

- [WiFi Scanner — command-line scan with pywifi](../Wifi%20Scanner/readme.md)
- [WiFi Profiles — saved Windows Wi-Fi networks](../Wifi%20Profiles/readme.md)
- [Port Scanner](../Port%20Scanner/readme.md)
- [Back to all Python projects](../README.md)

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python_codes/documentation/) · [Project overview](https://gcfernando.github.io/python_codes/) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
