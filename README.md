# Time-Series Forecasting: Energy Consumption (PJM East)

## Project Overview
This project focuses on forecasting hourly energy consumption in the PJM East region using historical data. The goal is to predict energy usage (in MW) for a given future date. By default, the prediction function returns the forecast for today, but it can be extended to any target date.

> **Note:** This project is inspired by Rob Mulla, who provided the original PJM East dataset on Kaggle.

---

## Dataset
- **File:** `PJME_hourly.csv`
- **Source:** Historical PJM East hourly energy consumption data (via Kaggle)
- **Target variable:** Energy consumption in MW
- **Data split:**  
  - 80% Training  
  - 10% Validation  
  - 10% Testing

---

## Key Findings

The PJM East energy consumption data shows clear temporal patterns:

| Pattern Type | Observation |
|--------------|------------|
| **Daily pattern** | Energy usage is **lowest between 12am–6am** and peaks around **6pm–9pm**, reflecting typical human and industrial activity. |
| **Weekly pattern** | Weekdays have slightly higher consumption than weekends due to commercial and industrial usage. |
| **Monthly / Seasonal pattern** | Usage peaks in **summer (June–August)** and **winter (Dec–Feb)** due to cooling and heating demand, with moderate consumption in spring and fall. |
| **Trends** | Overall, energy demand shows a **predictable repeating pattern** suitable for time-series forecasting. |

**Summary:**  
- Energy consumption is highly cyclical both daily and seasonally.  
- Forecasting models benefit from hour-of-day, day-of-week, and month-of-year features.  
- Adding external features (temperature, holidays) could further improve predictions.

---

## Approach

### 1. Data Preprocessing
- Handled missing values and cleaned the dataset
- Converted timestamps to datetime format
- Resampled and structured the data for time-series modeling

### 2. Feature Engineering
- Encoded time-related features such as hour-of-day, day-of-week, and month

### 3. Model
- **Model:** `XGBRegressor` (tree-based gradient boosting)
- **Hyperparameter tuning:** `GridSearchCV` using the **validation set**
- **Evaluation metric:** Mean Absolute Percentage Accuracy (MAPA)

---

## Results
- **Mean Absolute Percentage Accuracy (MAPA):** 89.97%  
- Model predictions closely track historical energy consumption patterns  
- Demonstrates strong performance for short-term hourly forecasts

---

## How to Run

1. Clone the repository:

```bash
git clone https://github.com/sandy3w/time-series-forecasting-energy-consumption.git
cd time-series-forecasting-energy-consumption
````

2. Install required packages:

```bash
pip install -r requirements.txt
```

3. Open the notebook and run `training.ipynb` to:

* Explore data
* Train and evaluate the model
* Generate predictions for a future date

---

## File Structure

```text
time-series-forecasting-energy-consumption/
│── PJME_hourly.csv       # Historical hourly energy consumption data
│── training.ipynb        # Jupyter notebook with preprocessing, modeling, and evaluation
│── README.md             # Project overview and instructions
```

---

## Next Steps

* **Feature Expansion:** Include additional features like:

  * Temperature and weather data
  * Holiday and special event indicators
  * Electricity pricing or demand-response signals
