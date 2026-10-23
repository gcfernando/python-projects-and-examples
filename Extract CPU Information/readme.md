# Get CPU Information in Python — psutil and py-cpuinfo Example

A short script that shows **how to get CPU information in Python**: processor brand, architecture, clock speed, and physical and logical core counts, using `psutil` and `py-cpuinfo`.

<a id="overview"></a>

## 🔎 Overview

This script uses the `psutil` and `py-cpuinfo` libraries to gather and print CPU details to the console, including brand name, architecture, clock speed, core counts, and an estimated temperature.

<a id="features"></a>

## ✨ Features

- CPU brand name and architecture
- cpuinfo version string
- Actual clock frequency (human-readable)
- Number of physical cores
- Number of logical cores (including hyper-threaded)
- Estimated temperature in °C (derived from current frequency)

<a id="requirements"></a>

## 📦 Prerequisites and installation

```text
psutil
py-cpuinfo
```

Install dependencies:

```bash
python -m pip install psutil py-cpuinfo
```

<a id="usage"></a>

## 💡 Usage

From the `Console_Code` folder:

```bash
python CPU.py
```

### Example Output

Values depend on your machine; the labels are printed exactly as below (including the script's `Actucal Hz` spelling).

```text
Processor Info
    Brand            : Intel(R) Core(TM) i7-10750H CPU @ 2.60GHz
    Architecture     : X86_64
    Version          : cpuinfo-9.0.0
    Actucal Hz       : 2.6000 GHz
    Physical Cores   : 6
    Logical Cores    : 12
    Temperature      : 41.0°C
```

<a id="file-structure"></a>

## 🏗️ Architecture

```text
Extract CPU Information/
└── Console_Code/
    └── CPU.py    # Main script
```

<a id="notes"></a>

## 🛠️ Troubleshooting and limitations

- Temperature is estimated based on the current CPU frequency (`freq / 100 + 15`). It is not a hardware sensor reading and should not be used to judge whether a CPU is overheating. On Linux, `psutil.sensors_temperatures()` can read real sensor values where the hardware exposes them.
- `psutil` and `cpuinfo` support Windows, macOS, and Linux.

<a id="related-projects"></a>

## 🔗 Related documentation

- [Health Monitor — live process memory dashboard](../Health%20Monitor/readme.md)
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python_codes/documentation/) · [Project overview](https://gcfernando.github.io/python_codes/) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
