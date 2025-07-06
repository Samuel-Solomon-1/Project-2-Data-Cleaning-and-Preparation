# Project 2: Data Cleaning and Preparation

## Project Overview

This project builds on the foundational work in Project 1 (Exploratory Data Analysis) and prepares the historical stock price dataset for advanced analysis and machine learning. The primary focus is on improving data quality, engineering meaningful features, and structuring the dataset for predictive modeling.

## Dataset Summary

- **historical_stocks.csv**: Contains metadata for each stock (e.g., ticker, sector, industry).
- **historical_stock_prices.csv**: Contains daily trading data from 1970–2018 (open, high, low, close, volume, etc.).

Due to memory constraints in a typical analysis environment, a subset of ~20 widely recognized tickers was selected for the cleaning and transformation process.

## Tasks Completed

### 1. Advanced Data Cleaning

- **Missing Values**:  
  - 1,440 missing values found in `sector` and `industry` columns.
  - Filled using `'Unknown'` to retain the stock while marking the absence of metadata.
  - No missing values were found in price-related columns.

- **Outlier Detection and Handling**:  
  - Extreme values in `close` and `volume` columns were capped using the 1st and 99th percentiles.
  - Log transformation applied to `volume` to reduce skew.

- **Error Correction**:  
  - Removed rows with invalid values (e.g., zero or negative prices/volumes).
  - Duplicate records were dropped to preserve data integrity.

### 2. Data Transformation

- **Rolling Features**:  
  - `rolling_7`: 7-day moving average of closing price per ticker.  
  - `rolling_30`: 30-day moving average.  
  - `volatility_7`: 7-day rolling standard deviation (volatility).

- **Returns**:  
  - Daily percentage change in closing price (`return`).

- **Log Transformation**:  
  - `volume_log`: `log1p(volume)` to reduce scale imbalance.

- **Standardization**:  
  Applied `StandardScaler` to:  
  - `close`, `volume_log`, and `return`.

- **Encoding**:  
  - Applied one-hot encoding to `exchange` and `sector` to prepare categorical features for modeling.

### 3. Data Integration & Splitting

- Merged price data with company metadata (`exchange`, `sector`).
- Filtered dataset to include 20 high-volume, large-cap tickers such as `AAPL`, `GOOG`, `MSFT`, `AMZN`, `TSLA`, and others.
- Performed **time-aware data splitting**:
  - **Training Set**: 70%
  - **Validation Set**: 15%
  - **Test Set**: 15%
- Ensured no data leakage by sorting chronologically before splitting.

## Output Files

All files are saved to Google Drive for reuse:

- `train_clean.csv`
- `val_clean.csv`
- `test_clean.csv`

These files include cleaned, transformed, and encoded data ready for input into machine learning models.

## Conclusion

This project produced a high-quality dataset that is:

- Free from inconsistencies, anomalies, and invalid entries  
- Enriched with time-series features (rolling averages, volatility, returns)  
- Standardized and encoded for modeling  
- Split in a time-sensitive manner for real-world predictive applications

This cleaned dataset is ready for use in the next project, which will focus on applying regression and classification models to forecast stock behavior.
