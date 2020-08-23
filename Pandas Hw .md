```python

```

 #  A Whale off the Port(folio)

 In this assignment, you'll get to use what you've learned this week to evaluate the performance among various algorithmic, hedge, and mutual fund portfolios and compare them against the S&P 500.

 #  A Whale off the Port(folio)

 In this assignment, you'll get to use what you've learned this week to evaluate the performance among various algorithmic, hedge, and mutual fund portfolios and compare them against the S&P 500.


```python
import pandas as pd
import os 
import numpy as np
import datetime as dt
from pathlib import Path
%matplotlib inline
```


```python
# Data Cleaning

In this section, you will need to read the CSV files into DataFrames and perform any necessary data cleaning steps. After cleaning, combine all DataFrames into a single DataFrame.

Files:
1. whale_returns.csv
2. algo_returns.csv
3. sp500_history.csv
```

## Whale Returns

Read the Whale Portfolio daily returns and clean the data


```python

```


```python
# Reading whale returns
whale_returns_csv = Path("Resources/whale_returns.csv")
whale_returns_dataframe= pd.read_csv(whale_returns_csv,)
whale_returns_dataframe.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>SOROS FUND MANAGEMENT LLC</th>
      <th>PAULSON &amp; CO.INC.</th>
      <th>TIGER GLOBAL MANAGEMENT LLC</th>
      <th>BERKSHIRE HATHAWAY INC</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2015-03-02</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015-03-03</td>
      <td>-0.001266</td>
      <td>-0.004981</td>
      <td>-0.000496</td>
      <td>-0.006569</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2015-03-04</td>
      <td>0.002230</td>
      <td>0.003241</td>
      <td>-0.002534</td>
      <td>0.004213</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2015-03-05</td>
      <td>0.004016</td>
      <td>0.004076</td>
      <td>0.002355</td>
      <td>0.006726</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2015-03-06</td>
      <td>-0.007905</td>
      <td>-0.003574</td>
      <td>-0.008481</td>
      <td>-0.013098</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Count nulls
whale_returns_dataframe.isnull().sum()
```




    Date                           0
    SOROS FUND MANAGEMENT LLC      1
    PAULSON & CO.INC.              1
    TIGER GLOBAL MANAGEMENT LLC    1
    BERKSHIRE HATHAWAY INC         1
    dtype: int64




```python
# Drop nulls
whale_returns_dataframe=whale_returns_dataframe.dropna().copy()
whale_returns_dataframe
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>SOROS FUND MANAGEMENT LLC</th>
      <th>PAULSON &amp; CO.INC.</th>
      <th>TIGER GLOBAL MANAGEMENT LLC</th>
      <th>BERKSHIRE HATHAWAY INC</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>2015-03-03</td>
      <td>-0.001266</td>
      <td>-0.004981</td>
      <td>-0.000496</td>
      <td>-0.006569</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2015-03-04</td>
      <td>0.002230</td>
      <td>0.003241</td>
      <td>-0.002534</td>
      <td>0.004213</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2015-03-05</td>
      <td>0.004016</td>
      <td>0.004076</td>
      <td>0.002355</td>
      <td>0.006726</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2015-03-06</td>
      <td>-0.007905</td>
      <td>-0.003574</td>
      <td>-0.008481</td>
      <td>-0.013098</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2015-03-09</td>
      <td>0.000582</td>
      <td>0.004225</td>
      <td>0.005843</td>
      <td>-0.001652</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1055</th>
      <td>2019-04-25</td>
      <td>-0.000285</td>
      <td>-0.001291</td>
      <td>-0.005153</td>
      <td>0.004848</td>
    </tr>
    <tr>
      <th>1056</th>
      <td>2019-04-26</td>
      <td>0.008149</td>
      <td>0.009162</td>
      <td>0.012355</td>
      <td>0.010434</td>
    </tr>
    <tr>
      <th>1057</th>
      <td>2019-04-29</td>
      <td>0.001254</td>
      <td>0.002719</td>
      <td>0.006251</td>
      <td>0.005223</td>
    </tr>
    <tr>
      <th>1058</th>
      <td>2019-04-30</td>
      <td>-0.001295</td>
      <td>-0.002211</td>
      <td>-0.000259</td>
      <td>-0.003702</td>
    </tr>
    <tr>
      <th>1059</th>
      <td>2019-05-01</td>
      <td>-0.005847</td>
      <td>-0.001341</td>
      <td>-0.007936</td>
      <td>-0.007833</td>
    </tr>
  </tbody>
</table>
<p>1059 rows × 5 columns</p>
</div>



## Algorithmic Daily Returns

Read the algorithmic daily returns and clean the data


```python
# Reading algorithmic returns
algo_returns_csv = Path("Resources/algo_returns.csv")
algo_returns_dataframe= pd.read_csv(algo_returns_csv,)
algo_returns_dataframe.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Algo 1</th>
      <th>Algo 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2014-05-28</td>
      <td>0.001745</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2014-05-29</td>
      <td>0.003978</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2014-05-30</td>
      <td>0.004464</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2014-06-02</td>
      <td>0.005692</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2014-06-03</td>
      <td>0.005292</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Count nulls
algo_returns_dataframe.isnull().sum()
```




    Date      0
    Algo 1    0
    Algo 2    6
    dtype: int64




```python
# Drop nulls
algo_returns_dataframe=algo_returns_dataframe.dropna().copy()
algo_returns_dataframe.head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Algo 1</th>
      <th>Algo 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>2014-06-05</td>
      <td>0.004062</td>
      <td>0.013285</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2014-06-06</td>
      <td>0.001857</td>
      <td>0.008284</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2014-06-09</td>
      <td>-0.005012</td>
      <td>0.005668</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2014-06-10</td>
      <td>0.004406</td>
      <td>-0.000735</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2014-06-11</td>
      <td>0.004760</td>
      <td>-0.003761</td>
    </tr>
  </tbody>
</table>
</div>



## S&P 500 Returns

Read the S&P500 Historic Closing Prices and create a new daily returns DataFrame from the data. 


```python
# Reading S&P 500 Closing Prices
sp500_history_csv = Path("Resources/sp500_history.csv")
sp500_history_csv_dataframe= pd.read_csv(sp500_history_csv,)
sp500_history_csv_dataframe.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Close</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>23-Apr-19</td>
      <td>$2933.68</td>
    </tr>
    <tr>
      <th>1</th>
      <td>22-Apr-19</td>
      <td>$2907.97</td>
    </tr>
    <tr>
      <th>2</th>
      <td>18-Apr-19</td>
      <td>$2905.03</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17-Apr-19</td>
      <td>$2900.45</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16-Apr-19</td>
      <td>$2907.06</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Check Data Types
sp500_history_csv_dataframe.dtypes
```




    Date     object
    Close    object
    dtype: object




```python
# Fix Data Types
# YOUR CODE HERE
```




    Close    float64
    dtype: object




```python
# Calculate Daily Returns
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Close</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2012-10-01</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2012-10-02</th>
      <td>0.000872</td>
    </tr>
    <tr>
      <th>2012-10-03</th>
      <td>0.003624</td>
    </tr>
    <tr>
      <th>2012-10-04</th>
      <td>0.007174</td>
    </tr>
    <tr>
      <th>2012-10-05</th>
      <td>-0.000322</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Drop nulls
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Close</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2012-10-02</th>
      <td>0.000872</td>
    </tr>
    <tr>
      <th>2012-10-03</th>
      <td>0.003624</td>
    </tr>
    <tr>
      <th>2012-10-04</th>
      <td>0.007174</td>
    </tr>
    <tr>
      <th>2012-10-05</th>
      <td>-0.000322</td>
    </tr>
    <tr>
      <th>2012-10-08</th>
      <td>-0.003457</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Rename Column
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>S&amp;P 500</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2012-10-02</th>
      <td>0.000872</td>
    </tr>
    <tr>
      <th>2012-10-03</th>
      <td>0.003624</td>
    </tr>
    <tr>
      <th>2012-10-04</th>
      <td>0.007174</td>
    </tr>
    <tr>
      <th>2012-10-05</th>
      <td>-0.000322</td>
    </tr>
    <tr>
      <th>2012-10-08</th>
      <td>-0.003457</td>
    </tr>
  </tbody>
</table>
</div>



## Combine Whale, Algorithmic, and S&P 500 Returns


```python
# Concatenate all DataFrames into a single DataFrame
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SOROS FUND MANAGEMENT LLC</th>
      <th>PAULSON &amp; CO.INC.</th>
      <th>TIGER GLOBAL MANAGEMENT LLC</th>
      <th>BERKSHIRE HATHAWAY INC</th>
      <th>Algo 1</th>
      <th>Algo 2</th>
      <th>S&amp;P 500</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2015-03-03</th>
      <td>-0.001266</td>
      <td>-0.004981</td>
      <td>-0.000496</td>
      <td>-0.006569</td>
      <td>-0.001942</td>
      <td>-0.000949</td>
      <td>-0.004539</td>
    </tr>
    <tr>
      <th>2015-03-04</th>
      <td>0.002230</td>
      <td>0.003241</td>
      <td>-0.002534</td>
      <td>0.004213</td>
      <td>-0.008589</td>
      <td>0.002416</td>
      <td>-0.004389</td>
    </tr>
    <tr>
      <th>2015-03-05</th>
      <td>0.004016</td>
      <td>0.004076</td>
      <td>0.002355</td>
      <td>0.006726</td>
      <td>-0.000955</td>
      <td>0.004323</td>
      <td>0.001196</td>
    </tr>
    <tr>
      <th>2015-03-06</th>
      <td>-0.007905</td>
      <td>-0.003574</td>
      <td>-0.008481</td>
      <td>-0.013098</td>
      <td>-0.004957</td>
      <td>-0.011460</td>
      <td>-0.014174</td>
    </tr>
    <tr>
      <th>2015-03-09</th>
      <td>0.000582</td>
      <td>0.004225</td>
      <td>0.005843</td>
      <td>-0.001652</td>
      <td>-0.005447</td>
      <td>0.001303</td>
      <td>0.003944</td>
    </tr>
  </tbody>
</table>
</div>



---

# Portfolio Analysis

In this section, you will calculate and visualize performance and risk metrics for the portfolios.

## Performance

Calculate and Plot the daily returns and cumulative returns. Does any portfolio outperform the S&P 500? 


```python
# Plot daily returns
# YOUR CODE HERE
```




    <matplotlib.axes._subplots.AxesSubplot at 0x173bc74f2b0>




![png](output_26_1.png)



```python
# Plot cumulative returns
# YOUR CODE HERE
```




    <matplotlib.axes._subplots.AxesSubplot at 0x173bccca780>




![png](output_27_1.png)


## Risk

Determine the _risk_ of each portfolio:

1. Create a box plot for each portfolio. 
2. Calculate the standard deviation for all portfolios
4. Determine which portfolios are riskier than the S&P 500
5. Calculate the Annualized Standard Deviation


```python
# Box plot to visually show risk
# YOUR CODE HERE
```




    <matplotlib.axes._subplots.AxesSubplot at 0x173bcfc0d30>




![png](output_29_1.png)



```python
# Daily Standard Deviations
# Calculate the standard deviation for each portfolio. 
# Which portfolios are riskier than the S&P 500?
# YOUR CODE HERE
```




    SOROS FUND MANAGEMENT LLC      0.007895
    PAULSON & CO.INC.              0.007023
    TIGER GLOBAL MANAGEMENT LLC    0.010894
    BERKSHIRE HATHAWAY INC         0.012919
    Algo 1                         0.007620
    Algo 2                         0.008342
    S&P 500                        0.008554
    dtype: float64




```python
# Determine which portfolios are riskier than the S&P 500
# YOUR CODE HERE
```




    SOROS FUND MANAGEMENT LLC      False
    PAULSON & CO.INC.              False
    TIGER GLOBAL MANAGEMENT LLC     True
    BERKSHIRE HATHAWAY INC          True
    Algo 1                         False
    Algo 2                         False
    S&P 500                        False
    dtype: bool




```python
# Calculate the annualized standard deviation (252 trading days)
# YOUR CODE HERE
```




    SOROS FUND MANAGEMENT LLC      0.125335
    PAULSON & CO.INC.              0.111488
    TIGER GLOBAL MANAGEMENT LLC    0.172936
    BERKSHIRE HATHAWAY INC         0.205077
    Algo 1                         0.120967
    Algo 2                         0.132430
    S&P 500                        0.135786
    dtype: float64



---

## Rolling Statistics

Risk changes over time. Analyze the rolling statistics for Risk and Beta. 

1. Plot the rolling standard deviation of the various portfolios along with the rolling standard deviation of the S&P 500 (consider a 21 day window). Does the risk increase for each of the portfolios at the same time risk increases in the S&P?
2. Construct a correlation table for the algorithmic, whale, and S&P 500 returns. Which returns most closely mimic the S&P?
3. Choose one portfolio and plot a rolling beta between that portfolio's returns and S&P 500 returns. Does the portfolio seem sensitive to movements in the S&P 500?
4. An alternative way to calculate a rolling window is to take the exponentially weighted moving average. This is like a moving window average, but it assigns greater importance to more recent observations. Try calculating the ewm with a 21 day half-life.


```python
# Calculate and plot the rolling standard deviation for
# the S&P 500 and whale portfolios using a 21 trading day window
# YOUR CODE HERE
```




    <matplotlib.axes._subplots.AxesSubplot at 0x173bd31e438>




![png](output_35_1.png)



```python
# Construct a correlation table
# YOUR CODE HERE
```




<style  type="text/css" >
    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col0 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col1 {
            background-color:  #96cb66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col2 {
            background-color:  #79bc66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col3 {
            background-color:  #a7d366;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col4 {
            background-color:  #309866;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col5 {
            background-color:  #c1e066;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col6 {
            background-color:  #c6e266;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col0 {
            background-color:  #8ec666;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col1 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col2 {
            background-color:  #52a866;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col3 {
            background-color:  #5bad66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col4 {
            background-color:  #209066;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col5 {
            background-color:  #8cc666;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col6 {
            background-color:  #8ac466;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col0 {
            background-color:  #5aac66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col1 {
            background-color:  #399c66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col2 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col3 {
            background-color:  #2f9766;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col4 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col5 {
            background-color:  #4ea666;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col6 {
            background-color:  #7abc66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col0 {
            background-color:  #a3d166;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col1 {
            background-color:  #60b066;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col2 {
            background-color:  #4fa766;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col3 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col4 {
            background-color:  #279366;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col5 {
            background-color:  #8fc766;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col6 {
            background-color:  #a7d366;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col0 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col1 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col2 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col3 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col4 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col5 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col6 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col0 {
            background-color:  #bede66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col1 {
            background-color:  #8fc766;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col2 {
            background-color:  #69b466;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col3 {
            background-color:  #8fc766;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col4 {
            background-color:  #259266;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col5 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col6 {
            background-color:  #cde666;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col0 {
            background-color:  #c2e066;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col1 {
            background-color:  #8cc666;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col2 {
            background-color:  #8cc666;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col3 {
            background-color:  #a6d266;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col4 {
            background-color:  #239166;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col5 {
            background-color:  #cde666;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col6 {
            background-color:  #ffff66;
            color:  #000000;
        }</style><table id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >SOROS FUND MANAGEMENT LLC</th>        <th class="col_heading level0 col1" >PAULSON & CO.INC. </th>        <th class="col_heading level0 col2" >TIGER GLOBAL MANAGEMENT LLC</th>        <th class="col_heading level0 col3" >BERKSHIRE HATHAWAY INC</th>        <th class="col_heading level0 col4" >Algo 1</th>        <th class="col_heading level0 col5" >Algo 2</th>        <th class="col_heading level0 col6" >S&P 500</th>    </tr></thead><tbody>
                <tr>
                        <th id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7level0_row0" class="row_heading level0 row0" >SOROS FUND MANAGEMENT LLC</th>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col0" class="data row0 col0" >1</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col1" class="data row0 col1" >0.699914</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col2" class="data row0 col2" >0.561243</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col3" class="data row0 col3" >0.75436</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col4" class="data row0 col4" >0.321211</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col5" class="data row0 col5" >0.826873</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col6" class="data row0 col6" >0.837864</td>
            </tr>
            <tr>
                        <th id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7level0_row1" class="row_heading level0 row1" >PAULSON & CO.INC. </th>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col0" class="data row1 col0" >0.699914</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col1" class="data row1 col1" >1</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col2" class="data row1 col2" >0.434479</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col3" class="data row1 col3" >0.545623</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col4" class="data row1 col4" >0.26884</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col5" class="data row1 col5" >0.678152</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col6" class="data row1 col6" >0.669732</td>
            </tr>
            <tr>
                        <th id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7level0_row2" class="row_heading level0 row2" >TIGER GLOBAL MANAGEMENT LLC</th>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col0" class="data row2 col0" >0.561243</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col1" class="data row2 col1" >0.434479</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col2" class="data row2 col2" >1</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col3" class="data row2 col3" >0.424423</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col4" class="data row2 col4" >0.164387</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col5" class="data row2 col5" >0.507414</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col6" class="data row2 col6" >0.623946</td>
            </tr>
            <tr>
                        <th id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7level0_row3" class="row_heading level0 row3" >BERKSHIRE HATHAWAY INC</th>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col0" class="data row3 col0" >0.75436</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col1" class="data row3 col1" >0.545623</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col2" class="data row3 col2" >0.424423</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col3" class="data row3 col3" >1</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col4" class="data row3 col4" >0.292033</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col5" class="data row3 col5" >0.688082</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col6" class="data row3 col6" >0.751371</td>
            </tr>
            <tr>
                        <th id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7level0_row4" class="row_heading level0 row4" >Algo 1</th>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col0" class="data row4 col0" >0.321211</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col1" class="data row4 col1" >0.26884</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col2" class="data row4 col2" >0.164387</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col3" class="data row4 col3" >0.292033</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col4" class="data row4 col4" >1</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col5" class="data row4 col5" >0.288243</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col6" class="data row4 col6" >0.279494</td>
            </tr>
            <tr>
                        <th id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7level0_row5" class="row_heading level0 row5" >Algo 2</th>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col0" class="data row5 col0" >0.826873</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col1" class="data row5 col1" >0.678152</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col2" class="data row5 col2" >0.507414</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col3" class="data row5 col3" >0.688082</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col4" class="data row5 col4" >0.288243</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col5" class="data row5 col5" >1</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col6" class="data row5 col6" >0.858764</td>
            </tr>
            <tr>
                        <th id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7level0_row6" class="row_heading level0 row6" >S&P 500</th>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col0" class="data row6 col0" >0.837864</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col1" class="data row6 col1" >0.669732</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col2" class="data row6 col2" >0.623946</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col3" class="data row6 col3" >0.751371</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col4" class="data row6 col4" >0.279494</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col5" class="data row6 col5" >0.858764</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col6" class="data row6 col6" >1</td>
            </tr>
    </tbody></table>




```python
# Calculate Beta for a single portfolio compared to the total market (S&P 500)
# (Your graph may differ, dependent upon which portfolio you are comparing)
# YOUR CODE HERE
```




    <matplotlib.axes._subplots.AxesSubplot at 0x173bed736a0>




![png](output_37_1.png)



```python
# Calculate a rolling window using the exponentially weighted moving average. 
# YOUR CODE HERE
```




    <matplotlib.axes._subplots.AxesSubplot at 0x173bf094240>




![png](output_38_1.png)


---

## Sharpe Ratios
In reality, investment managers and thier institutional investors look at the ratio of return-to-risk, and not just returns alone. (After all, if you could invest in one of two portfolios, each offered the same 10% return, yet one offered lower risk, you'd take that one, right?)

1. Using the daily returns, calculate and visualize the Sharpe ratios using a bar plot.
2. Determine whether the algorithmic strategies outperform both the market (S&P 500) and the whales portfolios.


```python
# Calculate annualized Sharpe Ratios
# YOUR CODE HERE
```




    SOROS FUND MANAGEMENT LLC      0.356417
    PAULSON & CO.INC.             -0.483570
    TIGER GLOBAL MANAGEMENT LLC   -0.121060
    BERKSHIRE HATHAWAY INC         0.621810
    Algo 1                         1.378648
    Algo 2                         0.501364
    S&P 500                        0.648267
    dtype: float64




```python
# Visualize the sharpe ratios as a bar plot
# YOUR CODE HERE
```




    <matplotlib.axes._subplots.AxesSubplot at 0x173bd954e10>




![png](output_42_1.png)


On the basis of this performance metric, do our algo strategies outperform both 'the market' and the whales? Type your answer here:

---

# Portfolio Returns

In this section, you will build your own portfolio of stocks, calculate the returns, and compare the results to the Whale Portfolios and the S&P 500. 

1. Visit [Google Sheets](https://docs.google.com/spreadsheets/) and use the in-built Google Finance function to choose 3-5 stocks for your own portfolio.
2. Download the data as CSV files and calculate the portfolio returns.
3. Calculate the returns for each stock.
4. Using those returns, calculate the weighted returns for your entire portfolio assuming an equal number of shares for each stock.
5. Add your portfolio returns to the DataFrame with the other portfolios and rerun the analysis. How does your portfolio fair?


## Your analysis should include the following:

- Using all portfolios:
 - The annualized standard deviation (252 trading days) for all portfolios.
 - The plotted rolling standard deviation using a 21 trading day window for all portfolios.
 - The calculated annualized Sharpe Ratios and the accompanying bar plot visualization.
 - A correlation table.
- Using your custom portfolio and one other of your choosing:
 - The plotted beta. 

## Choose 3-5 custom stocks with at last 1 year's worth of historic prices and create a DataFrame of the closing prices and dates for each stock.


```python
# Read the first stock
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Symbol</th>
      <th>NOCP</th>
    </tr>
    <tr>
      <th>Trade DATE</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-05-11</th>
      <td>GOOG</td>
      <td>1098.26</td>
    </tr>
    <tr>
      <th>2018-05-14</th>
      <td>GOOG</td>
      <td>1100.20</td>
    </tr>
    <tr>
      <th>2018-05-15</th>
      <td>GOOG</td>
      <td>1079.23</td>
    </tr>
    <tr>
      <th>2018-05-16</th>
      <td>GOOG</td>
      <td>1081.77</td>
    </tr>
    <tr>
      <th>2018-05-17</th>
      <td>GOOG</td>
      <td>1078.59</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Read the second stock
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Symbol</th>
      <th>NOCP</th>
    </tr>
    <tr>
      <th>Trade DATE</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-05-11</th>
      <td>AAPL</td>
      <td>188.59</td>
    </tr>
    <tr>
      <th>2018-05-14</th>
      <td>AAPL</td>
      <td>188.15</td>
    </tr>
    <tr>
      <th>2018-05-15</th>
      <td>AAPL</td>
      <td>186.44</td>
    </tr>
    <tr>
      <th>2018-05-16</th>
      <td>AAPL</td>
      <td>188.18</td>
    </tr>
    <tr>
      <th>2018-05-17</th>
      <td>AAPL</td>
      <td>186.99</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Read the third stock
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Symbol</th>
      <th>NOCP</th>
    </tr>
    <tr>
      <th>Trade DATE</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-05-11</th>
      <td>COST</td>
      <td>195.76</td>
    </tr>
    <tr>
      <th>2018-05-14</th>
      <td>COST</td>
      <td>195.88</td>
    </tr>
    <tr>
      <th>2018-05-15</th>
      <td>COST</td>
      <td>195.48</td>
    </tr>
    <tr>
      <th>2018-05-16</th>
      <td>COST</td>
      <td>198.71</td>
    </tr>
    <tr>
      <th>2018-05-17</th>
      <td>COST</td>
      <td>199.60</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Concatenate all stocks into a single DataFrame
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Symbol</th>
      <th>NOCP</th>
    </tr>
    <tr>
      <th>Trade DATE</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-05-11</th>
      <td>GOOG</td>
      <td>1098.26</td>
    </tr>
    <tr>
      <th>2018-05-14</th>
      <td>GOOG</td>
      <td>1100.20</td>
    </tr>
    <tr>
      <th>2018-05-15</th>
      <td>GOOG</td>
      <td>1079.23</td>
    </tr>
    <tr>
      <th>2018-05-16</th>
      <td>GOOG</td>
      <td>1081.77</td>
    </tr>
    <tr>
      <th>2018-05-17</th>
      <td>GOOG</td>
      <td>1078.59</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Reset the index
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Trade DATE</th>
      <th>Symbol</th>
      <th>NOCP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-05-11</td>
      <td>GOOG</td>
      <td>1098.26</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-05-14</td>
      <td>GOOG</td>
      <td>1100.20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-05-15</td>
      <td>GOOG</td>
      <td>1079.23</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018-05-16</td>
      <td>GOOG</td>
      <td>1081.77</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2018-05-17</td>
      <td>GOOG</td>
      <td>1078.59</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Pivot so that each column of prices represents a unique symbol
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Symbol</th>
      <th>AAPL</th>
      <th>COST</th>
      <th>GOOG</th>
    </tr>
    <tr>
      <th>Trade DATE</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-05-11</th>
      <td>188.59</td>
      <td>195.76</td>
      <td>1098.26</td>
    </tr>
    <tr>
      <th>2018-05-14</th>
      <td>188.15</td>
      <td>195.88</td>
      <td>1100.20</td>
    </tr>
    <tr>
      <th>2018-05-15</th>
      <td>186.44</td>
      <td>195.48</td>
      <td>1079.23</td>
    </tr>
    <tr>
      <th>2018-05-16</th>
      <td>188.18</td>
      <td>198.71</td>
      <td>1081.77</td>
    </tr>
    <tr>
      <th>2018-05-17</th>
      <td>186.99</td>
      <td>199.60</td>
      <td>1078.59</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Drop Nulls
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Symbol</th>
      <th>AAPL</th>
      <th>COST</th>
      <th>GOOG</th>
    </tr>
    <tr>
      <th>Trade DATE</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-05-14</th>
      <td>-0.002333</td>
      <td>0.000613</td>
      <td>0.001766</td>
    </tr>
    <tr>
      <th>2018-05-15</th>
      <td>-0.009088</td>
      <td>-0.002042</td>
      <td>-0.019060</td>
    </tr>
    <tr>
      <th>2018-05-16</th>
      <td>0.009333</td>
      <td>0.016523</td>
      <td>0.002354</td>
    </tr>
    <tr>
      <th>2018-05-17</th>
      <td>-0.006324</td>
      <td>0.004479</td>
      <td>-0.002940</td>
    </tr>
    <tr>
      <th>2018-05-18</th>
      <td>-0.003637</td>
      <td>-0.003206</td>
      <td>-0.011339</td>
    </tr>
  </tbody>
</table>
</div>



## Calculate the weighted returns for the portfolio assuming an equal number of shares for each stock


```python
# Calculate weighted portfolio returns
weights = [1/3, 1/3, 1/3]
# YOUR CODE HERE
```




    Trade DATE
    2018-05-14    0.000015
    2018-05-15   -0.010064
    2018-05-16    0.009403
    2018-05-17   -0.001595
    2018-05-18   -0.006061
    dtype: float64



## Join your portfolio returns to the DataFrame that contains all of the portfolio returns


```python
# Add your "Custom" portfolio to the larger dataframe of fund returns
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SOROS FUND MANAGEMENT LLC</th>
      <th>PAULSON &amp; CO.INC.</th>
      <th>TIGER GLOBAL MANAGEMENT LLC</th>
      <th>BERKSHIRE HATHAWAY INC</th>
      <th>Algo 1</th>
      <th>Algo 2</th>
      <th>S&amp;P 500</th>
      <th>Custom</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2019-04-16</th>
      <td>0.002699</td>
      <td>0.000388</td>
      <td>-0.000831</td>
      <td>0.000837</td>
      <td>-0.006945</td>
      <td>0.002899</td>
      <td>0.000509</td>
      <td>0.000340</td>
    </tr>
    <tr>
      <th>2019-04-17</th>
      <td>-0.002897</td>
      <td>-0.006467</td>
      <td>-0.004409</td>
      <td>0.003222</td>
      <td>-0.010301</td>
      <td>-0.005228</td>
      <td>-0.002274</td>
      <td>0.009292</td>
    </tr>
    <tr>
      <th>2019-04-18</th>
      <td>0.001448</td>
      <td>0.001222</td>
      <td>0.000582</td>
      <td>0.001916</td>
      <td>-0.000588</td>
      <td>-0.001229</td>
      <td>0.001579</td>
      <td>0.001545</td>
    </tr>
    <tr>
      <th>2019-04-22</th>
      <td>-0.002586</td>
      <td>-0.007333</td>
      <td>-0.003640</td>
      <td>-0.001088</td>
      <td>0.000677</td>
      <td>-0.001936</td>
      <td>0.001012</td>
      <td>0.001217</td>
    </tr>
    <tr>
      <th>2019-04-23</th>
      <td>0.007167</td>
      <td>0.003485</td>
      <td>0.006472</td>
      <td>0.013278</td>
      <td>0.004969</td>
      <td>0.009622</td>
      <td>0.008841</td>
      <td>0.011959</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Only compare dates where return data exists for all the stocks (drop NaNs)
# YOUR CODE HERE
```

## Re-run the performance and risk analysis with your portfolio to see how it compares to the others


```python
# Risk
# YOUR CODE HERE
```




    SOROS FUND MANAGEMENT LLC      0.146675
    PAULSON & CO.INC.              0.116732
    TIGER GLOBAL MANAGEMENT LLC    0.232531
    BERKSHIRE HATHAWAY INC         0.247155
    Algo 1                         0.133704
    Algo 2                         0.139556
    S&P 500                        0.152054
    Custom                         0.211496
    dtype: float64




```python
# Rolling
# YOUR CODE HERE
```




    <matplotlib.axes._subplots.AxesSubplot at 0x173bf457e80>




![png](output_61_1.png)



```python
# Annualized Sharpe Ratios
# YOUR CODE HERE
```




    SOROS FUND MANAGEMENT LLC      0.430713
    PAULSON & CO.INC.              0.258738
    TIGER GLOBAL MANAGEMENT LLC   -1.034216
    BERKSHIRE HATHAWAY INC         0.159756
    Algo 1                         2.035665
    Algo 2                         0.080607
    S&P 500                        0.584820
    Custom                         0.933123
    dtype: float64




```python
# Visualize the sharpe ratios as a bar plot
# YOUR CODE HERE
```




    <matplotlib.axes._subplots.AxesSubplot at 0x173bf7dfa58>




![png](output_63_1.png)



```python
# Create a correlation analysis
# YOUR CODE HERE
```




<style  type="text/css" >
    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col0 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col1 {
            background-color:  #acd666;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col2 {
            background-color:  #69b466;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col3 {
            background-color:  #badc66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col4 {
            background-color:  #40a066;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col5 {
            background-color:  #c8e366;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col6 {
            background-color:  #d3e966;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col7 {
            background-color:  #a3d166;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col0 {
            background-color:  #afd766;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col1 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col2 {
            background-color:  #6bb566;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col3 {
            background-color:  #7bbd66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col4 {
            background-color:  #47a366;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col5 {
            background-color:  #a8d366;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col6 {
            background-color:  #abd566;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col7 {
            background-color:  #84c266;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col0 {
            background-color:  #369a66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col1 {
            background-color:  #319866;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col2 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col3 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col4 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col5 {
            background-color:  #118866;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col6 {
            background-color:  #45a266;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col7 {
            background-color:  #2d9666;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col0 {
            background-color:  #b9dc66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col1 {
            background-color:  #74ba66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col2 {
            background-color:  #3c9e66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col3 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col4 {
            background-color:  #3d9e66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col5 {
            background-color:  #a8d366;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col6 {
            background-color:  #cae466;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col7 {
            background-color:  #bbdd66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col0 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col1 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col2 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col3 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col4 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col5 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col6 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col7 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col0 {
            background-color:  #cae466;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col1 {
            background-color:  #a9d466;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col2 {
            background-color:  #55aa66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col3 {
            background-color:  #add666;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col4 {
            background-color:  #48a366;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col5 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col6 {
            background-color:  #d3e966;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col7 {
            background-color:  #a5d266;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col0 {
            background-color:  #d0e866;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col1 {
            background-color:  #a2d066;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col2 {
            background-color:  #69b466;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col3 {
            background-color:  #c7e366;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col4 {
            background-color:  #329866;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col5 {
            background-color:  #cde666;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col6 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col7 {
            background-color:  #d3e966;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col0 {
            background-color:  #98cc66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col1 {
            background-color:  #71b866;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col2 {
            background-color:  #50a866;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col3 {
            background-color:  #b4da66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col4 {
            background-color:  #2a9466;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col5 {
            background-color:  #97cb66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col6 {
            background-color:  #d1e866;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col7 {
            background-color:  #ffff66;
            color:  #000000;
        }</style><table id="T_85543dfe_953f_11ea_9340_c0b6f9140de7" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >SOROS FUND MANAGEMENT LLC</th>        <th class="col_heading level0 col1" >PAULSON & CO.INC. </th>        <th class="col_heading level0 col2" >TIGER GLOBAL MANAGEMENT LLC</th>        <th class="col_heading level0 col3" >BERKSHIRE HATHAWAY INC</th>        <th class="col_heading level0 col4" >Algo 1</th>        <th class="col_heading level0 col5" >Algo 2</th>        <th class="col_heading level0 col6" >S&P 500</th>        <th class="col_heading level0 col7" >Custom</th>    </tr></thead><tbody>
                <tr>
                        <th id="T_85543dfe_953f_11ea_9340_c0b6f9140de7level0_row0" class="row_heading level0 row0" >SOROS FUND MANAGEMENT LLC</th>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col0" class="data row0 col0" >1</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col1" class="data row0 col1" >0.791962</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col2" class="data row0 col2" >0.478627</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col3" class="data row0 col3" >0.816675</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col4" class="data row0 col4" >0.337826</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col5" class="data row0 col5" >0.862846</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col6" class="data row0 col6" >0.876981</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col7" class="data row0 col7" >0.73325</td>
            </tr>
            <tr>
                        <th id="T_85543dfe_953f_11ea_9340_c0b6f9140de7level0_row1" class="row_heading level0 row1" >PAULSON & CO.INC. </th>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col0" class="data row1 col0" >0.791962</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col1" class="data row1 col1" >1</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col2" class="data row1 col2" >0.485375</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col3" class="data row1 col3" >0.650758</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col4" class="data row1 col4" >0.361301</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col5" class="data row1 col5" >0.783656</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col6" class="data row1 col6" >0.76668</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col7" class="data row1 col7" >0.64421</td>
            </tr>
            <tr>
                        <th id="T_85543dfe_953f_11ea_9340_c0b6f9140de7level0_row2" class="row_heading level0 row2" >TIGER GLOBAL MANAGEMENT LLC</th>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col0" class="data row2 col0" >0.478627</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col1" class="data row2 col1" >0.485375</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col2" class="data row2 col2" >1</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col3" class="data row2 col3" >0.325457</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col4" class="data row2 col4" >0.114554</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col5" class="data row2 col5" >0.409496</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col6" class="data row2 col6" >0.48103</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col7" class="data row2 col7" >0.391972</td>
            </tr>
            <tr>
                        <th id="T_85543dfe_953f_11ea_9340_c0b6f9140de7level0_row3" class="row_heading level0 row3" >BERKSHIRE HATHAWAY INC</th>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col0" class="data row3 col0" >0.816675</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col1" class="data row3 col1" >0.650758</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col2" class="data row3 col2" >0.325457</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col3" class="data row3 col3" >1</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col4" class="data row3 col4" >0.327</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col5" class="data row3 col5" >0.782804</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col6" class="data row3 col6" >0.852303</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col7" class="data row3 col7" >0.801158</td>
            </tr>
            <tr>
                        <th id="T_85543dfe_953f_11ea_9340_c0b6f9140de7level0_row4" class="row_heading level0 row4" >Algo 1</th>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col0" class="data row4 col0" >0.337826</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col1" class="data row4 col1" >0.361301</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col2" class="data row4 col2" >0.114554</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col3" class="data row4 col3" >0.327</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col4" class="data row4 col4" >1</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col5" class="data row4 col5" >0.365512</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col6" class="data row4 col6" >0.289358</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col7" class="data row4 col7" >0.261471</td>
            </tr>
            <tr>
                        <th id="T_85543dfe_953f_11ea_9340_c0b6f9140de7level0_row5" class="row_heading level0 row5" >Algo 2</th>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col0" class="data row5 col0" >0.862846</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col1" class="data row5 col1" >0.783656</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col2" class="data row5 col2" >0.409496</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col3" class="data row5 col3" >0.782804</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col4" class="data row5 col4" >0.365512</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col5" class="data row5 col5" >1</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col6" class="data row5 col6" >0.875721</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col7" class="data row5 col7" >0.739936</td>
            </tr>
            <tr>
                        <th id="T_85543dfe_953f_11ea_9340_c0b6f9140de7level0_row6" class="row_heading level0 row6" >S&P 500</th>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col0" class="data row6 col0" >0.876981</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col1" class="data row6 col1" >0.76668</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col2" class="data row6 col2" >0.48103</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col3" class="data row6 col3" >0.852303</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col4" class="data row6 col4" >0.289358</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col5" class="data row6 col5" >0.875721</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col6" class="data row6 col6" >1</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col7" class="data row6 col7" >0.871875</td>
            </tr>
            <tr>
                        <th id="T_85543dfe_953f_11ea_9340_c0b6f9140de7level0_row7" class="row_heading level0 row7" >Custom</th>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col0" class="data row7 col0" >0.73325</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col1" class="data row7 col1" >0.64421</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col2" class="data row7 col2" >0.391972</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col3" class="data row7 col3" >0.801158</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col4" class="data row7 col4" >0.261471</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col5" class="data row7 col5" >0.739936</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col6" class="data row7 col6" >0.871875</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col7" class="data row7 col7" >1</td>
            </tr>
    </tbody></table>




```python
# Beta
# YOUR CODE HERE
```




    <matplotlib.axes._subplots.AxesSubplot at 0x173bf76e828>




![png](output_65_1.png)


 #  A Whale off the Port(folio)

 In this assignment, you'll get to use what you've learned this week to evaluate the performance among various algorithmic, hedge, and mutual fund portfolios and compare them against the S&P 500.


```python
import pandas as pd
import os 
import numpy as np
import datetime as dt
from pathlib import Path
%matplotlib inline
```


```python
# Data Cleaning

In this section, you will need to read the CSV files into DataFrames and perform any necessary data cleaning steps. After cleaning, combine all DataFrames into a single DataFrame.

Files:
1. whale_returns.csv
2. algo_returns.csv
3. sp500_history.csv
```

## Whale Returns

Read the Whale Portfolio daily returns and clean the data


```python

```


```python
# Reading whale returns
whale_returns_csv = Path("Resources/whale_returns.csv")
whale_returns_dataframe= pd.read_csv(whale_returns_csv,)
whale_returns_dataframe.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>SOROS FUND MANAGEMENT LLC</th>
      <th>PAULSON &amp; CO.INC.</th>
      <th>TIGER GLOBAL MANAGEMENT LLC</th>
      <th>BERKSHIRE HATHAWAY INC</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2015-03-02</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015-03-03</td>
      <td>-0.001266</td>
      <td>-0.004981</td>
      <td>-0.000496</td>
      <td>-0.006569</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2015-03-04</td>
      <td>0.002230</td>
      <td>0.003241</td>
      <td>-0.002534</td>
      <td>0.004213</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2015-03-05</td>
      <td>0.004016</td>
      <td>0.004076</td>
      <td>0.002355</td>
      <td>0.006726</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2015-03-06</td>
      <td>-0.007905</td>
      <td>-0.003574</td>
      <td>-0.008481</td>
      <td>-0.013098</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Count nulls
whale_returns_dataframe.isnull().sum()
```




    Date                           0
    SOROS FUND MANAGEMENT LLC      1
    PAULSON & CO.INC.              1
    TIGER GLOBAL MANAGEMENT LLC    1
    BERKSHIRE HATHAWAY INC         1
    dtype: int64




```python
# Drop nulls
whale_returns_dataframe=whale_returns_dataframe.dropna().copy()
whale_returns_dataframe
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>SOROS FUND MANAGEMENT LLC</th>
      <th>PAULSON &amp; CO.INC.</th>
      <th>TIGER GLOBAL MANAGEMENT LLC</th>
      <th>BERKSHIRE HATHAWAY INC</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>2015-03-03</td>
      <td>-0.001266</td>
      <td>-0.004981</td>
      <td>-0.000496</td>
      <td>-0.006569</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2015-03-04</td>
      <td>0.002230</td>
      <td>0.003241</td>
      <td>-0.002534</td>
      <td>0.004213</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2015-03-05</td>
      <td>0.004016</td>
      <td>0.004076</td>
      <td>0.002355</td>
      <td>0.006726</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2015-03-06</td>
      <td>-0.007905</td>
      <td>-0.003574</td>
      <td>-0.008481</td>
      <td>-0.013098</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2015-03-09</td>
      <td>0.000582</td>
      <td>0.004225</td>
      <td>0.005843</td>
      <td>-0.001652</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1055</th>
      <td>2019-04-25</td>
      <td>-0.000285</td>
      <td>-0.001291</td>
      <td>-0.005153</td>
      <td>0.004848</td>
    </tr>
    <tr>
      <th>1056</th>
      <td>2019-04-26</td>
      <td>0.008149</td>
      <td>0.009162</td>
      <td>0.012355</td>
      <td>0.010434</td>
    </tr>
    <tr>
      <th>1057</th>
      <td>2019-04-29</td>
      <td>0.001254</td>
      <td>0.002719</td>
      <td>0.006251</td>
      <td>0.005223</td>
    </tr>
    <tr>
      <th>1058</th>
      <td>2019-04-30</td>
      <td>-0.001295</td>
      <td>-0.002211</td>
      <td>-0.000259</td>
      <td>-0.003702</td>
    </tr>
    <tr>
      <th>1059</th>
      <td>2019-05-01</td>
      <td>-0.005847</td>
      <td>-0.001341</td>
      <td>-0.007936</td>
      <td>-0.007833</td>
    </tr>
  </tbody>
</table>
<p>1059 rows × 5 columns</p>
</div>



## Algorithmic Daily Returns

Read the algorithmic daily returns and clean the data


```python
# Reading algorithmic returns
algo_returns_csv = Path("Resources/algo_returns.csv")
algo_returns_dataframe= pd.read_csv(algo_returns_csv,)
algo_returns_dataframe.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Algo 1</th>
      <th>Algo 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2014-05-28</td>
      <td>0.001745</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2014-05-29</td>
      <td>0.003978</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2014-05-30</td>
      <td>0.004464</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2014-06-02</td>
      <td>0.005692</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2014-06-03</td>
      <td>0.005292</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Count nulls
algo_returns_dataframe.isnull().sum()
```




    Date      0
    Algo 1    0
    Algo 2    6
    dtype: int64




```python
# Drop nulls
algo_returns_dataframe=algo_returns_dataframe.dropna().copy()
algo_returns_dataframe.head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Algo 1</th>
      <th>Algo 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>2014-06-05</td>
      <td>0.004062</td>
      <td>0.013285</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2014-06-06</td>
      <td>0.001857</td>
      <td>0.008284</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2014-06-09</td>
      <td>-0.005012</td>
      <td>0.005668</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2014-06-10</td>
      <td>0.004406</td>
      <td>-0.000735</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2014-06-11</td>
      <td>0.004760</td>
      <td>-0.003761</td>
    </tr>
  </tbody>
</table>
</div>



## S&P 500 Returns

Read the S&P500 Historic Closing Prices and create a new daily returns DataFrame from the data. 


```python
# Reading S&P 500 Closing Prices
sp500_history_csv = Path("Resources/sp500_history.csv")
sp500_history_csv_dataframe= pd.read_csv(sp500_history_csv,)
sp500_history_csv_dataframe.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Close</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>23-Apr-19</td>
      <td>$2933.68</td>
    </tr>
    <tr>
      <th>1</th>
      <td>22-Apr-19</td>
      <td>$2907.97</td>
    </tr>
    <tr>
      <th>2</th>
      <td>18-Apr-19</td>
      <td>$2905.03</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17-Apr-19</td>
      <td>$2900.45</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16-Apr-19</td>
      <td>$2907.06</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Check Data Types
sp500_history_csv_dataframe.dtypes
```




    Date     object
    Close    object
    dtype: object




```python
# Fix Data Types
# YOUR CODE HERE
```




    Close    float64
    dtype: object




```python
# Calculate Daily Returns
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Close</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2012-10-01</th>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2012-10-02</th>
      <td>0.000872</td>
    </tr>
    <tr>
      <th>2012-10-03</th>
      <td>0.003624</td>
    </tr>
    <tr>
      <th>2012-10-04</th>
      <td>0.007174</td>
    </tr>
    <tr>
      <th>2012-10-05</th>
      <td>-0.000322</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Drop nulls
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Close</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2012-10-02</th>
      <td>0.000872</td>
    </tr>
    <tr>
      <th>2012-10-03</th>
      <td>0.003624</td>
    </tr>
    <tr>
      <th>2012-10-04</th>
      <td>0.007174</td>
    </tr>
    <tr>
      <th>2012-10-05</th>
      <td>-0.000322</td>
    </tr>
    <tr>
      <th>2012-10-08</th>
      <td>-0.003457</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Rename Column
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>S&amp;P 500</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2012-10-02</th>
      <td>0.000872</td>
    </tr>
    <tr>
      <th>2012-10-03</th>
      <td>0.003624</td>
    </tr>
    <tr>
      <th>2012-10-04</th>
      <td>0.007174</td>
    </tr>
    <tr>
      <th>2012-10-05</th>
      <td>-0.000322</td>
    </tr>
    <tr>
      <th>2012-10-08</th>
      <td>-0.003457</td>
    </tr>
  </tbody>
</table>
</div>



## Combine Whale, Algorithmic, and S&P 500 Returns


```python
# Concatenate all DataFrames into a single DataFrame
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SOROS FUND MANAGEMENT LLC</th>
      <th>PAULSON &amp; CO.INC.</th>
      <th>TIGER GLOBAL MANAGEMENT LLC</th>
      <th>BERKSHIRE HATHAWAY INC</th>
      <th>Algo 1</th>
      <th>Algo 2</th>
      <th>S&amp;P 500</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2015-03-03</th>
      <td>-0.001266</td>
      <td>-0.004981</td>
      <td>-0.000496</td>
      <td>-0.006569</td>
      <td>-0.001942</td>
      <td>-0.000949</td>
      <td>-0.004539</td>
    </tr>
    <tr>
      <th>2015-03-04</th>
      <td>0.002230</td>
      <td>0.003241</td>
      <td>-0.002534</td>
      <td>0.004213</td>
      <td>-0.008589</td>
      <td>0.002416</td>
      <td>-0.004389</td>
    </tr>
    <tr>
      <th>2015-03-05</th>
      <td>0.004016</td>
      <td>0.004076</td>
      <td>0.002355</td>
      <td>0.006726</td>
      <td>-0.000955</td>
      <td>0.004323</td>
      <td>0.001196</td>
    </tr>
    <tr>
      <th>2015-03-06</th>
      <td>-0.007905</td>
      <td>-0.003574</td>
      <td>-0.008481</td>
      <td>-0.013098</td>
      <td>-0.004957</td>
      <td>-0.011460</td>
      <td>-0.014174</td>
    </tr>
    <tr>
      <th>2015-03-09</th>
      <td>0.000582</td>
      <td>0.004225</td>
      <td>0.005843</td>
      <td>-0.001652</td>
      <td>-0.005447</td>
      <td>0.001303</td>
      <td>0.003944</td>
    </tr>
  </tbody>
</table>
</div>



---

# Portfolio Analysis

In this section, you will calculate and visualize performance and risk metrics for the portfolios.

## Performance

Calculate and Plot the daily returns and cumulative returns. Does any portfolio outperform the S&P 500? 


```python
# Plot daily returns
# YOUR CODE HERE
```




    <matplotlib.axes._subplots.AxesSubplot at 0x173bc74f2b0>




![png](output_90_1.png)



```python
# Plot cumulative returns
# YOUR CODE HERE
```




    <matplotlib.axes._subplots.AxesSubplot at 0x173bccca780>




![png](output_91_1.png)


## Risk

Determine the _risk_ of each portfolio:

1. Create a box plot for each portfolio. 
2. Calculate the standard deviation for all portfolios
4. Determine which portfolios are riskier than the S&P 500
5. Calculate the Annualized Standard Deviation


```python
# Box plot to visually show risk
# YOUR CODE HERE
```




    <matplotlib.axes._subplots.AxesSubplot at 0x173bcfc0d30>




![png](output_93_1.png)



```python
# Daily Standard Deviations
# Calculate the standard deviation for each portfolio. 
# Which portfolios are riskier than the S&P 500?
# YOUR CODE HERE
```




    SOROS FUND MANAGEMENT LLC      0.007895
    PAULSON & CO.INC.              0.007023
    TIGER GLOBAL MANAGEMENT LLC    0.010894
    BERKSHIRE HATHAWAY INC         0.012919
    Algo 1                         0.007620
    Algo 2                         0.008342
    S&P 500                        0.008554
    dtype: float64




```python
# Determine which portfolios are riskier than the S&P 500
# YOUR CODE HERE
```




    SOROS FUND MANAGEMENT LLC      False
    PAULSON & CO.INC.              False
    TIGER GLOBAL MANAGEMENT LLC     True
    BERKSHIRE HATHAWAY INC          True
    Algo 1                         False
    Algo 2                         False
    S&P 500                        False
    dtype: bool




```python
# Calculate the annualized standard deviation (252 trading days)
# YOUR CODE HERE
```




    SOROS FUND MANAGEMENT LLC      0.125335
    PAULSON & CO.INC.              0.111488
    TIGER GLOBAL MANAGEMENT LLC    0.172936
    BERKSHIRE HATHAWAY INC         0.205077
    Algo 1                         0.120967
    Algo 2                         0.132430
    S&P 500                        0.135786
    dtype: float64



---

## Rolling Statistics

Risk changes over time. Analyze the rolling statistics for Risk and Beta. 

1. Plot the rolling standard deviation of the various portfolios along with the rolling standard deviation of the S&P 500 (consider a 21 day window). Does the risk increase for each of the portfolios at the same time risk increases in the S&P?
2. Construct a correlation table for the algorithmic, whale, and S&P 500 returns. Which returns most closely mimic the S&P?
3. Choose one portfolio and plot a rolling beta between that portfolio's returns and S&P 500 returns. Does the portfolio seem sensitive to movements in the S&P 500?
4. An alternative way to calculate a rolling window is to take the exponentially weighted moving average. This is like a moving window average, but it assigns greater importance to more recent observations. Try calculating the ewm with a 21 day half-life.


```python
# Calculate and plot the rolling standard deviation for
# the S&P 500 and whale portfolios using a 21 trading day window
# YOUR CODE HERE
```




    <matplotlib.axes._subplots.AxesSubplot at 0x173bd31e438>




![png](output_99_1.png)



```python
# Construct a correlation table
# YOUR CODE HERE
```




<style  type="text/css" >
    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col0 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col1 {
            background-color:  #96cb66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col2 {
            background-color:  #79bc66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col3 {
            background-color:  #a7d366;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col4 {
            background-color:  #309866;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col5 {
            background-color:  #c1e066;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col6 {
            background-color:  #c6e266;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col0 {
            background-color:  #8ec666;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col1 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col2 {
            background-color:  #52a866;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col3 {
            background-color:  #5bad66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col4 {
            background-color:  #209066;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col5 {
            background-color:  #8cc666;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col6 {
            background-color:  #8ac466;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col0 {
            background-color:  #5aac66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col1 {
            background-color:  #399c66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col2 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col3 {
            background-color:  #2f9766;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col4 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col5 {
            background-color:  #4ea666;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col6 {
            background-color:  #7abc66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col0 {
            background-color:  #a3d166;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col1 {
            background-color:  #60b066;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col2 {
            background-color:  #4fa766;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col3 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col4 {
            background-color:  #279366;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col5 {
            background-color:  #8fc766;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col6 {
            background-color:  #a7d366;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col0 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col1 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col2 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col3 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col4 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col5 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col6 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col0 {
            background-color:  #bede66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col1 {
            background-color:  #8fc766;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col2 {
            background-color:  #69b466;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col3 {
            background-color:  #8fc766;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col4 {
            background-color:  #259266;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col5 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col6 {
            background-color:  #cde666;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col0 {
            background-color:  #c2e066;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col1 {
            background-color:  #8cc666;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col2 {
            background-color:  #8cc666;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col3 {
            background-color:  #a6d266;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col4 {
            background-color:  #239166;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col5 {
            background-color:  #cde666;
            color:  #000000;
        }    #T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col6 {
            background-color:  #ffff66;
            color:  #000000;
        }</style><table id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >SOROS FUND MANAGEMENT LLC</th>        <th class="col_heading level0 col1" >PAULSON & CO.INC. </th>        <th class="col_heading level0 col2" >TIGER GLOBAL MANAGEMENT LLC</th>        <th class="col_heading level0 col3" >BERKSHIRE HATHAWAY INC</th>        <th class="col_heading level0 col4" >Algo 1</th>        <th class="col_heading level0 col5" >Algo 2</th>        <th class="col_heading level0 col6" >S&P 500</th>    </tr></thead><tbody>
                <tr>
                        <th id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7level0_row0" class="row_heading level0 row0" >SOROS FUND MANAGEMENT LLC</th>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col0" class="data row0 col0" >1</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col1" class="data row0 col1" >0.699914</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col2" class="data row0 col2" >0.561243</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col3" class="data row0 col3" >0.75436</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col4" class="data row0 col4" >0.321211</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col5" class="data row0 col5" >0.826873</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row0_col6" class="data row0 col6" >0.837864</td>
            </tr>
            <tr>
                        <th id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7level0_row1" class="row_heading level0 row1" >PAULSON & CO.INC. </th>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col0" class="data row1 col0" >0.699914</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col1" class="data row1 col1" >1</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col2" class="data row1 col2" >0.434479</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col3" class="data row1 col3" >0.545623</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col4" class="data row1 col4" >0.26884</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col5" class="data row1 col5" >0.678152</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row1_col6" class="data row1 col6" >0.669732</td>
            </tr>
            <tr>
                        <th id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7level0_row2" class="row_heading level0 row2" >TIGER GLOBAL MANAGEMENT LLC</th>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col0" class="data row2 col0" >0.561243</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col1" class="data row2 col1" >0.434479</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col2" class="data row2 col2" >1</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col3" class="data row2 col3" >0.424423</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col4" class="data row2 col4" >0.164387</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col5" class="data row2 col5" >0.507414</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row2_col6" class="data row2 col6" >0.623946</td>
            </tr>
            <tr>
                        <th id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7level0_row3" class="row_heading level0 row3" >BERKSHIRE HATHAWAY INC</th>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col0" class="data row3 col0" >0.75436</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col1" class="data row3 col1" >0.545623</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col2" class="data row3 col2" >0.424423</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col3" class="data row3 col3" >1</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col4" class="data row3 col4" >0.292033</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col5" class="data row3 col5" >0.688082</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row3_col6" class="data row3 col6" >0.751371</td>
            </tr>
            <tr>
                        <th id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7level0_row4" class="row_heading level0 row4" >Algo 1</th>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col0" class="data row4 col0" >0.321211</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col1" class="data row4 col1" >0.26884</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col2" class="data row4 col2" >0.164387</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col3" class="data row4 col3" >0.292033</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col4" class="data row4 col4" >1</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col5" class="data row4 col5" >0.288243</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row4_col6" class="data row4 col6" >0.279494</td>
            </tr>
            <tr>
                        <th id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7level0_row5" class="row_heading level0 row5" >Algo 2</th>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col0" class="data row5 col0" >0.826873</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col1" class="data row5 col1" >0.678152</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col2" class="data row5 col2" >0.507414</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col3" class="data row5 col3" >0.688082</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col4" class="data row5 col4" >0.288243</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col5" class="data row5 col5" >1</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row5_col6" class="data row5 col6" >0.858764</td>
            </tr>
            <tr>
                        <th id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7level0_row6" class="row_heading level0 row6" >S&P 500</th>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col0" class="data row6 col0" >0.837864</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col1" class="data row6 col1" >0.669732</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col2" class="data row6 col2" >0.623946</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col3" class="data row6 col3" >0.751371</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col4" class="data row6 col4" >0.279494</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col5" class="data row6 col5" >0.858764</td>
                        <td id="T_83668ff6_953f_11ea_8db6_c0b6f9140de7row6_col6" class="data row6 col6" >1</td>
            </tr>
    </tbody></table>




```python
# Calculate Beta for a single portfolio compared to the total market (S&P 500)
# (Your graph may differ, dependent upon which portfolio you are comparing)
# YOUR CODE HERE
```




    <matplotlib.axes._subplots.AxesSubplot at 0x173bed736a0>




![png](output_101_1.png)



```python
# Calculate a rolling window using the exponentially weighted moving average. 
# YOUR CODE HERE
```




    <matplotlib.axes._subplots.AxesSubplot at 0x173bf094240>




![png](output_102_1.png)


---

## Sharpe Ratios
In reality, investment managers and thier institutional investors look at the ratio of return-to-risk, and not just returns alone. (After all, if you could invest in one of two portfolios, each offered the same 10% return, yet one offered lower risk, you'd take that one, right?)

1. Using the daily returns, calculate and visualize the Sharpe ratios using a bar plot.
2. Determine whether the algorithmic strategies outperform both the market (S&P 500) and the whales portfolios.


```python
# Calculate annualized Sharpe Ratios
# YOUR CODE HERE
```




    SOROS FUND MANAGEMENT LLC      0.356417
    PAULSON & CO.INC.             -0.483570
    TIGER GLOBAL MANAGEMENT LLC   -0.121060
    BERKSHIRE HATHAWAY INC         0.621810
    Algo 1                         1.378648
    Algo 2                         0.501364
    S&P 500                        0.648267
    dtype: float64




```python
# Visualize the sharpe ratios as a bar plot
# YOUR CODE HERE
```




    <matplotlib.axes._subplots.AxesSubplot at 0x173bd954e10>




![png](output_106_1.png)


On the basis of this performance metric, do our algo strategies outperform both 'the market' and the whales? Type your answer here:

---

# Portfolio Returns

In this section, you will build your own portfolio of stocks, calculate the returns, and compare the results to the Whale Portfolios and the S&P 500. 

1. Visit [Google Sheets](https://docs.google.com/spreadsheets/) and use the in-built Google Finance function to choose 3-5 stocks for your own portfolio.
2. Download the data as CSV files and calculate the portfolio returns.
3. Calculate the returns for each stock.
4. Using those returns, calculate the weighted returns for your entire portfolio assuming an equal number of shares for each stock.
5. Add your portfolio returns to the DataFrame with the other portfolios and rerun the analysis. How does your portfolio fair?


## Your analysis should include the following:

- Using all portfolios:
 - The annualized standard deviation (252 trading days) for all portfolios.
 - The plotted rolling standard deviation using a 21 trading day window for all portfolios.
 - The calculated annualized Sharpe Ratios and the accompanying bar plot visualization.
 - A correlation table.
- Using your custom portfolio and one other of your choosing:
 - The plotted beta. 

## Choose 3-5 custom stocks with at last 1 year's worth of historic prices and create a DataFrame of the closing prices and dates for each stock.


```python
# Read the first stock
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Symbol</th>
      <th>NOCP</th>
    </tr>
    <tr>
      <th>Trade DATE</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-05-11</th>
      <td>GOOG</td>
      <td>1098.26</td>
    </tr>
    <tr>
      <th>2018-05-14</th>
      <td>GOOG</td>
      <td>1100.20</td>
    </tr>
    <tr>
      <th>2018-05-15</th>
      <td>GOOG</td>
      <td>1079.23</td>
    </tr>
    <tr>
      <th>2018-05-16</th>
      <td>GOOG</td>
      <td>1081.77</td>
    </tr>
    <tr>
      <th>2018-05-17</th>
      <td>GOOG</td>
      <td>1078.59</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Read the second stock
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Symbol</th>
      <th>NOCP</th>
    </tr>
    <tr>
      <th>Trade DATE</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-05-11</th>
      <td>AAPL</td>
      <td>188.59</td>
    </tr>
    <tr>
      <th>2018-05-14</th>
      <td>AAPL</td>
      <td>188.15</td>
    </tr>
    <tr>
      <th>2018-05-15</th>
      <td>AAPL</td>
      <td>186.44</td>
    </tr>
    <tr>
      <th>2018-05-16</th>
      <td>AAPL</td>
      <td>188.18</td>
    </tr>
    <tr>
      <th>2018-05-17</th>
      <td>AAPL</td>
      <td>186.99</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Read the third stock
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Symbol</th>
      <th>NOCP</th>
    </tr>
    <tr>
      <th>Trade DATE</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-05-11</th>
      <td>COST</td>
      <td>195.76</td>
    </tr>
    <tr>
      <th>2018-05-14</th>
      <td>COST</td>
      <td>195.88</td>
    </tr>
    <tr>
      <th>2018-05-15</th>
      <td>COST</td>
      <td>195.48</td>
    </tr>
    <tr>
      <th>2018-05-16</th>
      <td>COST</td>
      <td>198.71</td>
    </tr>
    <tr>
      <th>2018-05-17</th>
      <td>COST</td>
      <td>199.60</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Concatenate all stocks into a single DataFrame
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Symbol</th>
      <th>NOCP</th>
    </tr>
    <tr>
      <th>Trade DATE</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-05-11</th>
      <td>GOOG</td>
      <td>1098.26</td>
    </tr>
    <tr>
      <th>2018-05-14</th>
      <td>GOOG</td>
      <td>1100.20</td>
    </tr>
    <tr>
      <th>2018-05-15</th>
      <td>GOOG</td>
      <td>1079.23</td>
    </tr>
    <tr>
      <th>2018-05-16</th>
      <td>GOOG</td>
      <td>1081.77</td>
    </tr>
    <tr>
      <th>2018-05-17</th>
      <td>GOOG</td>
      <td>1078.59</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Reset the index
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Trade DATE</th>
      <th>Symbol</th>
      <th>NOCP</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2018-05-11</td>
      <td>GOOG</td>
      <td>1098.26</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2018-05-14</td>
      <td>GOOG</td>
      <td>1100.20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018-05-15</td>
      <td>GOOG</td>
      <td>1079.23</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018-05-16</td>
      <td>GOOG</td>
      <td>1081.77</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2018-05-17</td>
      <td>GOOG</td>
      <td>1078.59</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Pivot so that each column of prices represents a unique symbol
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Symbol</th>
      <th>AAPL</th>
      <th>COST</th>
      <th>GOOG</th>
    </tr>
    <tr>
      <th>Trade DATE</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-05-11</th>
      <td>188.59</td>
      <td>195.76</td>
      <td>1098.26</td>
    </tr>
    <tr>
      <th>2018-05-14</th>
      <td>188.15</td>
      <td>195.88</td>
      <td>1100.20</td>
    </tr>
    <tr>
      <th>2018-05-15</th>
      <td>186.44</td>
      <td>195.48</td>
      <td>1079.23</td>
    </tr>
    <tr>
      <th>2018-05-16</th>
      <td>188.18</td>
      <td>198.71</td>
      <td>1081.77</td>
    </tr>
    <tr>
      <th>2018-05-17</th>
      <td>186.99</td>
      <td>199.60</td>
      <td>1078.59</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Drop Nulls
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Symbol</th>
      <th>AAPL</th>
      <th>COST</th>
      <th>GOOG</th>
    </tr>
    <tr>
      <th>Trade DATE</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-05-14</th>
      <td>-0.002333</td>
      <td>0.000613</td>
      <td>0.001766</td>
    </tr>
    <tr>
      <th>2018-05-15</th>
      <td>-0.009088</td>
      <td>-0.002042</td>
      <td>-0.019060</td>
    </tr>
    <tr>
      <th>2018-05-16</th>
      <td>0.009333</td>
      <td>0.016523</td>
      <td>0.002354</td>
    </tr>
    <tr>
      <th>2018-05-17</th>
      <td>-0.006324</td>
      <td>0.004479</td>
      <td>-0.002940</td>
    </tr>
    <tr>
      <th>2018-05-18</th>
      <td>-0.003637</td>
      <td>-0.003206</td>
      <td>-0.011339</td>
    </tr>
  </tbody>
</table>
</div>



## Calculate the weighted returns for the portfolio assuming an equal number of shares for each stock


```python
# Calculate weighted portfolio returns
weights = [1/3, 1/3, 1/3]
# YOUR CODE HERE
```




    Trade DATE
    2018-05-14    0.000015
    2018-05-15   -0.010064
    2018-05-16    0.009403
    2018-05-17   -0.001595
    2018-05-18   -0.006061
    dtype: float64



## Join your portfolio returns to the DataFrame that contains all of the portfolio returns


```python
# Add your "Custom" portfolio to the larger dataframe of fund returns
# YOUR CODE HERE
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>SOROS FUND MANAGEMENT LLC</th>
      <th>PAULSON &amp; CO.INC.</th>
      <th>TIGER GLOBAL MANAGEMENT LLC</th>
      <th>BERKSHIRE HATHAWAY INC</th>
      <th>Algo 1</th>
      <th>Algo 2</th>
      <th>S&amp;P 500</th>
      <th>Custom</th>
    </tr>
    <tr>
      <th>Date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2019-04-16</th>
      <td>0.002699</td>
      <td>0.000388</td>
      <td>-0.000831</td>
      <td>0.000837</td>
      <td>-0.006945</td>
      <td>0.002899</td>
      <td>0.000509</td>
      <td>0.000340</td>
    </tr>
    <tr>
      <th>2019-04-17</th>
      <td>-0.002897</td>
      <td>-0.006467</td>
      <td>-0.004409</td>
      <td>0.003222</td>
      <td>-0.010301</td>
      <td>-0.005228</td>
      <td>-0.002274</td>
      <td>0.009292</td>
    </tr>
    <tr>
      <th>2019-04-18</th>
      <td>0.001448</td>
      <td>0.001222</td>
      <td>0.000582</td>
      <td>0.001916</td>
      <td>-0.000588</td>
      <td>-0.001229</td>
      <td>0.001579</td>
      <td>0.001545</td>
    </tr>
    <tr>
      <th>2019-04-22</th>
      <td>-0.002586</td>
      <td>-0.007333</td>
      <td>-0.003640</td>
      <td>-0.001088</td>
      <td>0.000677</td>
      <td>-0.001936</td>
      <td>0.001012</td>
      <td>0.001217</td>
    </tr>
    <tr>
      <th>2019-04-23</th>
      <td>0.007167</td>
      <td>0.003485</td>
      <td>0.006472</td>
      <td>0.013278</td>
      <td>0.004969</td>
      <td>0.009622</td>
      <td>0.008841</td>
      <td>0.011959</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Only compare dates where return data exists for all the stocks (drop NaNs)
# YOUR CODE HERE
```

## Re-run the performance and risk analysis with your portfolio to see how it compares to the others


```python
# Risk
# YOUR CODE HERE
```




    SOROS FUND MANAGEMENT LLC      0.146675
    PAULSON & CO.INC.              0.116732
    TIGER GLOBAL MANAGEMENT LLC    0.232531
    BERKSHIRE HATHAWAY INC         0.247155
    Algo 1                         0.133704
    Algo 2                         0.139556
    S&P 500                        0.152054
    Custom                         0.211496
    dtype: float64




```python
# Rolling
# YOUR CODE HERE
```




    <matplotlib.axes._subplots.AxesSubplot at 0x173bf457e80>




![png](output_125_1.png)



```python
# Annualized Sharpe Ratios
# YOUR CODE HERE
```




    SOROS FUND MANAGEMENT LLC      0.430713
    PAULSON & CO.INC.              0.258738
    TIGER GLOBAL MANAGEMENT LLC   -1.034216
    BERKSHIRE HATHAWAY INC         0.159756
    Algo 1                         2.035665
    Algo 2                         0.080607
    S&P 500                        0.584820
    Custom                         0.933123
    dtype: float64




```python
# Visualize the sharpe ratios as a bar plot
# YOUR CODE HERE
```




    <matplotlib.axes._subplots.AxesSubplot at 0x173bf7dfa58>




![png](output_127_1.png)



```python
# Create a correlation analysis
# YOUR CODE HERE
```




<style  type="text/css" >
    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col0 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col1 {
            background-color:  #acd666;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col2 {
            background-color:  #69b466;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col3 {
            background-color:  #badc66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col4 {
            background-color:  #40a066;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col5 {
            background-color:  #c8e366;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col6 {
            background-color:  #d3e966;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col7 {
            background-color:  #a3d166;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col0 {
            background-color:  #afd766;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col1 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col2 {
            background-color:  #6bb566;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col3 {
            background-color:  #7bbd66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col4 {
            background-color:  #47a366;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col5 {
            background-color:  #a8d366;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col6 {
            background-color:  #abd566;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col7 {
            background-color:  #84c266;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col0 {
            background-color:  #369a66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col1 {
            background-color:  #319866;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col2 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col3 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col4 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col5 {
            background-color:  #118866;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col6 {
            background-color:  #45a266;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col7 {
            background-color:  #2d9666;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col0 {
            background-color:  #b9dc66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col1 {
            background-color:  #74ba66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col2 {
            background-color:  #3c9e66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col3 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col4 {
            background-color:  #3d9e66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col5 {
            background-color:  #a8d366;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col6 {
            background-color:  #cae466;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col7 {
            background-color:  #bbdd66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col0 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col1 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col2 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col3 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col4 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col5 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col6 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col7 {
            background-color:  #008066;
            color:  #f1f1f1;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col0 {
            background-color:  #cae466;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col1 {
            background-color:  #a9d466;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col2 {
            background-color:  #55aa66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col3 {
            background-color:  #add666;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col4 {
            background-color:  #48a366;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col5 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col6 {
            background-color:  #d3e966;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col7 {
            background-color:  #a5d266;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col0 {
            background-color:  #d0e866;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col1 {
            background-color:  #a2d066;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col2 {
            background-color:  #69b466;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col3 {
            background-color:  #c7e366;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col4 {
            background-color:  #329866;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col5 {
            background-color:  #cde666;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col6 {
            background-color:  #ffff66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col7 {
            background-color:  #d3e966;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col0 {
            background-color:  #98cc66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col1 {
            background-color:  #71b866;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col2 {
            background-color:  #50a866;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col3 {
            background-color:  #b4da66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col4 {
            background-color:  #2a9466;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col5 {
            background-color:  #97cb66;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col6 {
            background-color:  #d1e866;
            color:  #000000;
        }    #T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col7 {
            background-color:  #ffff66;
            color:  #000000;
        }</style><table id="T_85543dfe_953f_11ea_9340_c0b6f9140de7" ><thead>    <tr>        <th class="blank level0" ></th>        <th class="col_heading level0 col0" >SOROS FUND MANAGEMENT LLC</th>        <th class="col_heading level0 col1" >PAULSON & CO.INC. </th>        <th class="col_heading level0 col2" >TIGER GLOBAL MANAGEMENT LLC</th>        <th class="col_heading level0 col3" >BERKSHIRE HATHAWAY INC</th>        <th class="col_heading level0 col4" >Algo 1</th>        <th class="col_heading level0 col5" >Algo 2</th>        <th class="col_heading level0 col6" >S&P 500</th>        <th class="col_heading level0 col7" >Custom</th>    </tr></thead><tbody>
                <tr>
                        <th id="T_85543dfe_953f_11ea_9340_c0b6f9140de7level0_row0" class="row_heading level0 row0" >SOROS FUND MANAGEMENT LLC</th>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col0" class="data row0 col0" >1</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col1" class="data row0 col1" >0.791962</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col2" class="data row0 col2" >0.478627</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col3" class="data row0 col3" >0.816675</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col4" class="data row0 col4" >0.337826</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col5" class="data row0 col5" >0.862846</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col6" class="data row0 col6" >0.876981</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row0_col7" class="data row0 col7" >0.73325</td>
            </tr>
            <tr>
                        <th id="T_85543dfe_953f_11ea_9340_c0b6f9140de7level0_row1" class="row_heading level0 row1" >PAULSON & CO.INC. </th>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col0" class="data row1 col0" >0.791962</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col1" class="data row1 col1" >1</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col2" class="data row1 col2" >0.485375</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col3" class="data row1 col3" >0.650758</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col4" class="data row1 col4" >0.361301</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col5" class="data row1 col5" >0.783656</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col6" class="data row1 col6" >0.76668</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row1_col7" class="data row1 col7" >0.64421</td>
            </tr>
            <tr>
                        <th id="T_85543dfe_953f_11ea_9340_c0b6f9140de7level0_row2" class="row_heading level0 row2" >TIGER GLOBAL MANAGEMENT LLC</th>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col0" class="data row2 col0" >0.478627</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col1" class="data row2 col1" >0.485375</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col2" class="data row2 col2" >1</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col3" class="data row2 col3" >0.325457</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col4" class="data row2 col4" >0.114554</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col5" class="data row2 col5" >0.409496</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col6" class="data row2 col6" >0.48103</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row2_col7" class="data row2 col7" >0.391972</td>
            </tr>
            <tr>
                        <th id="T_85543dfe_953f_11ea_9340_c0b6f9140de7level0_row3" class="row_heading level0 row3" >BERKSHIRE HATHAWAY INC</th>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col0" class="data row3 col0" >0.816675</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col1" class="data row3 col1" >0.650758</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col2" class="data row3 col2" >0.325457</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col3" class="data row3 col3" >1</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col4" class="data row3 col4" >0.327</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col5" class="data row3 col5" >0.782804</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col6" class="data row3 col6" >0.852303</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row3_col7" class="data row3 col7" >0.801158</td>
            </tr>
            <tr>
                        <th id="T_85543dfe_953f_11ea_9340_c0b6f9140de7level0_row4" class="row_heading level0 row4" >Algo 1</th>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col0" class="data row4 col0" >0.337826</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col1" class="data row4 col1" >0.361301</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col2" class="data row4 col2" >0.114554</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col3" class="data row4 col3" >0.327</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col4" class="data row4 col4" >1</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col5" class="data row4 col5" >0.365512</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col6" class="data row4 col6" >0.289358</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row4_col7" class="data row4 col7" >0.261471</td>
            </tr>
            <tr>
                        <th id="T_85543dfe_953f_11ea_9340_c0b6f9140de7level0_row5" class="row_heading level0 row5" >Algo 2</th>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col0" class="data row5 col0" >0.862846</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col1" class="data row5 col1" >0.783656</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col2" class="data row5 col2" >0.409496</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col3" class="data row5 col3" >0.782804</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col4" class="data row5 col4" >0.365512</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col5" class="data row5 col5" >1</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col6" class="data row5 col6" >0.875721</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row5_col7" class="data row5 col7" >0.739936</td>
            </tr>
            <tr>
                        <th id="T_85543dfe_953f_11ea_9340_c0b6f9140de7level0_row6" class="row_heading level0 row6" >S&P 500</th>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col0" class="data row6 col0" >0.876981</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col1" class="data row6 col1" >0.76668</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col2" class="data row6 col2" >0.48103</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col3" class="data row6 col3" >0.852303</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col4" class="data row6 col4" >0.289358</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col5" class="data row6 col5" >0.875721</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col6" class="data row6 col6" >1</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row6_col7" class="data row6 col7" >0.871875</td>
            </tr>
            <tr>
                        <th id="T_85543dfe_953f_11ea_9340_c0b6f9140de7level0_row7" class="row_heading level0 row7" >Custom</th>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col0" class="data row7 col0" >0.73325</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col1" class="data row7 col1" >0.64421</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col2" class="data row7 col2" >0.391972</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col3" class="data row7 col3" >0.801158</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col4" class="data row7 col4" >0.261471</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col5" class="data row7 col5" >0.739936</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col6" class="data row7 col6" >0.871875</td>
                        <td id="T_85543dfe_953f_11ea_9340_c0b6f9140de7row7_col7" class="data row7 col7" >1</td>
            </tr>
    </tbody></table>




```python
# Beta
# YOUR CODE HERE
```




    <matplotlib.axes._subplots.AxesSubplot at 0x173bf76e828>




![png](output_129_1.png)

