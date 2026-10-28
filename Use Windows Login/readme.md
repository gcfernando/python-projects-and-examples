[Python projects](../README.md) · **Windows integration**

<a id="verify-windows-credentials-in-python--pywin32-logonuser-example"></a>

# Check Windows Credentials with Python and pywin32

A short Python script that shows **how to check a Windows username and password from Python** with `win32security.LogonUser` (pywin32), as a simple Windows credential gate for a script or tool.

> **In this guide:** [Get started](#guide-prerequisites-and-installation) · [Walk through the example](#guide-usage) · [Understand the details](#guide-features) · [Check the limits](#guide-troubleshooting-and-limitations)

<a id="overview"></a>

## 🔎 Overview

This script uses `getpass` to securely collect the current user's Windows password (without echoing it to the terminal) and then verifies it via the Win32 `LogonUser` API. This is a credential-check demonstration. It prints the result; the sample does not implement application authorization or session management.

<a id="features"></a>

<a id="guide-features"></a>

## ✨ Features

- Automatically detects the currently logged-in Windows username
- Prompts for the password securely (input is not displayed)
- Verifies credentials against the local Windows account using `win32security.LogonUser`
- Prints a success or failure message; failure does not call `sys.exit()` or set a nonzero exit status

<a id="requirements"></a>

<a id="guide-prerequisites-and-installation"></a>

## 📦 Prerequisites and installation

```text
pywin32
```

Install the dependency:

```bash
python -m pip install pywin32
```

> The script imports Python's built-in `getpass` module, so no extra package is needed for the password prompt. `pywin32` provides the `win32security` module required for Windows authentication.

<a id="usage"></a>

<a id="guide-usage"></a>

## 💡 Usage

From the `Console_Code` folder:

```bash
python Use_Win_Login.py
```

### Example Session

```text
Enter your Windows password:
Login successful!
```

Or, if the password is incorrect:

```text
Enter your Windows password:
Login failed. Exiting application.
```

## How It Works

1. `getpass.getuser()` retrieves the current Windows username from the environment.
2. `getpass.getpass()` securely prompts for a password without displaying it.
3. `win32security.LogonUser()` attempts a network logon with the provided credentials.
   - If successful: prints `Login successful!`
   - If it raises `win32security.error`: prints `Login failed. Exiting application.`

<a id="file-structure"></a>

## 🏗️ Architecture

```text
Use Windows Login/
└── Console_Code/
    └── Use_Win_Login.py    # Main script
```

<a id="notes"></a>

<a id="guide-troubleshooting-and-limitations"></a>

## 🛠️ Troubleshooting and limitations

- This script is Windows-only. `win32security` is not available on macOS or Linux.
- The `LOGON32_LOGON_NETWORK` logon type is used, which validates credentials without creating a full user session.
- The domain argument is `None`. Microsoft's `LogonUser` documentation recommends the UPN format (`user@domain`) for the username in that case, so domain accounts may need the username adjusted.
- Accounts that sign in with a Microsoft account, PIN, or Windows Hello may need the Microsoft account password rather than the PIN. Repeated failed attempts count towards account lockout policies.

<a id="related-projects"></a>

## 🔗 Related documentation

- [Password Generator and Strength Checker](https://gcfernando.github.io/python-projects-and-examples/Password%20Utility/)
- [WiFi Profiles — Windows Wi-Fi utility](https://gcfernando.github.io/python-projects-and-examples/Wifi%20Profiles/)
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python-projects-and-examples/documentation/) · [Project overview](../README.md) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
