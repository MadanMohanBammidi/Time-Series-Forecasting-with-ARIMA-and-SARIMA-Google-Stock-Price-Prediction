# Time Series Forecasting with ARIMA and SARIMA

## Overview

This project demonstrates how to use **ARIMA** (AutoRegressive Integrated Moving Average) and **SARIMA** (Seasonal AutoRegressive Integrated Moving Average) models to forecast time series data. Specifically, we use the **Google (GOOG) stock price** data from Yahoo Finance for the prediction task.

We will walk through:
- How to acquire and explore stock price data.
- Understanding and applying ARIMA and SARIMA models.
- Performing stationarity checks and identifying key model parameters (p, d, q).
- Evaluating the models using forecast error metrics.

## Project Objective

The objective of this project is to predict the future stock prices of **Google** using ARIMA and SARIMA models, compare their performance, and analyze the results. By doing so, we can get an understanding of how these models perform for financial time series forecasting.

---

## Step-by-Step Process

### 1. **Data Acquisition and Exploration**
First, we download the historical stock price data for **Google** (GOOG) using the `yfinance` package. We focus on the **closing price** as it reflects the market's perception of the company's value.

After obtaining the data, we perform initial exploratory analysis:
- Visualize the data to see the trend, seasonality, and volatility.
- Check for patterns in the data, such as cyclical behavior and irregular fluctuations.

### 2. **Stationarity Checks**
Before applying ARIMA or SARIMA models, we must ensure the data is **stationary**. Stationarity means that the statistical properties (mean, variance) of the time series are constant over time.

There are multiple methods to check for stationarity:
- **Augmented Dickey-Fuller Test (ADF Test)**: A statistical test where the null hypothesis assumes the series has a unit root (i.e., it is non-stationary). If the p-value is less than 0.05, the data is stationary.
- **Visual Inspection**: By plotting the rolling statistics (e.g., rolling mean and standard deviation), we can visually assess whether the time series is stationary.
- **Differencing**: If the data is non-stationary, we apply differencing to remove trends and make the data stationary.

### 3. **Identifying Model Parameters (p, d, q)**
For ARIMA and SARIMA models, we need to determine three key parameters: **p**, **d**, and **q**:
- **p (AutoRegressive term)**: The number of lag observations used in the model. This can be determined using the **Partial Autocorrelation Function (PACF)** plot. The point at which the PACF plot cuts off gives us the value of **p**.
- **d (Differencing term)**: The number of differencing operations required to make the series stationary. Typically, if the series is non-stationary, **d = 1** (first-order differencing) is used.
- **q (Moving Average term)**: The number of lagged forecast errors included in the model. The **Autocorrelation Function (ACF)** plot helps in determining **q** by showing the correlation between a time series and its lagged versions.

### 4. **ARIMA Model**
Once the parameters p, d, and q are determined, the ARIMA model is fitted to the time series data. ARIMA is composed of three components:
- **AR (AutoRegressive)**: A model that uses the dependency between an observation and a number of lagged observations (p).
- **I (Integrated)**: The differencing part (d) used to make the time series stationary.
- **MA (Moving Average)**: A model that uses the dependency between an observation and a residual error from a moving average model applied to lagged observations (q).

The model is then trained on the available historical data, and predictions are made for future values.

### 5. **SARIMA Model**
**SARIMA** (Seasonal ARIMA) extends the ARIMA model by accounting for seasonality in the time series data. It includes additional seasonal terms:
- **Seasonal AR (P)**: The seasonal autoregressive part.
- **Seasonal Differencing (D)**: The differencing at seasonal lags.
- **Seasonal MA (Q)**: The seasonal moving average part.
- **Seasonal Period (s)**: The period of the seasonal cycle (e.g., 12 for monthly data with annual seasonality).

SARIMA is particularly useful for time series with patterns that repeat over fixed periods, such as yearly or quarterly cycles.

### 6. **Model Evaluation**
To evaluate the performance of the ARIMA and SARIMA models, we use error metrics:
- **Mean Absolute Error (MAE)**
- **Root Mean Squared Error (RMSE)**

Since we don't have access to future data points, we can evaluate the models using historical data that we know. By comparing the predicted values with the actual values in the test set, we can compute these error metrics.

### 7. **Comparison of ARIMA and SARIMA**
We compare the performance of ARIMA and SARIMA based on their error metrics:
- **ARIMA**: Suitable when there is no clear seasonal pattern in the data.
- **SARIMA**: More effective when the data exhibits seasonality (e.g., yearly, monthly trends).

---

## Detailed Explanation of ARIMA and SARIMA

### ARIMA (AutoRegressive Integrated Moving Average)

ARIMA is a class of models used for forecasting stationary time series data. It combines three components:
- **AR (AutoRegressive)**: This component uses the relationship between an observation and a number of lagged observations. It can be thought of as a weighted sum of past observations.
- **I (Integrated)**: This component is used to make the series stationary by differencing the data (subtracting the previous value from the current value).
- **MA (Moving Average)**: This component models the relationship between an observation and a residual error from a moving average model applied to lagged observations.

ARIMA is represented as **ARIMA(p, d, q)** where:
- **p** is the number of autoregressive terms,
- **d** is the number of differencing operations,
- **q** is the number of moving average terms.

#### How to Determine p, d, q:
- **p**: Identified using the Partial Autocorrelation Function (PACF) plot. The PACF shows the correlation between the time series and its lagged versions, helping determine the number of AR terms.
- **d**: The number of times differencing is required to make the series stationary. Usually, **d = 1** if the series is non-stationary.
- **q**: Identified using the Autocorrelation Function (ACF) plot. The ACF shows the correlation between the time series and the residual errors of the model, helping determine the number of MA terms.

### SARIMA (Seasonal ARIMA)

SARIMA is an extension of the ARIMA model that accounts for seasonality in time series data. In addition to the standard AR, I, and MA components, SARIMA includes seasonal components:
- **Seasonal AR (P)**: The seasonal autoregressive part.
- **Seasonal Differencing (D)**: The differencing applied at seasonal lags.
- **Seasonal MA (Q)**: The seasonal moving average part.
- **Seasonal Period (s)**: The period of the seasonal cycle.

SARIMA is represented as **SARIMA(p, d, q)(P, D, Q, s)** where:
- **(p, d, q)** are the non-seasonal parameters,
- **(P, D, Q)** are the seasonal parameters,
- **s** is the length of the seasonal cycle.

---

## Conclusion

In this project, we have demonstrated how to forecast stock prices using ARIMA and SARIMA models. By exploring the fundamental principles of time series analysis, such as stationarity, differencing, and identifying the appropriate p, d, q values, we were able to build and evaluate predictive models.

Understanding ARIMA and SARIMA is crucial for anyone working with time series data, especially for financial forecasting, weather prediction, and sales forecasting. The knowledge of how to properly prepare data and select model parameters leads to more accurate and reliable predictions.

---

## Future Work

- Explore additional forecasting techniques like **Exponential Smoothing** or **Prophet**(A Facebook's library for Forecasting at scale).
- Use more advanced evaluation techniques such as cross-validation or walk-forward validation.
- Extend the project to other stock data and try multivariate time series forecasting.

