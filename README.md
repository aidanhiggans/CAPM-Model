# CAPM Portfolio Analysis

## Project Overview

This project provides a Python-based implementation of the **Capital Asset Pricing Model (CAPM)** for analyzing financial portfolios. It is designed to evaluate the performance of individual securities or portfolios of assets in relation to the overall market.  

By combining historical market data with modern portfolio theory, the tool estimates expected returns, measures systematic risk exposure, and highlights whether a portfolio has delivered returns beyond what would be predicted by its risk profile.

A key feature of this implementation is its **flexibility**: the user can easily configure assets, portfolio weights, and benchmark indices directly from the script’s input variables. This makes it suitable both for single-stock analysis and for more complex portfolio structures.

---

## Key Features

### Flexible Portfolio Construction
The model supports both **single-asset** and **multi-asset portfolio analysis**.  
- To analyze one stock, the weights can simply be set to `[1]`.  
- For multi-asset portfolios, any combination of tickers can be chosen, with weights specified in a corresponding ordered list.  
- Weight validation ensures that the portfolio is always properly normalized (summing to 1).  
- The benchmark index (default: S&P 500, `^GSPC`) can also be swapped for another market index, allowing for different comparative baselines.

### Risk and Performance Metrics
The tool calculates a comprehensive set of metrics:
- **Realized annual returns** based on historical performance  
- **Annualized volatility**, using the square-root-of-time rule  
- **Sharpe ratio**, which evaluates returns relative to risk  
- **Beta**, measuring the sensitivity of the portfolio to market movements  
- **Alpha**, representing abnormal returns not explained by market exposure  

### Dual Beta Estimation
Beta can be computed in two independent ways:
1. Using the covariance-variance formula:  
β = Cov(Rₐ, Rₘ) / Var(Rₘ)
2. Via linear regression of excess returns against the market, which also yields an estimate of **alpha**.

### Visual Analysis
The model produces a **CAPM regression plot**, showing excess portfolio returns against excess market returns. The regression line represents the Security Market Line (SML), and the vertical intercept highlights alpha. This visualization helps determine whether the portfolio has historically underperformed, matched, or outperformed CAPM expectations.

---

## Methodology

### The CAPM Framework
The foundation of the analysis is the CAPM equation:

E[Rₐ] = Rf + β × (E[Rₘ] - Rf) + α

- **E[Rₐ]**: The expected return of the asset or portfolio  
- **Rf**: The risk-free rate (such as U.S. Treasury yields)  
- **β**: The sensitivity of the portfolio to market risk  
- **E[Rₘ]**: The expected return of the market  
- **α**: The abnormal return not explained by market risk  

### Understanding Beta and Alpha
- **β = 1.0** → The portfolio moves in line with the market.  
- **β > 1.0** → The portfolio is more volatile than the market (higher risk, higher potential reward).  
- **β < 1.0** → The portfolio is less sensitive to market movements (less risk).  

**Alpha** represents the return above or below what CAPM would predict:  
- **α > 0** → The portfolio has outperformed its risk-adjusted expectations.  
- **α = 0** → The portfolio’s returns are fully explained by market risk.  
- **α < 0** → The portfolio has underperformed relative to its risk profile.  

This distinction is crucial in active management, as a consistently positive alpha indicates skill or market inefficiency.

### Statistical Implementation
1. **Data Collection**: Adjusted closing prices are downloaded via Yahoo Finance.  
2. **Resampling**: Prices are resampled to month-end values to smooth daily volatility and align with CAPM’s assumption of approximately normal returns.  
3. **Return Calculation**: Logarithmic monthly returns are calculated as
   ln(Pₜ/Pₜ₋₁) 
5. **Portfolio Aggregation**: Weighted returns are computed based on user-specified allocations.  
6. **Excess Returns**: Returns are adjusted for the monthly risk-free rate.  
7. **Regression**: A linear regression estimates beta (slope) and alpha (intercept).  

---

## Libraries Used

- **NumPy**: Numerical and statistical computations  
- **Pandas**: Time series and portfolio data handling  
- **yFinance**: Market data collection from Yahoo Finance  
- **Matplotlib**: Visualization of regression lines and distributions  

---

## Usage

1. Edit the variables at the top of the script (`ASSET`, `WEIGHTS`, `MARKET_INDEX`, `START_DATE`, `END_DATE`, and `RISK_FREE_RATE`) to suit your analysis.  
2. Run the script.  
3. Review the printed metrics and regression plots to interpret portfolio performance.  

This approach allows for straightforward experimentation with different portfolios, benchmarks, and time periods.
