[Python projects](../README.md) · **Python fundamentals**

<a id="how-to-create-a-custom-exception-in-python--minimal-example"></a>

# Create and Catch a Custom Exception in Python

A minimal Python example demonstrating **how to define, raise, and catch a custom exception class** by subclassing `Exception`.

> **In this guide:** [Walk through the example](#guide-usage) · [Understand the details](#guide-architecture) · [Check the limits](#guide-troubleshooting-and-limitations)

<a id="overview"></a>

## 🔎 Overview

This script shows the pattern for creating a user-defined exception in Python by subclassing the built-in `Exception` class. It demonstrates how to raise the custom exception under a specific condition and catch it with a `try/except` block.

<a id="usage"></a>

<a id="guide-usage"></a>

## 💡 Usage

From the `Console_Code` folder:

```bash
python CustomException.py
```

**Output** (confirmed by running the script):
```text
Something went wrong
```

## How It Works

1. `CustomException` is defined as a subclass of `Exception`, accepting a `message` parameter.
2. `some_function()` raises `CustomException` when a condition is met (`x < y`).
3. The exception is caught in a `try/except` block, and the message is printed.

## Code Example

```python
class CustomException(Exception):
    def __init__(self, message):
        super().__init__(message)
        self.message = message

def some_function():
    x = 5
    y = 6
    if x < y:
        raise CustomException("Something went wrong")

try:
    some_function()
except CustomException as e:
    print(e.message)
```

## FAQ

**Do I need to store `message` on the exception?**
No — `str(e)` already returns the message passed to `super().__init__(message)`. Storing it as `self.message` simply makes it available as a named attribute, which is handy when you add more fields (such as an error code).

**Should custom exceptions inherit from `Exception` or `BaseException`?**
From `Exception` (or one of its subclasses). `BaseException` is reserved for exceptions such as `KeyboardInterrupt` and `SystemExit` that ordinary `except Exception` blocks should not catch.

<a id="file-structure"></a>

<a id="guide-architecture"></a>

## 🏗️ Architecture

```text
Custom Exception/
└── Console_Code/
    └── CustomException.py    # Main script
```

<a id="notes"></a>

<a id="guide-troubleshooting-and-limitations"></a>

## 🛠️ Troubleshooting and limitations

- No external dependencies required — uses only Python built-ins.
- The script includes a discussion in the docstring about when it is appropriate to make a custom exception serializable (relevant for distributed systems where exceptions may be passed across process boundaries).

<a id="related-projects"></a>

## 🔗 Related documentation

- [Object Clone — deep copy example](https://gcfernando.github.io/python-projects-and-examples/Object%20Clone/)
- [Python dbm database example](../Database/README.md)
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python-projects-and-examples/documentation/) · [Project overview](../README.md) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
