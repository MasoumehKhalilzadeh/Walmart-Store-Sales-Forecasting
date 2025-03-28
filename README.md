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

- Model sales at the **store + department** level for finer granularity.
- Tune Prophet with holiday regressors and changepoint detection.
- Explore machine learning-based forecasting methods (e.g., XGBoost, LSTM).
- Evaluate using additional metrics (MAPE, RMSE).

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

