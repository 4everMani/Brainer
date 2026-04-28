---
id: 01-tana-a1b2
tags: [agentic-ai, 01_Foundations, time-series]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Time Series Analysis Fundamentals

> [!ABSTRACT]
> Time series analysis is the study of data points collected at successive intervals over time. Success in forecasting requires understanding core components like trend and seasonality, achieving stationarity through techniques like differencing, and establishing strong baselines like naive forecasting and SARIMA.

## 🧠 Intuition First
- Imagine you're tracking daily attendance at a swimming pool. 
- **Trend:** Attendance is generally increasing every year as the city grows. 
- **Seasonality:** Attendance is much higher in the summer than in the winter (repeating pattern). 
- **Stationarity:** If you subtract today's number from last year's number at the same time, you get a "stationary" series where the yearly pattern and long-term growth are gone, leaving only the random day-to-day noise. It's much easier to predict noise than a complex, shifting wave.

## 🎯 Why This Matters
- Problem it solves: Provides a structured way to decompose complex temporal data into predictable components and establishes the "baseline" accuracy that a neural network must beat to be useful.
- Real-world usage: Demand forecasting, financial modeling, and weather prediction.

## 🧩 Glossary
- [[Trend]] : A long-term increase or decrease in the data.
- [[Seasonality]] : A repeating pattern over a fixed period (e.g., weekly, monthly, yearly).
- [[Stationarity]] : A property where statistical properties (mean, variance) remain constant over time.
- [[Differencing]] : Subtracting the value at a previous time step from the current value to remove trend and seasonality.
- [[Naive Forecasting]] : A simple baseline where you predict the next value will be identical to the current one (or the same time last period).

## ⚙️ Mechanics (First Principles)
### Achieving Stationarity:
- **Linear Trend:** Apply 1st order differencing: $y'_t = y_t - y_{t-1}$.
- **Quadratic Trend:** Apply 2nd order differencing: $y''_t = (y_t - y_{t-1}) - (y_{t-1} - y_{t-2})$.
- **Seasonality:** Apply seasonal differencing: $y'_t = y_t - y_{t-s}$, where $s$ is the period.

### Baseline Models:
1. **Naive Forecast:** Predict tomorrow = Today. 
2. **Seasonal Naive:** Predict tomorrow = Same day last week.
3. **ARMA/ARIMA:** Weighted sum of past values and past errors.
4. **SARIMA:** ARIMA with an explicit seasonal component.

## 📐 Mathematical Foundations
- **Order of Integration ($d$):** The number of times differencing is applied to make a series stationary.

## 💻 Implementation
- Computing a 12-month difference in Pandas:
```python
# Removes yearly seasonality and linear trends
stationary_series = df.diff(12)
```

## 🧪 Experiments
1. **The Baseline Challenge:** Calculate the Mean Absolute Error (MAE) for a "Naive Forecast" on your dataset. Train your most complex RNN. If the RNN MAE is not lower than the Naive MAE, your model is useless.

## ⚠️ Constraints & Pitfalls
- **Accumulated Error:** Using a model to predict one step ahead and then using that prediction to predict the next step leads to rapidly growing errors.
- **Correlated Time Splits:** When splitting data, never use random shuffling. Always split chronologically (e.g., train on 2018, test on 2019).

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Machine_Learning_Fundamentals]]
- Used in → [[RNN_Forecasting_Architectures]]
- Related to → [[Regression_Metrics]]
---
(MINIMUM 3 links)
