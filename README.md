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
- **β < 1.0** → The portfolio is less sensitive to market movements.  

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

---

## Analysis on Sample Run

From a sample run, the portfolio produced the following metrics:  

- **Realized Annual Return**: 21.3%  
- **Annual Volatility**: 17.7%  
- **Sharpe Ratio**: 1.09  
- **Beta (Regression and Covariance)**: ≈ 0.94  
- **Alpha**: 0.009 (≈ 0.9%)  
- **Expected Return (CAPM)**: 10.4%  

### Interpretation
- **Beta ≈ 1**: With a beta close to 1, the portfolio behaves very similarly to the market benchmark. A beta value of 0.94 indicates slightly less sensitivity than the overall market. Hence when the market rises or falls, this portfolio tends to move in the same direction but with slightly smaller magnitude.  
- **Alpha ≈ 0.9%**: A positive alpha suggests that the portfolio has generated returns above what would be predicted by its market risk exposure. In practical terms, this is an indication of “excess performance,” which may come from diversification benefits, security selection, or exposure to risks not captured by CAPM.  
- **Realized vs. Expected Returns**: The realized annual return (21.3%) is significantly higher than the CAPM-expected return (10.4%). This gap illustrates a key limitation of CAPM: while it provides an equilibrium prediction under simplifying assumptions, actual realized returns are influenced by many other factors, such as industry trends, macroeconomic shocks, liquidity effects, and investor sentiment.

### Assumptions and Limitations
The CAPM model is elegant but relies on assumptions that are restrictive in practice:  
- **Normality of returns**: CAPM assumes that asset returns are normally distributed, which justifies the use of mean and variance as sufficient risk-return descriptors. In reality, returns often exhibit skewness and fat tails (higher probability of extreme events).  
- **Linearity**: CAPM assumes a strictly linear relationship between excess portfolio returns and excess market returns. However, empirical evidence suggests that this linearity may not hold across all time periods or asset classes. 
- **Single-factor dependence**: CAPM explains returns solely through exposure to market risk (beta). Other systematic risk factors are ignored.  

### Possible Extensions
To overcome these limitations, CAPM can be extended into multi-factor frameworks:  
- **Fama-French Three-Factor Model**: In the Fama-French Three-Factor Model, two additional factors are introduced beyond the market: **SMB (Small Minus Big)**, which captures the size effect (the historical outperformance of small-cap stocks over large-cap stocks), and **HML (High Minus Low)**, which captures the value effect (the tendency for high book-to-market "value" stocks to outperform low book-to-market "growth" stocks). Together, these factors account for systematic risks that CAPM alone cannot explain.
- **Carhart Four-Factor Model**: Further includes a **momentum** factor, capturing the tendency of winning stocks to keep outperforming in the short term.  
- **Arbitrage Pricing Theory (APT)**: Generalizes the idea further, allowing multiple macroeconomic and firm-specific factors to drive returns.  

These extensions provide a richer description of asset returns and often align more closely with observed market behavior, reducing the discrepancy between realized and expected returns.
