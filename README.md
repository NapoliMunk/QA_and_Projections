# Qunataive_and_Projections
is a team project to demonstrate our collective ability to conduct financial analysis &amp; draw increasingly accurate predictions of major companies we deemed Heavy Hitters or simply Too Big To Fail within our economy and compare there metrics to the S&P 500.

The Great Recession of 2008 taught us no matter what the causation is certain companies are too big to fail, and the FED & there Reserves, will come to their rescue.

In this project, we selected 5 major companies (APPLE INC, MICROSOFT, GOOGLE, AMAZON, META) with the highest market caps and strongest influence in our economy to run a five-year historical return and compare them with the overall performance of the market using the S&P 500 index returns within the same five- year time period.

Once we determine their historical performance over the last 5 years, we’ll set the weights and investment capital to project potential future returns using Monte Carlo simulations.

We followed the steps below to execute the project:

 #- Import Libraries needed and API from Alpaca 
```import os
import requests
import pandas as pd
from dotenv import load_dotenv
import alpaca_trade_api as tradeapi
from alpaca_trade_api.rest import REST, TimeFrame
import seaborn as sns
from MCForecastTools import MCSimulation
%matplotlib inline
```

#- Set Alpaca API key and secret
    Create the Alpaca API object

# Set start and end dates of five years back from today.
  Sample results may vary from the solution based on the time frame chosen

# Set the ticker information
```tickers = ["AAPL","MSFT","GOOG","GOOGL","AMZN","META","SPY"]```

# Reorganize the DataFrame
  Separate ticker data

# Concatenate the ticker DataFrames

# Create and empty DataFrame for closing prices
# Fetch the closing prices of AAPL, MSFT, GOOG, GOOGL, AMZN, META, SPY

# Calculate Daily Returns
# Plot the daily returns/# Visualize the distribution of percent change 
CALCULATE AND PLOT CUMULATIVE RETURNS OF ALL PORTFOLIOS

# Calculate the standard deviations

# Calculate the annualized standard deviation (252 trading days)
# Calculate and plot the rolling standard deviation Heavy Hitters portfolio using a 100-day window


# Calculate and plot the rolling standard deviation Heavy Hitters portfolio using a 100-day window

# Calculate the correlation

# Calculate covariance of AAPL, MSFT, GOOG, GOOGL, AMZN, META
# Calculate variance of S&P 500


# Computing beta for AAPL, MSFT, GOOG, GOOGL, AMZN, META

calculate and visualize the Sharpe ratios using a bar plot

Calculate the weighted returns for the Heavy Hitters portfolio assuming an equal number of shares for each stock

Calculate the weighted returns for the Heavy Hitters portfolio different number of shares for each stock

# Plot simulation outcomes
# Fetch summary statistics from the Monte Carlo simulation results

Calculate the expected portfolio return at the 95% lower and upper confidence intervals based on a $500,000 initial investment.












