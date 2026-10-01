# Energy Consumption Demand Forecasting

A time-series forecasting project that predicts hourly electricity demand (MW) using calendar-based features and an XGBoost regression model.

## Project Overview

This project uses the **PJM East (PJME)** hourly electricity consumption dataset to forecast energy demand. The notebook explores demand patterns, creates time-based features, trains an XGBoost regressor, evaluates forecasts using RMSE, and analyses prediction errors.

### Objectives

- Explore hourly electricity demand over time
- Split the data into training and test periods
- Create calendar/time-series features from the datetime index
- Train an XGBoost regression model
- Evaluate forecast accuracy using RMSE
- Visualise actual vs predicted demand
- Identify the days with the largest prediction errors

## Dataset

**File:** `data/PJME_hourly.csv`

The dataset contains:

- `Datetime` — hourly timestamp
- `PJME_MW` — electricity demand in megawatts (MW)

Dataset size: **145,366 hourly observations**, covering **2002-01-01 to 2018-08-03**. There are no missing values in the supplied dataset.

## Methodology

### 1. Train/Test Split

The original notebook uses:

- **Training:** dates before 1 January 2015
- **Test:** dates from 1 January 2015 onwards

This preserves the chronological order of the time series and avoids randomly mixing future observations into the training data.

### 2. Feature Engineering

The notebook creates the following calendar features:

- `dayofyear`
- `hour`
- `dayofweek`
- `quarter`
- `month`
- `year`
- `dayofmonth`
- `weekofyear`

The model uses:

```text
dayofyear, hour, dayofweek, quarter, month, year
```

### 3. Model

The forecasting model is an **XGBoost XGBRegressor** with the following configuration from the notebook:

- Booster: `gbtree`
- Estimators: `1000`
- Maximum depth: `3`
- Learning rate: `0.01`
- Early stopping rounds: `50`
- Objective: regression

### 4. Evaluation

The main evaluation metric is **Root Mean Squared Error (RMSE)**.

The project also calculates absolute prediction error and identifies the 10 days with the highest mean absolute error.

## Repository Structure

```text
energy-consumption-demand-forecasting/
├── data/
│   └── PJME_hourly.csv
├── notebooks/
│   └── Energy_Consumption_Demand_Forecasting.ipynb
├── reports/
├── src/
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt
```

## Installation

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd energy-consumption-demand-forecasting
python -m venv .venv
```

Activate the environment:

### Windows

```bash
.venv\Scripts\activate
```

### macOS/Linux

```bash
source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

## Running the Project

Launch Jupyter Notebook:

```bash
jupyter notebook
```

Then open:

```text
notebooks/Energy_Consumption_Demand_Forecasting.ipynb
```

### Important notebook path change

The original notebook reads `/content/PJME_hourly.csv`, which is a Google Colab path. For this repository, change the data-loading line to:

```python
df = pd.read_csv('../data/PJME_hourly.csv')
```

when running the notebook from the `notebooks` directory.

## Results

The notebook calculates the final test-set RMSE when executed. The repository intentionally does not hard-code a result here because the value should be generated from the supplied notebook and dataset rather than copied as an unverified figure.

## Limitations and Future Improvements

The original notebook identifies several next steps:

- Use more robust time-series cross-validation
- Add weather-related variables
- Add holiday/calendar information

Additional improvements could include lag features, rolling statistics, hyperparameter tuning, and comparison with statistical forecasting models.

## Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- XGBoost
- Jupyter Notebook

## Author

**Ajay Kumar Bhogta**

MSc Business Analytics — University of Kent
