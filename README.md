# PCA of FAANG Stock Technical Indicators

Uses Principal Component Analysis to find the latent structure behind 16 technical indicators for Apple, Amazon, Google, Meta and Microsoft, and turns the components into financially meaningful factors.

**Tools:** Python · pandas · scikit-learn · factor_analyzer · SciPy · seaborn

## Data
14,964 daily observations with 16 numeric features: OHLC prices, volume, SMA/EMA, Bollinger Bands, RSI, MACD, daily return and 7-day volatility.
Source: FAANG stock prices dataset (Kaggle). Save it as `data/faang_stock_prices.csv`.

## Method
Missing values & feature selection (dropping the leakage-prone `Next_Day_Close`) → Z-score outliers → correlation matrix → **Bartlett's test & KMO** to check PCA suitability → standardisation → PCA → scree plot and Kaiser/90% variance criteria → loadings, score plots and biplots → reconstruction error → **comparison with Factor Analysis** → sensitivity analysis.

## Results
Four components explain **90.6% of the variance** (reconstruction MSE 0.069):

| Component | Interpretation | Variance |
|---|---|---|
| PC1 | Market price level (prices, moving averages, Bollinger Bands) | 63.6% |
| PC2 | Momentum / oscillator (MACD, RSI) | 14.1% |
| PC3 | Volume / volatility | 6.6% |
| PC4 | Residual daily return | 6.3% |

These match the core ideas of technical analysis: **trend, momentum and volatility**. Factor Analysis identified the same dominant variables, and PC1's loadings were stable across all thresholds tested.

## Run it
```bash
pip install -r requirements.txt
jupyter notebook faang_pca.ipynb
```

---
*MSc Data Science & Analytics, Munster Technological University (Multivariate Modelling)*
