# Python Port Scanner — Multithreaded TCP Scanner with IPv6, Banners and JSON Output

A fast, multithreaded **TCP port scanner written in pure Python** (standard library only). It resolves IPv4 or IPv6 hosts, reports open TCP ports, can read service banners, and can emit JSON for automation. Internal closed/filtered classification has a platform limitation described below.

> **Only scan systems you own or have explicit written permission to test.**
> Unauthorized scanning may violate computer-misuse laws in your jurisdiction.

<a id="features"></a>

## ✨ Features

- **IPv4 and IPv6** — resolves hostnames via `getaddrinfo`, selects an IPv4 result when available, otherwise an IPv6 result; it scans one resolved address
- **Flexible port specification** — single ports, ranges, lists, or any mix: `80`, `1-1024`, `22,80,443`, `1-100,8080`
- **Open-port output** — internal workers classify results, while CLI and JSON output contain only open ports
- **Banner grabbing** — optional service-banner read on open ports
- **Streamed output** — open ports are printed as they are discovered
- **JSON mode** — machine-readable output for piping into other tools
- **Graceful Ctrl+C** — requests cancellation of queued work and exits with code 130; in-flight connections may delay exit
- **Configurable** — timeout, concurrency, and port range are all tunable from the CLI

<a id="requirements"></a>

## 📦 Prerequisites and installation

- Python **3.10** or newer
- No external packages

<a id="usage"></a>

## 💡 Usage

Run from the `Port Scanner/Console_Code` directory:

```bash
python portscan.py <target> [options]
```

### Examples

`example.com` below is a placeholder — replace it with a host you own or are authorized to scan, such as `127.0.0.1` for your own machine.

```bash
# Scan default ports 1-1024
python portscan.py example.com

# Scan all ports
python portscan.py example.com -p 1-65535

# Scan specific ports
python portscan.py example.com -p 22,80,443

# Mixed range and singletons
python portscan.py example.com -p 1-100,443,8000-8100

# Faster scan
python portscan.py example.com -p 1-65535 -c 500 -t 0.5

# IPv6 target
python portscan.py ::1 -p 80,443

# Banner grabbing
python portscan.py example.com -p 22,80,443 --banner

# JSON output
python portscan.py example.com -p 1-1024 --json > results.json

# Verbose/debug logging
python portscan.py example.com -v
```

## CLI Options

| Flag | Default | Description |
|---|---|---|
| `target` | — | Hostname, IPv4, or IPv6 address (required) |
| `-p`, `--ports` | `1-1024` | Port specification |
| `-t`, `--timeout` | `1.0` | Per-port connection timeout (seconds) |
| `-c`, `--concurrency` | `200` | Maximum concurrent connections |
| `--banner` | off | Attempt to read a service banner from open ports |
| `--json` | off | Emit results as a JSON document on stdout |
| `-v`, `--verbose` | off | Enable debug logging on stderr |

## Output Formats

### Human-readable (default)

Illustrative output (addresses and open ports depend on the target):

```text
14:32:01 [INFO] Target: example.com -> 93.184.216.34 (IPv4)
14:32:01 [INFO] Scanning 1024 port(s) with concurrency=200, timeout=1.00s
  22     open   (ssh)
  80     open   (http)
  443    open   (https)
14:32:04 [INFO] Scan complete. 3 open port(s) found.
```

### JSON (`--json`)

```json
{
  "target": "example.com",
  "ip": "93.184.216.34",
  "family": "IPv4",
  "scanned": 1024,
  "open": [
    { "port": 22,  "state": "open", "service": "ssh",   "banner": null },
    { "port": 80,  "state": "open", "service": "http",  "banner": null },
    { "port": 443, "state": "open", "service": "https", "banner": null }
  ]
}
```

## Port States

| State | Meaning |
|---|---|
| `open` | Service accepted the TCP handshake |
| `closed` | Host actively refused the connection |
| `filtered` | Timeout, most nonzero connection errors, or an OS error; not proof of a firewall |

Only Linux error code `111` is recognized as `closed`. For example, Windows refusal code `10061` is classified internally as `filtered`. Neither closed nor filtered entries are emitted by the CLI, so an empty `open` array does not distinguish those conditions.

The output above is illustrative. Service names come from the operating system's services database (`socket.getservbyport`), so the same port can be labelled differently on different systems (for example, port 135 appears as `epmap` on Windows).

## Exit Codes

| Code | Meaning |
|---|---|
| `0` | Scan completed successfully |
| `1` | Unexpected error during scan |
| `2` | Invalid arguments, port specification, concurrency, or target resolution |
| `130` | Interrupted by user (Ctrl+C) |

## FAQ

**Is this a replacement for Nmap?**
No. It performs TCP connect scans only (no SYN, UDP, OS, or version detection). It is a readable example of a concurrent scanner and a lightweight tool for quick checks.

**Why are some ports shown as `filtered`?**
The CLI does not print filtered entries. Internally the worker uses that label for timeouts and most connection errors, including refusals on some operating systems. Increase `--timeout` for slow connections, but do not interpret this label as a reliable firewall diagnosis.

<a id="file-structure"></a>

## 🏗️ Architecture

```text
Port Scanner/
└── Console_Code/
    └── portscan.py    # Main script
```

Resolution does not retry another address after a connection fails. The JSON `scanned` value is the number of requested ports, including when interrupted; it is not a verified count of completed probes. Use a positive `--timeout`: the CLI does not validate that constraint before creating sockets.

<a id="related-projects"></a>

## 🔗 Related documentation

- [WiFi Radar — Flask Wi-Fi scanner dashboard](../Wifi%20Radar/readme.md)
- [Linux command reference for cybersecurity](https://github.com/gcfernando/other_codes/tree/main/Linux_Commands)
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python_codes/documentation/) · [Project overview](https://gcfernando.github.io/python_codes/) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
