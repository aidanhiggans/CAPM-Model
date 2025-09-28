# CAPM Portfolio Analysis

## Project Overview

A comprehensive Python implementation of the Capital Asset Pricing Model (CAPM) designed for financial portfolio analysis. This tool enables quantitative analysts, portfolio managers, and researchers to evaluate asset performance, calculate systematic risk metrics, and understand the relationship between portfolio returns and broad market movements.

## Features

### Single Asset and Portfolio Analysis
- Support for individual stock analysis by configuring portfolio weights as [1] for single assets
- Multi-asset portfolio evaluation with flexible weighting schemes for baskets of securities
- Customizable portfolio construction with weight validation ensuring all allocations sum to 1.0
- Automated handling of both individual equity tickers and complex portfolio combinations

### Comprehensive Risk and Return Metrics
- Beta coefficient calculation measuring portfolio sensitivity to market movements
- Alpha detection identifying abnormal returns not explained by market risk exposure
- Sharpe ratio computation for risk-adjusted performance measurement
- Annualized volatility calculation using square root of time rule
- Realized return metrics capturing historical performance with proper compounding

### Advanced Analytical Capabilities
- Dual methodology for beta estimation using covariance-variance formula and linear regression
- Excess returns analysis implementing proper CAPM framework with risk-free rate adjustments
- Expected returns forecasting based on CAPM equilibrium model
- Visual regression analysis plotting security market line with historical data points

### Robust Data Processing Pipeline
- Automated financial data download from Yahoo Finance API
- Monthly returns calculation using logarithmic returns
- Portfolio aggregation combining multiple asset returns according to weights
- Data validation handling missing values and multi-index data structures

## Methodology

### CAPM Theoretical Framework
The implementation follows the standard Capital Asset Pricing Model equation:

E[Rₐ] = Rf + β × (E[Rₘ] - Rf) + α

Where:
- E[Rₐ] = Expected portfolio return
- Rf = Risk-free rate
- β = Portfolio beta (systematic risk)
- E[Rₘ] = Expected market return
- α = Alpha (abnormal return)

### Statistical Implementation

#### Returns Calculation
- Monthly logarithmic returns computed as ln(Pₜ/Pₜ₋₁)
- Excess returns adjusted by monthly risk-free rate
- Annualization using √12 for volatility and ×12 for returns

#### Beta Estimation
- Covariance method: β = Cov(Rₐ, Rₘ) / Var(Rₘ)
- Regression method: Linear regression of excess returns
- Matrix operations for covariance calculations

#### Portfolio Construction
- Weighted return aggregation: Rₚ = ∑(wᵢ × Rᵢ) where ∑wᵢ = 1
- Multi-asset support with automatic validation
- Missing data handling through dropna operations

### Data Processing Architecture
1. Data collection from Yahoo Finance
2. Resampling to monthly frequency
3. Logarithmic returns calculation
4. Portfolio aggregation by weights
5. Risk metrics and regression analysis

## Tech Stack

### Core Libraries
- **NumPy**: Mathematical operations and statistical calculations
- **Pandas**: Data manipulation and time series analysis
- **yFinance**: Financial data extraction
- **Matplotlib**: Data visualization and plotting

### Financial Methodologies
- Time Series Analysis
- Risk Metrics Computation
- Regression Analysis (OLS)
- Modern Portfolio Theory

### Technical Features
- Object-Oriented Design
- Error Handling and Validation
- MultiIndex Data Handling
- Configurable Parameters

### Data Sources
- Equity Data: Yahoo Finance adjusted closing prices
- Market Benchmark: S&P 500 Index (^GSPC)
- Risk-Free Rate: User-configurable (default: 2% annual)

## Installation

```bash
pip install numpy pandas yfinance matplotlib scipy
