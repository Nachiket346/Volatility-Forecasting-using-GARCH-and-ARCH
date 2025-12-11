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
| Metric / Output                    | **ARCH(1)**      | **GARCH(1,1)**      | **Interpretation**                                                            |
| ---------------------------------- | ---------------- | ------------------- | ----------------------------------------------------------------------------- |
| **Log-Likelihood**                 | **–3522.80**     | **–3226.80**        | GARCH fits the data substantially better (≈ **296-point improvement**).       |
| **AIC**                            | **7051.59**      | **6461.60**         | GARCH lowers AIC by **≈590 points**, indicating a far better model.           |
| **BIC**                            | **7069.08**      | **6484.92**         | GARCH reduces BIC by **≈584 points**, reinforcing stronger explanatory power. |
| **α (shock sensitivity)**          | **0.5192**       | **0.1821**          | ARCH reacts strongly to recent shocks; GARCH reacts more moderately.          |
| **β (volatility persistence)**     | —                | **0.7869**          | GARCH persistence (α+β) ≈ **0.97**, capturing long-memory effects.            |
| **ω (base variance)**              | 0.6393           | 0.0389              | GARCH estimates lower unconditional variance due to persistence.              |
| **Volatility Persistence (α + β)** | 0.5192           | **0.9690**          | GARCH volatility decays much more slowly → more realistic for equities.       |
| **5-Day σ Forecast (Day 5)**       | **1.1358**       | **1.0097**          | ARCH forecast rises sharply; GARCH stays stable and smoother.                 |
| **Forecast Shape**                 | Spiky & reactive | Smooth & persistent | GARCH is better for portfolio risk, VaR/ES inputs, and stress testing.        |

Interpretation:
Model Fit:
GARCH(1,1) provides a dramatically improved fit, with ~590-point lower AIC and ~584-point lower BIC, indicating a significantly stronger explanation of volatility dynamics.

Shock vs Persistence Behavior:
ARCH(1) has a high α = 0.52, meaning volatility jumps aggressively after shocks but decays fast.
GARCH spreads volatility across α + β ≈ 0.97, capturing long-term clustering typical of equity indices.

Forecast Comparison:
Over a 5-day horizon, ARCH volatility increases ~28%, while GARCH increases only ~1.5%, producing smoother and more realistic forecasts for market-risk scenarios.

Residual Diagnostics:
GARCH reduces autocorrelation in standardized residuals and addresses conditional heteroskedasticity more effectively, confirming better statistical adequacy.

Future Enhancements:
GARCH(1,2), EGARCH, TGARCH.
Rolling and expanding window forecasts.
Compare with realized volatility.
VaR using conditional volatility
ES (Expected Shortfall)
Stress testing scenarios

