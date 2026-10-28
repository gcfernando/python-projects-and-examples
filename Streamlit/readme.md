[Python projects](../README.md) · **Interactive data apps**

<a id="streamlit-example-app-in-python--widgets-dataframes-and-charts"></a>

# Streamlit in Python — Widgets, DataFrames and Charts

A single-file **Streamlit example app** in Python that demonstrates sidebar input widgets, a pandas DataFrame, a matplotlib histogram, and Streamlit's native line and area charts — a quick way to learn how to build an interactive data web app without writing HTML or JavaScript.

> **In this guide:** [Get started](#guide-prerequisites-and-installation) · [Walk through the example](#guide-usage) · [Understand the details](#guide-features)

<a id="overview"></a>

## 🔎 Overview

This app serves as a showcase of Streamlit's core capabilities. Users can interact with various sidebar controls, view their selections displayed in the main area, explore a dynamically generated data table, and see multiple chart types — all in a single-page web interface.

<a id="features"></a>

<a id="guide-features"></a>

## ✨ Features

- **Sidebar widgets:**
  - Slider (age range selection)
  - Text input (name)
  - Selectbox (gender)
  - Multiselect (hobbies)
  - Date input (date of birth)
  - Number input (salary)
  - Checkbox (terms agreement)
  - Radio buttons (feedback source)

- **Main area:**
  - Display of all user inputs
  - Dynamic DataFrame combining user input with sample data
  - Age distribution histogram (matplotlib)
  - Salary-vs-age line chart (Streamlit native)
  - Salary-vs-age area chart (Streamlit native)
  - Conditional "Show More Info" section via checkbox

<a id="requirements"></a>

<a id="guide-prerequisites-and-installation"></a>

## 📦 Prerequisites and installation

```text
streamlit
pandas
numpy
matplotlib
```

Install dependencies:

```bash
python -m pip install streamlit pandas numpy matplotlib
```

<a id="usage"></a>

<a id="guide-usage"></a>

## 💡 Usage

From the `Console_Code` folder:

```bash
streamlit run streamlit_app.py
```

If the above command does not work:

```bash
python -m streamlit run streamlit_app.py
```

Streamlit normally serves at `http://localhost:8501`; use the URL printed by the CLI if its configuration or available port differs. Browser opening depends on the runtime environment.

The age-range slider is displayed in the summary but does not filter the table. The entered name, gender, salary and hobbies populate one sample row; its age is regenerated randomly on each rerun. No persistence or authentication is implemented.

## How Streamlit Runs the App

Streamlit re-runs the whole script from top to bottom every time a widget changes. Each widget call (for example `st.sidebar.slider`) returns its current value, so the page always reflects the latest inputs without callbacks.

<a id="file-structure"></a>

## 🏗️ Architecture

```text
Streamlit/
└── Console_Code/
    └── streamlit_app.py    # Main Streamlit application
```

<a id="related-projects"></a>

## 🔗 Related documentation

- [Local AI chat app with Ollama and Streamlit](https://github.com/gcfernando/developer-guides-and-cheatsheets/blob/main/local_ai_learning_lab.md)
- [WiFi Radar — Flask web dashboard](https://gcfernando.github.io/python-projects-and-examples/Wifi%20Radar/guide.html)
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python-projects-and-examples/documentation/) · [Project overview](../README.md) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
