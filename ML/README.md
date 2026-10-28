[Python projects](../README.md) · **Machine learning**

<a id="python-machine-learning-examples--arimasarimax-time-series-forecasting-and-linear-regression"></a>

# Python Machine Learning: Forecasting and Regression

A collection of beginner-friendly **machine learning projects built with Python**: a **COVID-19 time-series forecast** using auto-ARIMA and SARIMAX (`pmdarima`, `statsmodels`), and a **salary prediction model** using scikit-learn linear regression with a separate training and inference workflow.

> **In this guide:** [Understand the details](#guide-architecture) · [Projects](#guide-projects) · [Related documentation](#guide-related-documentation)

---

<a id="guide-projects"></a>

## Projects

### 1. COVID Forecast

**Location:** `COVID Forecast/Console_Code/CovidForecast.py`

A time series forecasting script that predicts the number of daily COVID-19 cases for a country using SARIMAX and auto-ARIMA models.

#### How It Works

1. Downloads daily COVID-19 case data via the `covid_daily` package (if not already cached locally as a CSV)
2. Detrends and differences a copy of the series for stationarity diagnostics (model fitting still uses the original series)
3. Performs the **Augmented Dickey-Fuller (ADF)** test and rolling-statistics diagnostics on that transformed series
4. Automatically fits the best ARIMA/SARIMA model using `pmdarima.auto_arima`
5. Fits the chosen model using `statsmodels.SARIMAX`
6. Generates a **static forecast** (in-sample) and a **future forecast** for the next N days
7. Displays all charts using `matplotlib`

#### Configuration

Edit these variables at the top of the script:

| Variable | Default | Description |
|---|---|---|
| `country` | `'india'` | Country to forecast (`'india'`, `'brazil'`, etc.) |
| `stepCount` | `50` | Number of future days to forecast |

#### Requirements

```text
numpy
pandas
pmdarima
covid_daily
statsmodels
matplotlib
```

```bash
python -m pip install numpy pandas pmdarima covid_daily statsmodels matplotlib
```

#### Usage

```bash
cd "COVID Forecast/Console_Code"
python CovidForecast.py
```

The downloaded data is cached as `<country>_corvid19.csv` in the working directory, so later runs reuse it instead of downloading again.

---

### 2. Salary Prediction

**Location:** `Salary/`

A linear regression pipeline that predicts salary based on years of experience.

#### Sub-projects

| File | Purpose |
|---|---|
| `Model Builder/builder.py` | Trains the model and saves it to disk |
| `Prediction/prediction.py` | Loads the saved model and predicts salary from user input |

#### Model Builder Pipeline (`builder.py`)

1. Load data from `Source/Salary.csv`
2. Remove duplicate rows
3. Drop columns with more than 50% missing values; fill remaining nulls with column mean
4. Scale `years_experience` using `StandardScaler`
5. Split into train (80%) and test (20%) sets
6. Train a `LinearRegression` model
7. Evaluate using R² score and Mean Squared Error
8. Save the model and scaler to `Source/salary.pkl` and `Source/scaler.pkl` if R² > 0.95

The current demo fits preprocessing before the train/test split, allowing held-out data to influence it. Split first and fit preprocessing on training data when adapting it for independent evaluation; see the [salary example's limitations](Salary/readme.md#notes). The R² threshold controls saving and does not guarantee accuracy on new data.

#### Prediction Inference (`prediction.py`)

1. Load the saved model and scaler from disk
2. Prompt the user for years of experience
3. Scale the input using the saved scaler
4. Predict and display the salary

#### Requirements

```text
pandas
scikit-learn
joblib
numpy
```

```bash
python -m pip install pandas scikit-learn joblib numpy
```

#### Usage

Both scripts use paths relative to the working directory (`./Source/...`), so run them from the `Salary` folder. A trained `salary.pkl` and `scaler.pkl` are already included in `Salary/Source/`, so you can run inference without training first.

**Train the model:**
```bash
cd Salary
python "Model Builder/builder.py"
```

**Run inference:**
```bash
cd Salary
python "Prediction/prediction.py"
```

**Inference session format:**
```text
Enter Years of Experience: 5
Predicted Salary for 5.0 years of experience: $<predicted amount>
```

---

<a id="folder-structure"></a>

<a id="guide-architecture"></a>

## 🏗️ Architecture

```text
ML/
├── COVID Forecast/
│   └── Console_Code/
│       └── CovidForecast.py       # Time series forecasting script
└── Salary/
    ├── Model Builder/
    │   └── builder.py             # Model training pipeline
    ├── Prediction/
    │   └── prediction.py          # Inference script
    └── Source/
        ├── Salary.csv             # Training data
        ├── salary.pkl             # Saved LinearRegression model
        └── scaler.pkl             # Saved StandardScaler
```

<a id="related"></a>

<a id="guide-related-documentation"></a>

## 🔗 Related documentation

- [Machine-learning datasets](https://github.com/gcfernando/machine-learning-practice-datasets) — more datasets for regression, classification, and forecasting practice
- [Back to all Python projects](../README.md)

---

## Documentation links

[Read all Python Projects and Code Examples guides online](https://gcfernando.github.io/python-projects-and-examples/documentation/) · [Project overview](../README.md) · [All developer projects](https://gcfernando.github.io/gcfernando/projects/)
