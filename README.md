Objective:
Quantify time-varying conditional volatility.
Compare short-memory vs persistent volatility dynamics.
Generate forward-looking volatility forecasts suitable for VaR, ES, stress testing, and capital modeling.

Methodology:

1. Market Data Preparation
Retrieved daily Adjusted Close prices for the S&P 500 using yFinance.
Computed logarithmic returns to ensure stationarity and scale invariance.
Cleaned and aligned data to remove missing observations.

2. Exploratory Risk Diagnostics
Analyzed return distribution for fat tails and volatility clustering
Examined autocorrelation of returns and squared returns
Confirmed presence of conditional heteroskedasticity, justifying ARCH/GARCH modeling

3.Volatility Model Specification & Estimation
Estimated and compared:
ARCH(1): Captures short-term volatility response to recent shocks
GARCH(1,1): Models both shock impact (α) and volatility persistence (β)

Model adequacy was assessed using:
Log-likelihood.
AIC / BIC.
Volatility persistence (α + β).
Residual autocorrelation diagnostics.

4. Volatility Forecasting
Generated multi-step conditional volatility forecasts.
Compared forecast dynamics and stability between ARCH and GARCH.
Evaluated suitability for risk forecasting horizons used in market risk.

Technology Stack:
Pandas
NumPy
ARCH / GARCH models
YFinance
Matplotlib

Model Results & Comparative Analysis

| Metric / Output                  | **ARCH(1)**      | **GARCH(1,1)**      | **Risk Interpretation**                                     |
| -------------------------------- | ---------------- | ------------------- | ----------------------------------------------------------- |
| **Log-Likelihood**               | –3522.80         | **–3226.80**        | GARCH delivers a materially superior statistical fit        |
| **AIC**                          | 7051.59          | **6461.60**         | ~**590-point reduction**, indicating strong model dominance |
| **BIC**                          | 7069.08          | **6484.92**         | Confirms improved parsimony-adjusted fit                    |
| **α (Shock Sensitivity)**        | 0.5192           | 0.1821              | ARCH overreacts to recent shocks                            |
| **β (Persistence)**              | —                | 0.7869              | GARCH captures sustained volatility regimes                 |
| **ω (Long-Run Variance)**        | 0.6393           | 0.0389              | Lower GARCH ω reflects persistent conditional variance      |
| **Volatility Persistence (α+β)** | 0.5192           | **0.9690**          | Near-unit persistence typical of equity markets             |
| **5-Day σ Forecast (Day 5)**     | 1.1358           | **1.0097**          | ARCH produces unstable risk estimates                       |
| **Forecast Profile**             | Reactive & spiky | Smooth & persistent | GARCH better suited for VaR / ES inputs                     |

Risk Interpretation & Insights:

1. Model Fit & Information Criteria
GARCH(1,1) improves log-likelihood by ~296 points relative to ARCH(1) (–3226.8 vs –3522.8), indicating a materially superior explanation of observed return volatility.
AIC decreases by ~590 points and BIC by ~584 points, far exceeding typical model-selection thresholds, providing strong statistical evidence in favor of GARCH.

2. Shock Sensitivity vs Volatility Persistence:
ARCH(1) assigns ~52% of next-day variance directly to the most recent shock (α = 0.519), leading to excessive short-term volatility spikes.
GARCH(1,1) allocates volatility more realistically:
Shock impact (α) = 0.182 (~18%)
Persistence (β) = 0.787 (~79%)
The resulting volatility persistence (α + β ≈ 0.97) implies that ~97% of today’s volatility carries forward, consistent with long-memory behavior observed in equity markets.

3. Volatility Decay & Half-Life:
With α + β ≈ 0.97, GARCH volatility shocks decay slowly:
Approximate half-life ≈ 23 trading days
In contrast, ARCH(1) volatility decays rapidly:
Half-life ≈ 1.3 trading days
This difference materially affects multi-day risk aggregation and capital estimation.



4. Forecast Stability (5-Day Horizon):
Over a 5-day forecast window:
ARCH volatility increases by ~28%, reflecting shock-driven overreaction.
GARCH volatility increases by only ~1.5%, remaining close to long-run conditional variance.
GARCH therefore reduces forecast-induced noise, improving reliability of downstream VaR and ES calculations.



5. Base Variance Estimation:
ARCH ω = 0.639 implies a high unconditional variance, compensating for lack of persistence.
GARCH ω = 0.039, combined with high β, produces the same long-run variance more efficiently, reducing parameter instability.
This structure lowers parameter risk and improves out-of-sample robustness.



6. Residual Diagnostics & Model Adequacy:
Standardized residuals under GARCH exhibit:
Minimal autocorrelation
No remaining ARCH effects
ARCH residuals retain significant dependence, indicating model misspecification.
From a validation standpoint, GARCH satisfies key diagnostic checks, supporting its use in regulated risk environments.

7. Market Risk Implications
Using ARCH volatility would inflate short-horizon VaR/ES following market shocks, potentially leading to:
Procyclical capital requirements.
Unstable risk limits.

GARCH volatility produces smoother, persistence-aware risk measures, improving:
Risk limit calibration.
Stress testing consistency.
Portfolio-level capital stability.

Future Enhancements
Higher-order models: GARCH(1,2)
Asymmetric volatility models: EGARCH, TGARCH
Rolling and expanding window estimation
Comparison with realized volatility
Integration with VaR and ES under conditional volatility
Market stress scenario overlays and regime analysis

Summary (One-Line Risk Conclusion)
GARCH(1,1) provides a statistically superior, persistence-aware volatility estimate that materially improves multi-day risk forecasting and reduces model-induced noise in VaR and ES calculations.

Key Takeaways:
GARCH(1,1) materially outperforms ARCH(1) in modeling S&P 500 volatility, with ~590-point lower AIC and near-unit volatility persistence (α + β ≈ 0.97), consistent with empirical equity market behavior.

ARCH models overreact to short-term shocks, producing unstable and spiky volatility forecasts, whereas GARCH delivers smoother, more reliable forward-looking risk estimates suitable for VaR, ES, and stress testing.

Volatility persistence is the dominant risk driver in equity indices; distributing shocks over time improves forecast realism and reduces model risk in portfolio applications.

Residual diagnostics confirm statistical adequacy of GARCH, with significantly reduced autocorrelation and effective correction of conditional heteroskedasticity.

Multi-step volatility forecasts from GARCH are better aligned with market risk horizons, showing minimal volatility drift over 5 days compared to exaggerated ARCH response.
