# Python Wi-Fi Scanner — List Nearby Networks with pywifi

A short Python script that **scans for nearby Wi-Fi networks** with the `pywifi` library and prints each network's SSID, BSSID, signal strength, frequency, and security type.

<a id="overview"></a>

## 🔎 Overview

This script initializes the system's first Wi-Fi interface, triggers a scan, and then reads the results to display network details including SSID, BSSID, signal strength, frequency, and security mode for each discovered access point.

<a id="features"></a>

## ✨ Features

- Scans all visible Wi-Fi networks
- Displays for each network:
  - SSID (network name)
  - BSSID (access point MAC address)
  - Signal strength (dBm)
  - Frequency (MHz)
  - AKM security mode (OPEN, WPA-PSK, WPA2-PSK, WPA-EAP, WPA2-EAP, UNKNOWN)
  - Authentication mode
- Error handling inside the scan/output block; interface initialization happens before that block

<a id="requirements"></a>

## 📦 Prerequisites and installation

```text
pywifi
```

Install the dependency:

```bash
python -m pip install pywifi
```

> On Windows, `pywifi` may also require `comtypes`. Install with:
> ```bash
> pip install pywifi comtypes
> ```

<a id="usage"></a>

## 💡 Usage

From the `Console_Code` folder:

```bash
python Wifi_Scanner.py
```

### Example Output

Illustrative Windows output for a WPA2-Personal network, including the existing unit and security-label defects described in [known issues](#known-issues). Actual values depend on the adapter and scan. With the default integer authentication value `0`, no `Security Auth` line is printed.

```text
SSID: HomeNetwork
BSSID: AA:BB:CC:DD:EE:FF
Signal Strength (dBm): -55
Frequency (MHz): 2.412
Security Mode: WPA2-EAP
```

## Known issues

- **Authentication value is scalar.** The [upstream Profile definition](https://github.com/awkman/pywifi/blob/master/pywifi/profile.py) stores `auth` as an integer, while this script indexes `network.auth[0]`. The default `0` skips the branch; a nonzero integer raises a type error and ends the scan/output block. Use the documented integer constants when adapting the display rather than treating authentication as a list.
- **Security labels are shifted.** `pywifi` numbers its AKM types as 0 = none, 1 = WPA, 2 = WPA-PSK, 3 = WPA2, 4 = WPA2-PSK, 5 = unknown, but the script's `akm_modes` list is ordered `OPEN, WPA-PSK, WPA-EAP, WPA2-PSK, WPA2-EAP, UNKNOWN`. As a result, a typical WPA2-Personal network (type 4) is printed as `WPA2-EAP`. Reordering the list to `['OPEN', 'WPA-EAP', 'WPA-PSK', 'WPA2-EAP', 'WPA2-PSK', 'UNKNOWN']` matches `pywifi`'s constants.
- **Frequency units.** On Windows, `pywifi` returns the channel centre frequency in kHz, so `network.freq / 1000000` prints gigahertz (for example `2.412`) under a "MHz" label. Dividing by `1000` gives MHz. Other platforms may report frequency in different units.

<a id="file-structure"></a>

## 🏗️ Architecture

```text
Wifi Scanner/
└── Console_Code/
    └── Wifi_Scanner.py    # Main script
```

<a id="notes"></a>

## 🛠️ Troubleshooting and limitations

- If no Wi-Fi interface exists, `interfaces()[0]` fails before the `try` block and its friendly error handler cannot run.
- The script always uses the first Wi-Fi interface (`interfaces()[0]`). Systems with multiple Wi-Fi adapters will use whichever is first in the list.
- `pywifi` support varies by platform. It works on Windows and Linux; macOS support is limited.
- On Linux, you may need to run the script with `sudo` for full scan access.
- `scan()` starts an asynchronous scan, and the script reads `scan_results()` immediately afterwards. Waiting a few seconds between the two calls (for example `time.sleep(3)`) can return a more complete list.

<a id="related-projects"></a>

## 🔗 Related documentation

- [WiFi Radar — live Wi-Fi dashboard](../Wifi%20Radar/readme.md)
- [WiFi Profiles — saved Windows Wi-Fi networks](../Wifi%20Profiles/readme.md)
- [Internet Speed Test](../Internet%20Speed%20Test/readme.md)
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python_codes/documentation/) · [Project overview](https://gcfernando.github.io/python_codes/) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
