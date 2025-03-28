# 📊 Walmart Store Sales Forecasting

## 📄 Project Overview
This project focuses on forecasting weekly sales for Walmart using classical and Bayesian time series models. We use the publicly available Walmart Store Sales Forecasting dataset from a Kaggle competition to predict future trends and evaluate model performance. The objective is to compare traditional ARIMA modeling with Facebook's Prophet model and generate actionable insights based on forecast accuracy.

---

## 📅 Dataset Description
**Source:** [Walmart Recruiting - Store Sales Forecasting (Kaggle)](https://www.kaggle.com/competitions/walmart-recruiting-store-sales-forecasting)

### Files Used:
- `train.csv`: Historical weekly sales data per store and department  
- `stores.csv`: Metadata about each store (type and size)  
- `features.csv`: Additional features such as temperature, fuel price, CPI, unemployment, and holiday indicators  

### Key Columns:
- `Date`: Week of sales  
- `Store`: Store identifier  
- `Weekly_Sales`: Sales in USD  
- `IsHoliday`: Boolean flag for major US holidays  

---

## ⚙️ Methodology & Steps

### 1. **Data Loading & Merging**
- Combined `train.csv`, `stores.csv`, and `features.csv` into a single DataFrame.
- Converted `Date` to datetime format for time series compatibility.

### 2. **Data Cleaning & Preprocessing**
- Handled missing values using forward-fill.
- Created time-based features: Year, Month, Week.
- Aggregated sales at the weekly level across all stores for total forecasting.

### 3. **Exploratory Data Analysis (EDA)**
- Visualized sales trends over time.
- Observed seasonal patterns and holiday effects.

### 4. **Time Series Decomposition**
- Used `seasonal_decompose` from `statsmodels` to separate trend, seasonality, and residual components of weekly sales.

### 5. **Stationarity Check & Differencing**
- Applied Augmented Dickey-Fuller test.
- Differenced the series to achieve stationarity before ARIMA modeling.

### 6. **Model 1: ARIMA Forecasting**
- Used ARIMA(1,1,1) model from `statsmodels`.
- Forecasted 12 future weeks.
- Evaluated using **Mean Absolute Error (MAE)**:  **`1,440,699.23`**

### 7. **Model 2: Prophet Forecasting**
- Trained Prophet model on weekly aggregated sales.
- Generated 12-week future forecasts.
- MAE for Prophet: **`8,255,984.62`**

---

## 📈 Results & Interpretation

### Exploratory Data Analysis (EDA)

- Visualized sales trends over time.
- Observed spikes around holidays and end-of-year periods.

![1](https://github.com/user-attachments/assets/5db33104-4e29-450b-a236-588912d59dea)



### Time Series Decomposition

- Used additive decomposition to extract trend, seasonality, and residuals from the time series.

![2](https://github.com/user-attachments/assets/a28f9bb4-15f8-4101-ae08-21dafff5f032)


### Stationarity Check & Model Diagnostics

- Differenced the data and plotted ACF/PACF to determine ARIMA parameters.


![3](https://github.com/user-attachments/assets/7b85b6e5-6a3a-4814-8554-0283b8aa63c1)

### 📃 ARIMA Model Summary

The ARIMA(1,1,1) model was selected based on ACF/PACF diagnostics and fitted to the weekly sales data. Below is the model output summary:


![Screenshot 2025-03-28 113435](https://github.com/user-attachments/assets/0efd75ca-be3e-4d36-90af-fd2a09c6db5f)


### 🧠 Interpretation:
- **ar.L1 (0.456)**: The AR(1) term is statistically significant (`p < 0.001`), indicating strong autocorrelation with lag 1.
- **ma.L1 (−0.976)**: The MA(1) term is also significant and negative, which suggests short-term corrections in forecast errors.
- **sigma²**: Represents the variance of the residuals (large due to scale of weekly sales).
- **Ljung-Box Q (p = 0.29)**: No significant autocorrelation in residuals → model is well-fitted.
- **Jarque-Bera (p = 0.00)**: Residuals are not normally distributed (common with sales data).
- **Skew = 1.37 / Kurtosis = 12.02**: Residuals are right-skewed with heavy tails, indicating potential outliers or holiday effects.

> ✅ Overall, this ARIMA(1,1,1) model fits the time series reasonably well, capturing the autocorrelation structure and producing low forecast error.



### ARIMA Forecasting

- Forecasted 12 future weeks using ARIMA(1,1,1).
- Lower error compared to Prophet.


![4](https://github.com/user-attachments/assets/164b4508-5bbd-4258-bb02-6387a7e8c44f)



### Prophet Forecasting

- Forecasted 12 future weeks with Prophet model.
- Included uncertainty intervals.


![5](https://github.com/user-attachments/assets/e049c4c5-0c31-4715-9b58-dedc913f984f)


## Forecast Accuracy Comparison: ARIMA vs Prophet

- **ARIMA outperformed Prophet** significantly in this project, producing a much lower forecasting error (MAE).
- **ARIMA MAE:** ~$1.44M  
- **Prophet MAE:** ~$8.26M

### 💡 Why ARIMA Performed Better:
- The time series was regular, weekly, and mostly stable with clear stationarity after differencing.
- Prophet may have struggled due to limited strong seasonal/holiday components or default parameters.

---

## 📊 Business Insight

The ability to accurately forecast weekly sales is crucial for inventory planning, staffing, and promotion scheduling. Based on this analysis, ARIMA provides a more reliable framework for short-term sales forecasting in Walmart's context.

---

## 📈 Future Improvements

For the next project, I will explore machine learning-based forecasting methods (e.g., XGBoost, LSTM) and evaluate them using additional metrics (MAPE, RMSE).

---

## 📂 How to Use This Project

> To run this project yourself:
1. Download the dataset from Kaggle.
2. Upload `train.csv`, `stores.csv`, and `features.csv` into your Colab or local environment.
3. Run the notebook step-by-step.

Make sure to install required libraries: `prophet`, `statsmodels`, `matplotlib`, `pandas`, `seaborn`, `scikit-learn`.

---

## 📄 License & Credit

Dataset provided by Walmart and Kaggle for educational and non-commercial use.

