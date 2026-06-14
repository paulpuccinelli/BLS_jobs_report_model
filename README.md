# BLS Jobs Report Model

## Project Overview
This project explores whether publicly available macroeconomic and labor-market data can be used to anticipate payroll surprises in the U.S. Employment Situation Report. Rather than trying to predict payroll levels directly, the analysis focuses on identifying periods when actual payroll outcomes deviate from what would be expected based on observable economic conditions.

The main goal is to build a practical forecasting framework that combines public data sources, feature engineering, and statistical learning methods to classify whether labor-market outcomes are likely to be stronger or weaker than normal.

## Why This Project Matters
The Employment Situation Report is one of the most important macroeconomic releases for financial markets because payroll growth, unemployment, and labor-market momentum can affect interest rates, equities, and broader economic expectations. This project asks a simple but important question:

- Can public economic indicators provide useful signals about upcoming payroll surprises?

The answer is not meant to be a perfect forecasting system, but rather a structured way to evaluate whether public data contains meaningful predictive information.

## Project Goals
1. Build a model-based proxy for market expectations around payroll growth.
2. Generate surprise measures based on differences between realized payroll outcomes and model-implied expectations.
3. Use classification models to identify upside and downside surprise regimes.
4. Evaluate whether macroeconomic and labor-market indicators contain useful predictive signal.

## Methods
The project follows a multi-stage workflow:

### 1. Data Collection
The analysis combines data from:
- Bureau of Labor Statistics (BLS) labor-market indicators
- Federal Reserve Economic Data (FRED) macroeconomic and market indicators

### 2. Data Cleaning and Alignment
The raw series were cleaned, aligned by date, and consolidated into a single time-series dataset. This included handling missing values, standardizing variable formats, and preparing the data for model development.

### 3. Feature Engineering
Several derived indicators were created to capture momentum and persistence in labor-market conditions, including:
- rolling averages
- short-term changes in key rates
- transformations designed to stabilize skewed variables

These engineered features are intended to capture the broader economic environment rather than relying only on raw monthly levels.

### 4. Modeling Approach
The project uses two major modeling strategies:
- Ridge Regression for building an expectations model for payroll levels and growth
- XGBoost classifiers for upside and downside surprise classification

The modeling workflow uses time-series-aware validation methods such as TimeSeriesSplit and hyperparameter tuning through RandomizedSearchCV.

### 5. Evaluation
Performance was assessed using metrics such as:
- MAE (Mean Absolute Error)
- R-squared (R²)
- ROC-AUC
- classification precision, recall, and confusion-matrix analysis

## Data Sources
### BLS
The BLS data used in the project focuses on labor-market conditions, especially indicators related to hiring, separations, and labor demand.

### FRED
The FRED data includes macro and market variables such as:
- Total Nonfarm Payroll Employment (PAYEMS)
- Unemployment Rate (UNRATE)
- Initial Claims (ICSA)
- Continuing Claims (CCSA)
- 2-Year Treasury Yield (DGS2)
- 10-Year Treasury Yield (DGS10)
- Treasury yield spread (T10Y2Y)
- Consumer Sentiment (UMCSENT)

These variables were selected because they capture labor-market strength, policy expectations, financial conditions, and consumer confidence.

## Key Findings
The notebook reports the following main takeaways:
- The Ridge Regression expectations model achieved an out-of-sample MAE of approximately 4,124 payrolls and an out-of-sample R² of 0.46.
- The model captures a meaningful portion of broad payroll movement, but it systematically underestimates payroll levels in the test period.
- The optimized XGBoost model for upside surprises reached an ROC-AUC of about 0.768.
- The optimized downside-surprise model reached an ROC-AUC of about 0.751.

These results suggest that public macroeconomic variables do contain some predictive signal, but the classification task remains difficult and imperfect.

## Limitations
This project should be interpreted as an exploratory forecasting exercise rather than a final production-grade forecasting model. Several limitations are important:

1. Limited sample size for a machine-learning problem.
   The available historical window is relatively short for modeling macroeconomic time series.

2. Proxy expectations instead of real market consensus.
   The model uses a statistical proxy for expectations rather than actual economist forecasts or market-implied expectations.

3. Payroll levels are difficult to model directly.
   The project uses surprise classifications based on predicted payroll growth behavior, which helps but does not fully solve the challenge of modeling long-run upward trends in payroll employment.

4. Class imbalance in the classification task.
   Surprise events are relatively rare compared with non-surprise periods, which can limit recall and make the models conservative.

5. Public data only.
   The project relies on a limited set of broad macro variables and does not include higher-frequency market data, alternative labor indicators, or more detailed financial variables.

6. Correlation is not causation.
   The model identifies statistical relationships, not necessarily causal drivers of payroll surprises.

## What This Project Demonstrates
Despite its limitations, the project demonstrates several useful skills and concepts:
- time-series data preparation
- macroeconomic data acquisition and integration
- feature engineering for forecasting problems
- regression and classification modeling
- evaluation of predictive performance in a non-random time-series setting

It is a strong example of applied data science work in an economic and finance-adjacent context.

## Suggested Next Steps
Possible extensions to improve this project include:
- adding more macroeconomic and financial predictors
- using alternate surprise definitions
- incorporating higher-frequency market indicators
- testing additional models such as random forests, LightGBM, or neural models
- addressing class imbalance with resampling or threshold tuning

## Repository Contents
- BLS_prediction.ipynb — primary analysis notebook
- BLS_prediction_notebook.ipynb — additional notebook version
- blsdata.csv — cleaned BLS dataset
- master_df.csv — combined feature dataset used in modeling
- BLS_prediction.html — rendered notebook export

## Summary
This project is best understood as an applied forecasting and classification exercise focused on labor-market surprises. It combines public economic data, statistical modeling, and machine learning to investigate whether macroeconomic information can help identify periods of unusually strong or weak payroll outcomes.

