[![Python Version](https://img.shields.io/pypi/pyversions/pandas_ta.svg)](https://pypi.org/project/pandas_ta/)
[![PyPi Version](https://img.shields.io/pypi/v/pandas_ta.svg)](https://pypi.org/project/pandas_ta/)
[![Package Status](https://img.shields.io/pypi/status/pandas_ta.svg)](https://pypi.org/project/pandas_ta/)
[![Downloads](https://img.shields.io/pypi/dm/pandas_ta.svg?style=flat)](https://pypistats.org/packages/pandas_ta)

# Technical Analysis Library in Python 3.7
![Example Chart](/images/TA_Chart.png)

Technical Analysis (TA) is an easy to use library that is built upon Python's Pandas library with more than 100 Indicators.  These indicators are comminly used for financial time series datasets with columns or labels similar to: datetime, open, high, low, close, volume, et al.  Many commonly used indicators are included, such as: _Moving Average Convergence Divergence_ (*MACD*), _Hull Exponential Moving Average_ (*HMA*), _Bollinger Bands_ (*BBANDS*), _On-Balance Volume_ (*OBV*), _Aroon & Aroon Oscillator_ (*AROON*) and more.

This version contains both the orignal code branch as well as a newly refactored branch with the option to use [Pandas DataFrame Extension](https://pandas.pydata.org/pandas-docs/stable/extending.html) mode. 
All the indicators return a named Series or a DataFrame in uppercase underscore parameter format.  For example, MACD(fast=12, slow=26, signal=9) will return a DataFrame with columns: ['MACD_12_26_9', 'MACDH_12_26_9', 'MACDS_12_26_9'].


## Features

* Has 100+ indicators and utility functions.
* Example Jupyter Notebook under the examples directory.
* Abbreviated Indicator names as listed below.
* *Extended Pandas DataFrame* as 'ta'.  See examples below.
* Easily add prefixes or suffixes or both to columns names.
* Categories similar to [TA-lib](https://github.com/mrjbq7/ta-lib/tree/master/docs/func_groups).


## Recent Changes

* Added indicators:
    - __Bias__ (bias)
    - __Choppiness Index__ (chop)
    - __Chande Kroll Stop__ (cksp)
    - __KDJ__ (kdj)
    - __Parabolic Stop and Reverse__ (psar)
    - __Price Distance__ (pdist)
    - __Psycholigical Line__ (psl)
    - __Weighted Closing Price__ (wcp)
* Added utilities:
    - __Above__ (above)
    - __Above Value__ (above_value)
    - __Below__ (below)
    - __Below Value__ (below_value)
* User Added Indicators:
    - __Aberration__ (aberration)
    - __BRAR__ (brar)
* Corrected Indicators:
    - __Absolute Price Oscillator__ (apo)
    - __Aroon & Aroon Oscillator__ (aroon)
        * Fixed indicator and included oscillator in returned dataframe
    - __Bollinger Bands__ (bbands)
    - __Commodity Channel Index__ (cci)
    - __Chande Momentum Oscillator__ (cmo)

## What is a Pandas DataFrame Extension?

A [Pandas DataFrame Extension](https://pandas.pydata.org/pandas-docs/stable/extending.html), extends a DataFrame allowing one to add more functionality and features to Pandas to suit your needs.  As such, it is now easier to run Technical Analysis on existing Financial Time Series without leaving the current DataFrame.  This extension by default returns the Indicator result or it can append the result to the existing DataFrame by including the parameter 'append=True' in the method call. Examples below.



# Getting Started and Examples

## Installation (python 3)

```sh
$ pip install pandas_ta
```

## Latest Version
```sh
$ pip install -U git+https://github.com/twopirllc/pandas-ta
```

## **Quick Start** using the DataFrame Extension

```python
import pandas as pd
import pandas_ta as ta

# Load data
df = pd.read_csv('symbol.csv', sep=',')

# Calculate Returns and append to the df DataFrame
df.ta.log_return(cumulative=True, append=True)
df.ta.percent_return(cumulative=True, append=True)

# New Columns with results
df.columns

# Take a peek
df.tail()

# vv Continue Post Processing vv
```

## Module and Indicator Help

```python
import pandas as pd
import pandas_ta as ta

# Help about this, 'ta', extension
help(pd.DataFrame().ta)

# List of all indicators
pd.DataFrame().ta.indicators()

# Help about the log_return indicator
help(ta.log_return)

# Help about the log_return indicator as a DataFrame Extension
help(pd.DataFrame().ta.log_return)
```

## New DataFrame kwargs: *prefix* and *suffix*

```python
prehl2 = df.ta.hl2(prefix="pre")
print(prehl2.columns)  # "pre_HL2"

endhl2 = df.ta.hl2(suffix="end")
print(endhl2.columns)  # "HL2_end"

bothhl2 = df.ta.hl2(prefix="pre", suffix="end")
print(bothhl2.columns)  # "pre_HL2_end"
```

## New DataFrame Properties: *reverse* & *datetime_ordered*

```python
# The 'reverse' is a helper property that returns the DataFrame
# in reverse order
df = df.ta.reverse

# The 'datetime_ordered' property returns True if the DataFrame
# index is of Pandas datetime64 and df.index[0] < df.index[-1]
# Otherwise it return False
time_series_in_order = df.ta.datetime_ordered
```

## DataFrame Property: *adjusted*

```python
# Set ta to default to an adjusted column, 'adj_close', overriding default 'close'
df.ta.adjusted = 'adj_close'
df.ta.sma(length=10, append=True)

# To reset back to 'close', set adjusted back to None
df.ta.adjusted = None
```


# Technical Analysis Indicators (by Category)

## _Momentum_ (25)

* _Awesome Oscillator_: **ao**
* _Absolute Price Oscillator_: **apo**
* _Bias_: **bias**
* _Balance of Power_: **bop**
* _BRAR_: **brar**
* _Commodity Channel Index_: **cci**
* _Center of Gravity_: **cg**
* _Chande Momentum Oscillator_: **cmo**
* _Coppock Curve_: **coppock**
* _Fisher Transform_: **fisher**
* _KDJ_: **kdj**
* _KST Oscillator_: **kst**
* _Moving Average Convergence Divergence_: **macd**
* _Momentum_: **mom**
* _Percentage Price Oscillator_: **ppo**
* _Psychological Line_: **psl**
* _Rate of Change_: **roc**
* _Relative Strength Index_: **rsi**
* _Relative Vigor Index_: **rvi**
* _Slope_: **slope*
* _Stochastic Oscillator_: **stoch**
* _Trix_: **trix**
* _True strength index_: **tsi**
* _Ultimate Oscillator_: **uo**
* _Williams %R_: **willr**


| _Moving Average Convergence Divergence_ (MACD) |
|:--------:|
| ![Example MACD](/images/SPY_MACD.png) |

## _Overlap_ (25)

* _Double Exponential Moving Average_: **dema**
* _Exponential Moving Average_: **ema**
* _Fibonacci's Weighted Moving Average_: **fwma**
* _High-Low Average_: **hl2**
* _High-Low-Close Average_: **hlc3**
    * Commonly known as 'Typical Price' in Technical Analysis literature
* _Hull Exponential Moving Average_: **hma**
* _Kaufman's Adaptive Moving Average_: **kama**
* _Ichimoku Kinkō Hyō_: **ichimoku**
    * Use: help(ta.ichimoku). Returns two DataFrames.
* _Linear Regression_: **linreg**
* _Midpoint_: **midpoint**
* _Midprice_: **midprice**
* _Open-High-Low-Close Average_: **ohlc4**
* _Pascal's Weighted Moving Average_: **pwma**
* _William's Moving Average_: **rma**
* _Simple Moving Average_: **sma**
* _Sine Weighted Moving Average_: **sinwma**
* _Symmetric Weighted Moving Average_: **swma**
* _T3 Moving Average_: **t3**
* _Triple Exponential Moving Average_: **tema**
* _Triangular Moving Average_: **trima**
* _Volume Weighted Average Price_: **vwap** 
* _Volume Weighted Moving Average_: **vwma**
* _Weighted Closing Price_: **wcp**
* _Weighted Moving Average_: **wma**
* _Zero Lag Moving Average_: **zlma**

| _Simple Moving Averages_ (SMA) and _Bollinger Bands_ (BBANDS) |
|:--------:|
| ![Example Chart](/images/TA_Chart.png) |

## _Performance_ (3)

Use parameter: cumulative=**True** for cumulative results.

* _Log Return_: **log_return**
* _Percent Return_: **percent_return**
* _Trend Return_: **trend_return**

| _Percent Return_ (Cumulative) with _Simple Moving Average_ (SMA) |
|:--------:|
| ![Example Cumulative Percent Return](/images/SPY_CumulativePercentReturn.png) |

## _Statistics_ (8)

* _Kurtosis_: **kurtosis**
* _Mean Absolute Deviation_: **mad**
* _Median_: **median**
* _Quantile_: **quantile**
* _Skew_: **skew**
* _Standard Deviation_: **stdev**
* _Variance_: **variance**
* _Z Score_: **zscore**

| _Z Score_ |
|:--------:|
| ![Example Z Score](/images/SPY_ZScore.png) |

## _Trend_ (14)

* _Average Directional Movement Index_: **adx**
* _Archer Moving Averages Trends_: **amat**
* _Aroon & Aroon Oscillator_: **aroon**
* _Choppiness Index_: **chop**
* _Chande Kroll Stop_: **cksp**
* _Decreasing_: **decreasing**
* _Detrended Price Oscillator_: **dpo**
* _Increasing_: **increasing**
* _Linear Decay_: **linear_decay**
* _Long Run_: **long_run**
* _Parabolic Stop and Reverse_: **psar**
* _Q Stick_: **qstick**
* _Short Run_: **short_run**
* _Vortex_: **vortex**

| _Average Directional Movement Index_ (ADX) |
|:--------:|
| ![Example ADX](/images/SPY_ADX.png) |

## _Utility_ (5)

* _Above_: **above**
* _Above Value_: **above_value**
* _Below_: **below**
* _Below Value_: **below_value**
* _Cross_: **cross**

## _Volatility_ (10)

* _Aberration_: **aberration**
* _Acceleration Bands_: **accbands**
* _Average True Range_: **atr**
* _Bollinger Bands_: **bbands**
* _Donchian Channel_: **donchian**
* _Keltner Channel_: **kc**
* _Mass Index_: **massi**
* _Normalized Average True Range_: **natr**
* _Price Distance_: **pdist**
* _True Range_: **true_range**

| _Average True Range_ (ATR) |
|:--------:|
| ![Example ATR](/images/SPY_ATR.png) |

## _Volume_ (13)

* _Accumulation/Distribution Index_: **ad**
* _Accumulation/Distribution Oscillator_: **adosc**
* _Archer On-Balance Volume_: **aobv**
* _Chaikin Money Flow_: **cmf**
* _Elder's Force Index_: **efi**
* _Ease of Movement_: **eom**
* _Money Flow Index_: **mfi**
* _Negative Volume Index_: **nvi**
* _On-Balance Volume_: **obv**
* _Positive Volume Index_: **pvi**
* _Price-Volume_: **pvol**
* _Price Volume Trend_: **pvt**
* _Volume Profile_: **vp**

| _On-Balance Volume_ (OBV) |
|:--------:|
| ![Example OBV](/images/SPY_OBV.png) |


# Contributors
* [allahyarzadeh](https://github.com/allahyarzadeh)
* [lluissalord](https://github.com/lluissalord)


# Inspiration
* TradingView: http://www.tradingview.com
* Original TA-LIB: http://ta-lib.org/
* Bukosabino: https://github.com/bukosabino/ta

Please leave any comments, feedback, or suggestions.