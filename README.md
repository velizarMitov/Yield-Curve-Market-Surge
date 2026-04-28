# Yield-Curve-Market-Surge

This project investigates the relationship between US Treasury yield curve inversions (10-year vs. 2-year bonds) and the performance of the S&P 500 index. The primary objective is to test the "Late-Cycle Market Surge" hypothesis – whether the stock market tends to rise significantly after the bond market signals an impending recession.

## Project Overview

Yield curve inversions are considered one of the most reliable indicators of an upcoming recession. This project analyzes whether the stock market reacts immediately or if there is a statistically significant delay (lag) in the reaction.

## Analysis Stages

1.  **Data Acquisition**: Automated extraction of indicators from FRED (GDP, CPI) and financial data from Yahoo Finance (S&P 500, DXY).
2.  **Processing**: Cleaning, frequency alignment (daily to quarterly), and handling missing values.
3.  **Exploratory Data Analysis (EDA)**: Visualization of time series, correlation matrices, and regression analysis by economic regimes.
4.  **Statistical Testing**: Applying Welch's t-test to compare mean S&P 500 returns under normal and inverted curve states with a one-quarter lag.

## Key Findings

The analysis confirms the "Late-Cycle Market Surge" hypothesis:
- The average quarterly return following a yield curve inversion is significantly higher (~5.41%) compared to normal periods (~1.72%).
- Welch's t-test results (p-value ≈ 0.02) allow for the rejection of the null hypothesis at a 95% confidence level.

## Tech Stack

- **Python** (Pandas, NumPy)
- **Visualization**: Matplotlib, Seaborn
- **Statistics**: SciPy
- **Data Sources**: yfinance, FRED API (CSV endpoints)

## Getting Started

1. Install the required libraries:
   ```bash
   pip install -r requirements.txt
   ```
2. Open and run `sample.ipynb`.
