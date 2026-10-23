# Python Process Memory Monitor — Possible Leak Alerts with psutil and Rich

A real-time terminal dashboard written in Python that watches the **memory usage of running processes** and flags ones whose memory keeps growing — a simple heuristic for spotting possible memory leaks.

<a id="overview"></a>

## 🔎 Overview

Health Monitor continuously tracks the memory usage of the top processes on your system and flags any that show consistent upward growth — a common sign of a memory leak. The live dashboard refreshes every second and color-codes each process with a clear status indicator.

<a id="features"></a>

## ✨ Features

- Live terminal dashboard powered by the `rich` library
- Tracks the top N processes by memory usage
- Flags possible memory leaks by observing consistent growth over a rolling window of snapshots
- Three status levels per process:
  - **OK** — neither growth threshold is currently met
  - **WATCH** — memory has grown by more than 25 MB across the recent snapshot history
  - **LEAK** — memory has increased on 10 or more consecutive intervals (at least 11 readings)
- Footer shows flagged process IDs or the application's "No leaks detected" message with a timestamp; that message only means no tracked process currently meets the heuristic
- Configurable number of processes to track and check interval via command-line arguments

<a id="requirements"></a>

## 📦 Prerequisites and installation

Use Python 3.10 or newer; the script uses runtime union type annotations such as `float | None`.

```text
psutil
rich
```

Install dependencies:

```bash
python -m pip install psutil rich
```

<a id="usage"></a>

## 💡 Usage

From the `Console_Code` folder:

```bash
# Run with defaults (top 15 processes, 1-second interval)
python health_monitor.py

# Monitor top 20 processes
python health_monitor.py --top 20

# Check every 5 seconds
python health_monitor.py --interval 5

# Combine options
python health_monitor.py -n 20 -i 5
```

### Arguments

| Argument | Short | Default | Description |
|---|---|---|---|
| `--top` | `-n` | 15 | Number of processes to display and track |
| `--interval` | `-i` | 1 | Seconds between each memory snapshot |

## Leak Detection Logic

| Parameter | Default | Description |
|---|---|---|
| Snapshot interval | 1 second | How often memory is sampled |
| `LEAK_THRESHOLD_MB` | 50 MB | WATCH is shown when growth exceeds half of this value (25 MB) |
| `LEAK_WINDOW` | 10 increases | Number of consecutive increases (of any size) that triggers LEAK |
| History length | 20 snapshots | Only the most recent 20 readings per process are kept |

These are heuristics, not proof of a leak: caches, garbage-collected runtimes, and applications that are legitimately loading data can also grow steadily. A LEAK alert requires 10 consecutive increases, with any increase size; the header's summary of "+50MB over 10 snapshots" does not match this implemented rule. Investigate flagged processes with a profiler before diagnosing a leak.

## Dashboard Columns

| Column | Description |
|---|---|
| PID | Process ID |
| Process Name | Name of the process |
| Current (MB) | Current resident memory usage in megabytes |
| Growth (MB) | Memory change since the oldest of the (up to 20) stored snapshots |
| Status | OK / WATCH / LEAK |

<a id="file-structure"></a>

## 🏗️ Architecture

```text
Health Monitor/
└── Console_Code/
    └── health_monitor.py    # Main script
```

<a id="notes"></a>

## 🛠️ Troubleshooting and limitations

- Press `Ctrl+C` to stop monitoring. The dashboard is cleared on exit.
- Processes that exit mid-session are automatically removed from tracking.
- Processes that cannot be read (e.g., protected system processes) are silently skipped.
- The top-N list is recalculated on every snapshot, so a process that drops out of the top N stops being tracked.
- Memory is the resident set size (RSS) reported by `psutil`.

The display labels memory as MB, but the source divides bytes by `1024 ** 2`, so the values are MiB. Tracking is limited to the selected top processes; a process that drops out of that set loses its stored history and growth streak.

<a id="related-projects"></a>

## 🔗 Related documentation

- [Extract CPU Information](../Extract%20CPU%20Information/readme.md)
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python_codes/documentation/) · [Project overview](https://gcfernando.github.io/python_codes/) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
