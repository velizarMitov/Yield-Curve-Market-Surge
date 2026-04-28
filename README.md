# S&P 500 Dynamics Analysis Following Yield Curve Inversion

This project investigates the relationship between the inversion of the US Treasury yield curve (10-year vs. 2-year) and the performance of the S&P 500 index. The primary objective is to test the "Late-Cycle Market Surge" hypothesis—whether the stock market rises significantly after the bond market signals an impending recession.

## Project Overview

Yield curve inversion is considered one of the most reliable indicators of an impending economic recession. This project analyzes whether the stock market reacts immediately or if there is a statistically significant lag in the reaction.

## Key Analysis Stages

1.  **Data Extraction**: Dynamic extraction of economic indicators from FRED (GDP, CPI, interest rates) and financial data from Yahoo Finance (S&P 500, DXY).
2.  **Data Processing**: Cleaning, frequency alignment (daily to quarterly), and handling missing values using forward-filling.
3.  **EDA (Exploratory Data Analysis)**: Time-series visualization, correlation matrices, and regression analysis by economic regimes (high vs. low inflation).
4.  **Statistical Testing**: Applying Welch's t-test to compare the average return of the S&P 500 during normal and inverted yield curve periods with a one-quarter lag.

## Key Findings

The analysis confirms the "Late-Cycle Market Surge" hypothesis:
- The average quarterly return after a curve inversion is significantly higher (~5.41%) compared to normal periods (~1.72%).
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
2. Open and run `sample.ipynb` in a Jupyter environment.
