# Internet Speed Test in Python — speedtest-cli Example

A short Python script that **tests your internet speed** — download, upload, and ping — using the `speedtest-cli` library and Speedtest.net servers.

<a id="overview"></a>

## 🔎 Overview

This script connects to the best available Speedtest.net server, runs a full speed test, and prints the results to the console.

<a id="features"></a>

## ✨ Features

- Automatically selects the best available test server
- Measures download speed (Mbps)
- Measures upload speed (Mbps)
- Reports ping latency (ms)
- Displays the selected server's host, country, and sponsor

<a id="requirements"></a>

## 📦 Prerequisites and installation

```text
speedtest-cli
```

Install the dependency:

```bash
python -m pip install speedtest-cli
```

<a id="usage"></a>

## 💡 Usage

From the `Console_Code` folder:

```bash
python SpeedTest.py
```

### Example Output

The numbers below are illustrative; the text matches what the script prints.

```text
Loading servers
Calulating download speed...
Calulating upload speed...
Calulating ping result...

Choose best server example.server.net located at United States Sponsor by Example ISP
Download    : 95.42 Mbps
Upload      : 48.17 Mbps
Ping        : 12.34 ms
```

## Note on the reported units

`speedtest-cli` returns speeds in bits per second. The script's `bytes_to_mb` helper divides by powers of **1024** and always appends `Mbps`, so a result shown as "90.6 Mbps" is about 95 megabits per second in the usual decimal sense (roughly 4.6% higher). Very slow connections, below 1,048,576 bit/s, are shown in kilobit units but are still labelled `Mbps`. Dividing by `1_000_000` gives standard Mbps.

<a id="file-structure"></a>

## 🏗️ Architecture

```text
Internet Speed Test/
└── Console_Code/
    └── SpeedTest.py    # Main script
```

<a id="related-projects"></a>

## 🔗 Related documentation

- [FixNetwork — Windows network reset script](../FixNetwork/readme.md)
- [WiFi Scanner](https://gcfernando.github.io/python-projects-and-examples/Wifi%20Scanner/)
- [Get your public IP address in C#](https://github.com/gcfernando/csharp-dotnet-examples/tree/main/PublicIP)
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python-projects-and-examples/documentation/) · [Project overview](../README.md) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
