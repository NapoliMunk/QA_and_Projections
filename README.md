# Quantaive_Analysis_and_Projections
is a team project to demonstrate our collective ability to conduct financial analysis &amp; draw increasingly accurate predictions of major companies we deemed Heavy Hitters or simply Too Big To Fail within our economy and compare there metrics to the S&P 500 & one commodity being gas.

We selected 9 major companies:
- APPL
- MSFT
- T
- GOOG/GOOGL
- AMZN
- META
- SPY
- XOM

Once we determined their historical performance over the last 5 years, we’ll set the weights and investment capital to project potential future  30 year returns using Monte Carlo simulations in hopes of finding some  insightful tips on how to adjust our strategy.

We followed the steps to execute our analysis and prediction simulation.

#- Import Libraries needed and API from Alpaca 
```import os
import requests
from MCForecastTools import MCSimulation
import pandas as pd
import hvplot.pandas
from dotenv import load_dotenv
import alpaca_trade_api as tradeapi
from alpaca_trade_api.rest import REST, TimeFrame
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
plt.style.use('ggplot')
import plotly.express as px


%matplotlib inline
```

#- Set Alpaca API key and secret
    Create the Alpaca API object
``` 
alpaca_api_key = os.getenv("ALPACA_API_KEY")
alpaca_secret_key = os.getenv("ALPACA_SECRET_KEY")
```

# Set start and end dates of five years back from today.
  Sample results may vary from the solution based on the time frame chosen
```
start_date = pd.Timestamp('2017-10-31', tz='America/New_York').isoformat()
end_date = pd.Timestamp('2022-10-31', tz='America/New_York').isoformat()
```
# Set the ticker information
```tickers = ["AAPL","MSFT","T","GOOG","GOOGL","AMZN","META","SPY","XOM"]```

# Reorganize the DataFrame
  Separate ticker data
```
AAPL=hh_5_year[hh_5_year['symbol']=='AAPL'].drop('symbol',axis=1)  # this is done for each individual ticker/stock
```
# Concatenate the ticker DataFrames
```
hh_5_year = pd.concat([AAPL, MSFT,T,GOOG,GOOGL,AMZN,META,SPY,XOM],axis=1, keys=['AAPL','MSFT','T','GOOG','GOOGL','AMZN','META','SPY','XOM'])
```
# Create and empty DataFrame for closing prices
# Fetch the closing prices of all tickers

```
hh_closing_prices["AAPL"] = hh_5_year["AAPL"]["close"] #this is done for each individual ticker
```

# Calculate Daily Returns
```
hh_portfolio = hh_closing_prices[['AAPL','MSFT','T','GOOG','GOOGL','AMZN','META','SPY','XOM']].pct_change()
```

# Plot the daily returns & Visualize the distribution of percent change 
```
hh_return_plot = hh_portfolio.plot(figsize=(12,8))
```

# Calculate the standard deviations
```
hh_std = hh_portfolio.std()
```
# Calculate the annualized standard deviation (252 trading days)
```
annual_std = hh_std * year**(1/2)
```

# Calculate and plot the rolling standard deviation Heavy Hitters portfolio using a 126-day window

```
hh_portfolio.rolling(window=126).std().plot.line(figsize=(12,8))
```

# Calculate the correlation
```
Correlation=hh_portfolio.corr().copy()
```
# Calculate covariance of tickers
```
APPL_cov=hh_portfolio['AAPL'].cov(hh_portfolio['SPY'])
```
# Calculate variance of S&P 500
```
variance=hh_portfolio['SPY'].var()
```

# Computing beta for our tickers

- calculate and visualize the Sharpe & Sortino ratios using a bar plot
- ``` Sharpe.plot.bar(title='Sharpe Ratios',figsize=(10,7)) ```

- Calculate the weighted returns for the Heavy Hitters portfolio assuming an equal number of shares for each stock
- ```SIM= MCSimulation(
    portfolio_data= heavy_hitters_df,
    num_simulation = num_sims,
    weights= [.12,.11,.11,.11,.11,.11,.11,.11,.11],
    num_trading_days = 252 * 30)
```

- Calculate the weighted returns for the Heavy Hitters portfolio different number of shares for each stock
- ```
- SIM_SPY= MCSimulation(
    portfolio_data= heavy_hitters_df,
    num_simulation = 200,
    weights= [.16,.11,.6,.11,.11,.16,.6,.18,.4],
    num_trading_days = 252 * 30) 
   ```
# Plot simulation outcomes
- ``` line_plot = SIM.plot_simulation()
```
-```
line_plot_safe = SIM_SPY.plot_simulation()
```

# Fetch summary statistics from the Monte Carlo simulation results

- Calculate the expected portfolio return at the 95% lower and upper confidence intervals based on a $500,000 initial investment.

``` 
ci_lower = round(sum_stats[8]*500000,9)
ci_upper = round(sum_stats[9]*500000,9)
```










