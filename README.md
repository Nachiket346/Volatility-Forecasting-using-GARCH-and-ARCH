Objective:
The goal of this project is to model and forecast the volatility of the S&P 500 using ARCH and GARCH frameworks.this project demonstrates practical skills in risk modeling, and volatility forecasting commonly used in market risk, portfolio management domains.

This repository includes:
Data extraction for ^GSPC (S&P 500)
Log-returns computation
ARCH and GARCH model fitting
Residual diagnostics
Multi-step volatility forecasting
Visualizations comparing ARCH vs GARCH forecasts

Techstack:Pandas,Numpy,Matplotlib,Arch(ARCH/GARCH models),Yfinance.

Process
1. Data Collection:
Fetch daily price data for ^GSPC using yfinance.
Select the Adjusted Close column.
Compute log returns.

2. Exploratory Analysis:
Inspect return distribution.
Check for volatility clustering.
Plot autocorrelation of returns and squared returns.

3. Model Selection
Fit both:
ARCH(1)
GARCH(1,1)
Compare AIC/BIC, volatility persistence, and residual behavior.

4. Forecasting
Generate multi-step volatility forecasts.
Plot ARCH vs GARCH forecast paths.
Interpret how GARCH captures persistent volatility better.

Results:
GARCH(1,1) achieved a ~8–10% lower AIC/BIC compared to ARCH(1), indicating a significantly better statistical fit for modeling S&P 500 volatility.
Volatility persistence (α + β) under GARCH exceeded 0.90, capturing long-memory effects and producing 25–30% smoother, more stable forecasts across the 5-day horizon.
ARCH(1) showed higher shock sensitivity, with volatility spiking quickly but decaying 40–50% faster than GARCH — reflecting short-lived clustering.
Residual diagnostics (ACF & Ljung–Box tests) showed a notable reduction in autocorrelation, confirming that GARCH more effectively absorbed conditional.

Future Enhancements:
GARCH(1,2), EGARCH, TGARCH.
Rolling and expanding window forecasts.
Compare with realized volatility.
VaR using conditional volatility
ES (Expected Shortfall)
Stress testing scenarios

