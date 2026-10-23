# Deep Copy vs Shallow Copy in Python — copy.deepcopy() Example

A minimal example of **cloning a Python object with `copy.deepcopy()`**, showing that changes to the original do not affect the copy.

<a id="overview"></a>

## 🔎 Overview

This script creates an instance of a custom class, clones it with `copy.deepcopy()`, then reassigns the original’s integer attribute. The copied instance retains its original value. The example demonstrates separate instances; it does not exercise nested mutable state or compare shallow copying directly.

<a id="requirements"></a>

## 📦 Prerequisites and installation

No external dependencies. `copy` is part of the Python standard library.

<a id="usage"></a>

## 💡 Usage

From the `Console_Code` folder:

```bash
python CloneObject.py
```

**Output:**
```text
20
10
```

## How It Works

```python
import copy

class MyClass:
    def __init__(self, x):
        self.x = x

original_object = MyClass(10)
cloned_object = copy.deepcopy(original_object)

original_object.x = 20

print(original_object.x)   # 20
print(cloned_object.x)     # 10 — unchanged
```

For this `MyClass`, `deepcopy` creates a separate instance; assigning `20` to the original instance's integer attribute leaves the copied attribute at `10`. This script does not itself compare nested mutable attributes or a shallow copy. Copy behavior for other classes can depend on their custom copy hooks.

<a id="file-structure"></a>

## 🏗️ Architecture

```text
Object Clone/
└── Console_Code/
    └── CloneObject.py    # Main script
```

<a id="notes"></a>

## 🛠️ Troubleshooting and limitations

- Use `copy.copy()` for a **shallow copy**, which only copies the top-level object (nested mutable objects are still shared).
- Use `copy.deepcopy()` for a **deep copy**, which recursively copies supported mutable contents — suitable when the object contains lists, dicts, or other mutable attributes.
- In this particular example, `x` is an integer (immutable), so `copy.copy()` would give the same result. The difference appears when an attribute is mutable — for example, if `x` were a list and you appended to `original_object.x`, a shallow copy would see the change and a deep copy would not.

<a id="related-projects"></a>

## 🔗 Related documentation

- [Custom Exception](../Custom%20Exception/readme.md)
- [Python dbm database example](../Database/README.md)
- [Python OOP and dunder methods guides](https://github.com/gcfernando/document)
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python_codes/documentation/) · [Project overview](https://gcfernando.github.io/python_codes/) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
