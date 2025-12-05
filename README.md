# Apple Fruit Hedging Strategy Analysis

## Overview

This project analyzes hedging strategies for apple fruit futures traded on the Zhengzhou Commodity Exchange. The analysis focuses on Western apple producers seeking to hedge their harvest exposure through exchange rate hedging and climate-based strategies.

## Project Structure

```
apple-fruit-hedging/
├── notebooks/
│   └── Apple.ipynb          # Main analysis notebook
├── data/
│   ├── APFUTURES2020-2025.txt    # Apple futures price data
│   ├── APOPTIONS2023-2025.txt    # Apple options data
│   ├── taxa de juros china.txt   # China interest rates
│   └── apple_dfs_backup.csv      # Backup data file
├── requirements.txt          # Python dependencies
└── README.md                # This file
```

## Key Analysis Components

### 1. **Data Collection & Processing**
- Apple futures data from Zhengzhou Commodity Exchange (2020-2025)
- Commodity futures correlation analysis (OJ, sugar, soybeans, cotton, wheat, corn, coffee, cocoa, lean hogs)
- Exchange rate data (CNY/USD)
- Climate data from NASA POWER API for major apple-producing regions

### 2. **Price Analysis**
- Continuous futures time-series construction using contract interpolation
- Log returns calculation
- Volatility analysis (annualized volatility ~38%)
- Distribution analysis (Shapiro-Wilk normality test)
- Skewness and kurtosis assessment
- Value at Risk (VaR) and Conditional VaR (CVaR) calculations

### 3. **Hedging Strategies**

#### Static Exchange Rate Hedge
- Hedge ratio: -1.10
- Risk reduction: ~2% reduction in daily volatility
- Uses fixed beta calculated over entire period

#### Dynamic Exchange Rate Hedge
- Rolls hedge ratio based on 60-day trailing window
- Avoids look-ahead bias
- Without leverage limits: Similar results to static hedge
- With leverage cap (±2): 550 bps variance reduction

#### Climate-Based Regression Models
Three regression models analyzing climate impact on apple prices:
1. **Full Model**: All regions + all climate variables (R² = 0.09, Adj. R² = 0.03)
2. **China Only**: Shandong + Shaanxi climate data (R² = 0.04, Adj. R² = 0.036)
3. **Multi-Region**: China + USA (Washington) + Italy (Bolzano) (R² = 0.058, Adj. R² = 0.046)

### 4. **Key Findings**

- **Cross-hedging viability**: Low correlation with US-traded commodities rules out effective cross-hedging
- **Exchange rate hedge effectiveness**: 2% daily volatility reduction is more practical than climate-based hedging
- **Climate impact**: Climate variables explain ~5% of price variance - marginally useful for hedging
- **Market risk**: 
  - VaR (95% confidence): ~3% daily
  - VaR (99% confidence): ~5% daily
  - Max drawdown: 57% (2022 peak to 2024 trough)

## Required Data Files

The following files must be present in the `data/` directory:

- `APFUTURES2020.txt` - Apple futures 2020
- `APFUTURES2021.txt` - Apple futures 2021
- `APFUTURES2022.txt` - Apple futures 2022
- `APFUTURES2023.txt` - Apple futures 2023
- `APFUTURES2024.txt` - Apple futures 2024
- `APFUTURES2025.txt` - Apple futures 2025
- `taxa de juros china.txt` - China interest rates (from TradingView)
- `apple_dfs_backup.csv` - Backup copy of processed apple data

## Installation & Setup

### Prerequisites
- Python 3.8+
- Jupyter Notebook or JupyterLab

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Running the Analysis

1. Open the notebook:
```bash
jupyter notebook notebooks/Apple.ipynb
```

2. The notebook supports two execution environments:
   - **Google Colab**: Automatically detects Colab paths
   - **Local PC**: Uses paths defined in `YOUR_LOCAL_PC_BASE_PATH` variable

## Data Sources

- **Apple Futures**: Zhengzhou Commodity Exchange (CZCE)
- **Commodity Futures**: Yahoo Finance (yfinance)
- **Exchange Rates**: Yahoo Finance (CNY=X)
- **Interest Rates**: 
  - USA: Federal Reserve (^IRX)
  - China: TradingView historical data
- **Climate Data**: NASA POWER API (https://power.larc.nasa.gov/)

## Major Apple Producing Regions Analyzed

- **China**: Shaanxi (Yan'an/Luochuan), Shandong (Yantai)
- **USA**: Washington (Yakima Valley)
- **Italy**: Bolzano (South Tyrol)
- **Brazil**: Vacaria
- **Poland**: Grojec (Mazovia)
- **France**: Angers (Loire Valley)
- **Turkey**: Isparta, Karaman, Nigde
- **India**: Srinagar (J&K), Shimla (Himachal Pradesh)
- **Iran**: Urmia, Damavand
- **Russia**: Krasnodar, Nalchik, Voronezh, Belgorod

## Dependencies

See `requirements.txt` for complete list. Main packages:
- pandas
- numpy
- matplotlib
- seaborn
- yfinance
- statsmodels
- scipy
- requests (for NASA API)

## Methodology Notes

### Continuous Futures Construction
The continuous futures series is created by:
1. Ranking two nearest-to-expire contracts by date
2. Applying weight-based interpolation 5 days before expiration
3. Smoothing transitions using weighted averages

### Look-Ahead Bias Avoidance
- Dynamic hedge ratios are lagged by 1 period
- All parameters calculated from historical data only
- No future information leaked into past calculations

### Climate Data Processing
- Daily observations from NASA POWER API
- Missing values (-999) replaced with NaN
- Forward-fill method used to align dates with futures data
- VIF (Variance Inflation Factor) analysis to detect multicollinearity

## Future Improvements

1. **Advanced hedging techniques**: Options-based strategies, futures spreads
2. **Machine learning**: Predictive models for apple prices
3. **Expanded climate analysis**: Non-linear relationships, seasonal patterns
4. **Real-time monitoring**: Live hedge ratio adjustment
5. **Scenario analysis**: Stress testing under extreme climate events

## Author

Analysis conducted as a comprehensive study of agricultural futures hedging strategies.

## License

This project is provided for educational and research purposes.

## References

- CZCE Documentation: https://www.czce.com.cn/

---

**Last Updated**: December 2025
