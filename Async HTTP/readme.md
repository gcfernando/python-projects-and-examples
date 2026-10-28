[Python projects](../README.md) · **HTTP and automation**

<a id="async-http-requests-in-python-with-aiohttp-and-asyncio--get-post-put-delete-example"></a>

# Async HTTP Requests in Python with aiohttp

An interactive command-line client that shows how to make **asynchronous HTTP requests in Python** with `asyncio` and `aiohttp` — sending GET, POST, PUT, and DELETE requests to a REST API and printing the JSON responses.

> **In this guide:** [Get started](#guide-prerequisites-and-installation) · [Walk through the example](#guide-usage) · [Understand the details](#guide-features) · [Check the limits](#guide-troubleshooting-and-limitations)

<a id="overview"></a>

## 🔎 Overview

This script demonstrates asynchronous HTTP communication by connecting to the Northwind sample REST API. It runs a loop that lets you repeatedly choose a request method, provide the necessary data, and view the JSON response — all using non-blocking I/O.

<a id="features"></a>

<a id="guide-features"></a>

## ✨ Features

- Supports GET, POST, PUT, and DELETE methods
- Asynchronous request handling via `aiohttp` and `asyncio`
- Interactive loop with an option to continue or exit after each request
- Pretty-printed JSON responses using `pprint`
- Targets the Northwind API's `/categories` resource for demonstration

<a id="requirements"></a>

<a id="guide-prerequisites-and-installation"></a>

## 📦 Prerequisites and installation

```text
aiohttp
```

> **Note:** `asyncio` and `pprint` are part of the Python standard library and do not require installation.

Install the external dependency:

```bash
python -m pip install aiohttp
```

<a id="usage"></a>

<a id="guide-usage"></a>

## 💡 Usage

From the `Console_Code` folder:

```bash
python HttpCall.py
```

The script uses `http://northwind.now.sh/api/` as its base URL. Availability, redirects, and write behavior of that external sample service are not guaranteed by this repository. Use an API you control before trying POST, PUT, or DELETE; those methods can mutate shared remote data. The base URL ends with `/` and request paths start with `/`, so the constructed URLs also contain a double slash.

### Example Session

```text
Enter Method (GET, POST, PUT, DELETE): GET
# → prints list of categories

More! (Y|N): Y

Enter Method (GET, POST, PUT, DELETE): POST
Enter Category Id: 10
Enter Category Name: Beverages
Enter Category Description: Soft drinks and teas
# → prints created category

More! (Y|N): N
```

### Supported Methods

| Method | Action | Input Required |
|---|---|---|
| GET | Retrieve all categories | None |
| POST | Create a new category | ID, Name, Description |
| PUT | Update an existing category | ID, Name, Description |
| DELETE | Delete a category | ID |

<a id="file-structure"></a>

## 🏗️ Architecture

```text
Async HTTP/
└── Console_Code/
    └── HttpCall.py    # Main script
```

<a id="notes"></a>

<a id="guide-troubleshooting-and-limitations"></a>

## 🛠️ Troubleshooting and limitations

- Each request opens its own `aiohttp.ClientSession`. That keeps the demo short; in larger programs, create one session and reuse it for many requests.
- Every response is parsed as JSON without `raise_for_status()` or a check for an empty body. HTML errors or a successful empty DELETE response can raise a JSON parsing error. The interactive `input()` calls block even though request I/O is asynchronous.
- Entering any method other than GET, POST, PUT, or DELETE ends the loop.

<a id="related-projects"></a>

## 🔗 Related documentation

- [Internet Speed Test](https://gcfernando.github.io/python-projects-and-examples/Internet%20Speed%20Test/)
- [Port Scanner](https://gcfernando.github.io/python-projects-and-examples/Port%20Scanner/)
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python-projects-and-examples/documentation/) · [Project overview](../README.md) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
