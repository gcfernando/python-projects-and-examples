# COVID-19 Time Series Forecasting in Python — auto-ARIMA and SARIMAX Example

A **time series forecasting** script in Python that predicts daily COVID-19 cases for a country using `pmdarima.auto_arima` for model selection and `statsmodels` SARIMAX for fitting — a worked example of the ADF stationarity test, seasonal ARIMA, in-sample validation, and future forecasts with confidence intervals.

<a id="overview"></a>

## 🔎 Overview

This script downloads daily COVID-19 case data, performs stationarity analysis, automatically selects the best ARIMA/SARIMA model, fits it, and generates both an in-sample static forecast and a future forecast for the next N days. All results are visualized with `matplotlib`.

<a id="features"></a>

## ✨ Features

- Automatically downloads COVID-19 daily case data if not cached locally
- Augmented Dickey-Fuller (ADF) stationarity test with detailed output
- Rolling mean and standard deviation visualization for stationarity inspection
- Automatic ARIMA/SARIMA parameter selection via `pmdarima.auto_arima`
- SARIMAX model fitting using `statsmodels`
- Static (in-sample) forecast for the last 120 days
- Future forecast for the next N days with confidence intervals
- All plots displayed with gridlines, auto-scaled axes, and monthly date formatting

<a id="requirements"></a>

## 📦 Prerequisites and installation

```text
numpy
pandas
pmdarima
covid_daily
statsmodels
matplotlib
```

Install dependencies:

```bash
python -m pip install numpy pandas pmdarima covid_daily statsmodels matplotlib
```

<a id="configuration"></a>

## ⚙️ Configuration

Edit the variables at the top of `CovidForecast.py`:

| Variable | Default | Description |
|---|---|---|
| `country` | `'india'` | Country to forecast (`'india'`, `'brazil'`, etc.) |
| `stepCount` | `50` | Number of future days to forecast |
| `frequency` | `'D'` | Time series frequency (`'D'` = daily) |

<a id="usage"></a>

## 💡 Usage

From the `Console_Code` folder:

```bash
python CovidForecast.py
```

On first run, a CSV file (e.g., `india_corvid19.csv`) is downloaded and saved in the working directory. Subsequent runs load from this cached file.

### Output

1. ADF test results printed to console
2. Rolling statistics chart (stationarity check)
3. Static forecast chart (last 120 days vs. in-sample prediction)
4. Future forecast chart with confidence interval shading and a table of predicted values

## How It Works

1. Data is loaded and resampled to daily frequency
2. A 12-period rolling detrend and differencing step produces a separate series for the stationarity diagnostics
3. `auto_arima` searches for the best ARIMA order using AIC and an ADF test for differencing
4. The SARIMAX model is fit with Powell optimization
5. Static in-sample predictions (`dynamic=False`) and future forecasts are generated and plotted

<a id="file-structure"></a>

## 🏗️ Architecture

```text
COVID Forecast/
└── Console_Code/
    └── CovidForecast.py    # Main script
```

<a id="notes"></a>

## 🛠️ Troubleshooting and limitations

- The transformed series is used for ADF testing and the rolling-statistics chart. Both `auto_arima` and SARIMAX are fitted to the original `y` series, not the detrended series. The in-sample chart is not an independent held-out evaluation.
- The `dataset[newColumn].astype(float)` result is not assigned back; provide numeric values in a cached CSV. The static forecast needs at least 120 observations.
- `auto_arima` is called with `seasonal=True` and `m=12`, so it looks for a 12-step seasonal pattern in the daily series. Weekly reporting patterns would correspond to `m=7`; try both if you adapt the script.
- The data download depends on the third-party `covid_daily` package and the site it reads from. If the download fails, place a CSV with the same structure at `<country>_corvid19.csv` and the script will load it instead.
- The forecasts are a modelling exercise, not public-health guidance.

<a id="related-projects"></a>

## 🔗 Related documentation

- [Salary prediction with scikit-learn linear regression](../Salary/readme.md)
- [Machine-learning examples overview](../README.md)
- [Machine-learning datasets for practice](https://github.com/gcfernando/machine-learning-practice-datasets)
- [Back to all Python projects](../../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python-projects-and-examples/documentation/) · [Project overview](../../README.md) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
