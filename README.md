# MIE1622_Assignment_1
 
I used Jupyter Notebook to implement the CPLEX Solver. The purpose of this assignment is to compare computational investment strategies based on minimizing portfolio variance and maximizing Sharpe's ratio. This also takes into account the effect of trading costs.

We will be testing 4 different strategies with the following scenario:

- Only trading stocks - 20 different ones
- There are 12 holding periods, each holding period is two months
- Translation cost is estimated to be 0.5% of the traded volume
- Using the daily returns to estimate the mean and covariance
- Cannot use future prices when making decisions
- Track the value of each portfolio at each holding period
- The value of the initial portfolio is 1 million.
- Cash account must be non-negative at all times
- Each share must be in integers
- The rest of the leftover money is set aside in a cash account

**Portfolio Strategies**

1. Buy and Hold
2. Equally Weighted (1/n)
3. Minimum Variance
4. Maximum Sharpe's Ratio

**Code**:

First, we had to import the required libraries such as CPLEX solver.

We have created a function that will decide whether we round up or down the stocks to buy based on whether there was enough money to buy up.

**Strategy 1:** Keep and hold the initial portfolio of 'HOG' and 'VZ'
The weights of the stocks remain the same, the cash account remains the same, weights of each stock change and fluctuate based on the value of the new stocks

**Strategy 2: Equally weighted**

Put an equal amount of money into each of the 20 stocks, we need to solve the rounding issue of which ones to round up or down, if you round down all of them, there may be too much money in the cash account not being invested, on the flip side, round up means we won't have enough money. 

x_share = p_current/N * x_ratio

# Calculate cash account
cash_optimal = cash_init + V_sell - V_buy - TC

# Calculate transaction cost
x_change = np.abs(x_init - x_optimal) # Number of units changed
TC = 0.005 * np.dot(cur_prices, x_change)

Buy 1 less stock of all stocks above 1, This would essentially round all share units down 1 so you would have enough money, Rounded-up stocks will go down two units 

Then we buy one stock at a time to use up the cash inside the cash account

**Strategy 3: Minimum Variance**

To use the cplex solver, there must be objectives (min variance) and constraints (all weights sum up to 1) in place. The cplex will also not be short (no negative weights) and will return the optimal weights. 

**Strategy 4: Maximum Sharpe's Ratio**

SHarpe's ratio is the expected return/unit of risk. We can use cplex to solve for the optimal weights of stocks. 

We calculate the covariance and mean returns of each stock. We set the risk-free rate, and calculate the number of holding periods. 

**Results**

Period 1: start date 01/02/2020, end date 02/28/2020
  Strategy "Buy and Hold", value begin = $ 1000012.93, value end = $ 893956.75
  Strategy "Equally Weighted Portfolio", value begin = $ 990881.80, value end = $ 892363.31
  Strategy "Minimum Variance Portfolio", value begin = $ 992756.25, value end = $ 915852.04
  Strategy "Maximum Sharpe Ratio Portfolio", value begin = $ 990063.24, value end = $ 922013.36

Period 2: start date 03/02/2020, end date 04/30/2020
  Strategy "Buy and Hold", value begin = $ 945076.08, value end = $ 949228.39
  Strategy "Equally Weighted Portfolio", value begin = $ 930689.62, value end = $ 862184.18
  Strategy "Minimum Variance Portfolio", value begin = $ 955715.61, value end = $ 850657.72
  Strategy "Maximum Sharpe Ratio Portfolio", value begin = $ 961925.43, value end = $ 1017080.07

Period 3: start date 05/01/2020, end date 06/30/2020
  Strategy "Buy and Hold", value begin = $ 937916.81, value end = $ 913415.30
  Strategy "Equally Weighted Portfolio", value begin = $ 830743.43, value end = $ 933833.25
  Strategy "Minimum Variance Portfolio", value begin = $ 826389.23, value end = $ 853450.05
  Strategy "Maximum Sharpe Ratio Portfolio", value begin = $ 974232.81, value end = $ 1175637.10

Period 4: start date 07/01/2020, end date 08/31/2020
  Strategy "Buy and Hold", value begin = $ 905419.63, value end = $ 994693.42
  Strategy "Equally Weighted Portfolio", value begin = $ 927429.17, value end = $ 1060410.21
  Strategy "Minimum Variance Portfolio", value begin = $ 855755.18, value end = $ 980881.46
  Strategy "Maximum Sharpe Ratio Portfolio", value begin = $ 1219488.39, value end = $ 1607469.19

Period 5: start date 09/01/2020, end date 10/30/2020
  Strategy "Buy and Hold", value begin = $ 993194.54, value end = $ 971914.18
  Strategy "Equally Weighted Portfolio", value begin = $ 1068021.21, value end = $ 998794.62
  Strategy "Minimum Variance Portfolio", value begin = $ 982633.87, value end = $ 942078.51
  Strategy "Maximum Sharpe Ratio Portfolio", value begin = $ 1641557.55, value end = $ 1554610.60

Period 6: start date 11/02/2020, end date 12/31/2020
  Strategy "Buy and Hold", value begin = $ 983801.02, value end = $ 1004435.67
  Strategy "Equally Weighted Portfolio", value begin = $ 1007615.85, value end = $ 1194009.60
  Strategy "Minimum Variance Portfolio", value begin = $ 950554.50, value end = $ 1005254.15
  Strategy "Maximum Sharpe Ratio Portfolio", value begin = $ 1553253.21, value end = $ 1790621.51

Period 7: start date 01/04/2021, end date 02/26/2021
  Strategy "Buy and Hold", value begin = $ 1005601.39, value end = $ 956244.15
  Strategy "Equally Weighted Portfolio", value begin = $ 1180423.17, value end = $ 1266799.62
  Strategy "Minimum Variance Portfolio", value begin = $ 1003280.29, value end = $ 974347.05
  Strategy "Maximum Sharpe Ratio Portfolio", value begin = $ 1738740.17, value end = $ 1854215.24

Period 8: start date 03/01/2021, end date 04/30/2021
  Strategy "Buy and Hold", value begin = $ 957791.42, value end = $ 1019731.31
  Strategy "Equally Weighted Portfolio", value begin = $ 1297147.46, value end = $ 1398677.74
  Strategy "Minimum Variance Portfolio", value begin = $ 974665.13, value end = $ 1087408.87
  Strategy "Maximum Sharpe Ratio Portfolio", value begin = $ 1902650.82, value end = $ 2061862.75

Period 9: start date 05/03/2021, end date 06/30/2021
  Strategy "Buy and Hold", value begin = $ 1022204.61, value end = $ 987842.85
  Strategy "Equally Weighted Portfolio", value begin = $ 1397454.10, value end = $ 1459030.32
  Strategy "Minimum Variance Portfolio", value begin = $ 1087214.87, value end = $ 1076065.34
  Strategy "Maximum Sharpe Ratio Portfolio", value begin = $ 2053359.96, value end = $ 2015852.83

Period 10: start date 07/01/2021, end date 08/31/2021
  Strategy "Buy and Hold", value begin = $ 993283.49, value end = $ 975250.12
  Strategy "Equally Weighted Portfolio", value begin = $ 1466439.38, value end = $ 1517538.82
  Strategy "Minimum Variance Portfolio", value begin = $ 1076108.30, value end = $ 1085948.88
  Strategy "Maximum Sharpe Ratio Portfolio", value begin = $ 2014854.33, value end = $ 2120429.10

Period 11: start date 09/01/2021, end date 10/29/2021
  Strategy "Buy and Hold", value begin = $ 974520.08, value end = $ 949068.41
  Strategy "Equally Weighted Portfolio", value begin = $ 1513305.17, value end = $ 1563148.29
  Strategy "Minimum Variance Portfolio", value begin = $ 1080422.13, value end = $ 1056577.04
  Strategy "Maximum Sharpe Ratio Portfolio", value begin = $ 2101168.08, value end = $ 2143099.77

Period 12: start date 11/01/2021, end date 12/31/2021
  Strategy "Buy and Hold", value begin = $ 951350.41, value end = $ 932471.35
  Strategy "Equally Weighted Portfolio", value begin = $ 1584369.08, value end = $ 1646240.36
  Strategy "Minimum Variance Portfolio", value begin = $ 1053830.53, value end = $ 1047872.09
  Strategy "Maximum Sharpe Ratio Portfolio", value begin = $ 2112466.24, value end = $ 2216754.37

**For the years 2020 and 2021:**

![image](https://github.com/user-attachments/assets/083877c9-68b6-4221-b7e5-29efb489ab5a)

**Weight Allocation for Minimum Variance Portfolio:**

![image](https://github.com/user-attachments/assets/07fa76c7-5b99-4e7c-91ea-ad2a4e2f100a)


**Weight Allocation for Maximum SHarpe's Ratio**

![image](https://github.com/user-attachments/assets/079ffde8-a91a-4abf-8f5b-b227e01d4a79)

**Can you suggest any improvement of the trading strategies you have implemented?**

Possible improvements can be the trading period, by optimizing the transaction costs and the trading period, we may find a more optimal period. Shorter periods may be beneficial if the transaction costs aren’t high and longer periods are preferred if the transaction costs are high.

Another improvement would be to optimize the rounding strategy. Currently the rounding procedure: After determining the optimal weight and determining the number of stocks in the portfolio, we use the numpy round function to round each stock to the nearest integer. We also keep track of the stocks that we rounded up. We run a while loop, in which in the first run, if there isn’t enough cash in the account only those units that were rounded up will go down by 1. If there still isn’t enough account, we overestimate and decrease all the stocks by 1 (stocks that are not 0). We then add a unit to each stock that should be rounded up until we go through all the stocks.

If we can decide which stocks to buy after decreasing all of the stocks, it may give a more optimal portfolio, whether how close it was to be rounded (since any weight after X.5 is rounded to X+1), or by the value of the stock (stocks worth $2000 vs stocks worth $200).

**Will select strategy 1/n portfolio at the beginning of period 1 and hold**
Until the end of period 12 (large transaction costs)

Period 1: start date 01/02/2020, end date 02/28/2020
  Strategy "Buy Equally Weighted and Hold", value begin = $ 990881.80, value end = $ 892363.31

Period 2: start date 03/02/2020, end date 04/30/2020
  Strategy "Buy Equally Weighted and Hold", value begin = $ 931075.01, value end = $ 868535.11

Period 3: start date 05/01/2020, end date 06/30/2020
  Strategy "Buy Equally Weighted and Hold", value begin = $ 837765.40, value end = $ 944421.16

Period 4: start date 07/01/2020, end date 08/31/2020
  Strategy "Buy Equally Weighted and Hold", value begin = $ 940832.47, value end = $ 1096615.92

Period 5: start date 09/01/2020, end date 10/30/2020
  Strategy "Buy Equally Weighted and Hold", value begin = $ 1107923.32, value end = $ 1019219.59

Period 6: start date 11/02/2020, end date 12/31/2020
  Strategy "Buy Equally Weighted and Hold", value begin = $ 1026359.89, value end = $ 1198894.93

Period 7: start date 01/04/2021, end date 02/26/2021
  Strategy "Buy Equally Weighted and Hold", value begin = $ 1186560.87, value end = $ 1258234.55

Period 8: start date 03/01/2021, end date 04/30/2021
  Strategy "Buy Equally Weighted and Hold", value begin = $ 1288250.80, value end = $ 1378075.91

Period 9: start date 05/03/2021, end date 06/30/2021
  Strategy "Buy Equally Weighted and Hold", value begin = $ 1374812.44, value end = $ 1458603.84

Period 10: start date 07/01/2021, end date 08/31/2021
  Strategy "Buy Equally Weighted and Hold", value begin = $ 1466617.35, value end = $ 1539061.21

Period 11: start date 09/01/2021, end date 10/29/2021
  Strategy "Buy Equally Weighted and Hold", value begin = $ 1536844.85, value end = $ 1609865.59

Period 12: start date 11/01/2021, end date 12/31/2021
  Strategy "Buy Equally Weighted and Hold", value begin = $ 1630591.70, value end = $ 1727212.77

# Implement Maximum Sharpe ratio strategy at the beginning of period 1


Period 1: start date 01/02/2020, end date 02/28/2020
  Strategy "Maximum Sharpe Ratio Portfolio from the start", value begin = $ 990063.05, value end = $ 937633.11

Period 2: start date 03/02/2020, end date 04/30/2020
  Strategy "Maximum Sharpe Ratio Portfolio from the start", value begin = $ 976204.45, value end = $ 1032177.75

Period 3: start date 05/01/2020, end date 06/30/2020
  Strategy "Maximum Sharpe Ratio Portfolio from the start", value begin = $ 988698.20, value end = $ 1192939.18

Period 4: start date 07/01/2020, end date 08/31/2020
  Strategy "Maximum Sharpe Ratio Portfolio from the start", value begin = $ 1237401.70, value end = $ 1630586.54

Period 5: start date 09/01/2020, end date 10/30/2020
  Strategy "Maximum Sharpe Ratio Portfolio from the start", value begin = $ 1665138.92, value end = $ 1576949.92

Period 6: start date 11/02/2020, end date 12/31/2020
  Strategy "Maximum Sharpe Ratio Portfolio from the start", value begin = $ 1575564.70, value end = $ 1816344.79

Period 7: start date 01/04/2021, end date 02/26/2021
  Strategy "Maximum Sharpe Ratio Portfolio from the start", value begin = $ 1763718.74, value end = $ 1880838.82

Period 8: start date 03/01/2021, end date 04/30/2021
  Strategy "Maximum Sharpe Ratio Portfolio from the start", value begin = $ 1929979.19, value end = $ 2091429.95

Period 9: start date 05/03/2021, end date 06/30/2021
  Strategy "Maximum Sharpe Ratio Portfolio from the start", value begin = $ 2082818.50, value end = $ 2044751.04

Period 10: start date 07/01/2021, end date 08/31/2021
  Strategy "Maximum Sharpe Ratio Portfolio from the start", value begin = $ 2043744.90, value end = $ 2150914.51

Period 11: start date 09/01/2021, end date 10/29/2021
  Strategy "Maximum Sharpe Ratio Portfolio from the start", value begin = $ 2131387.36, value end = $ 2173859.14

Period 12: start date 11/01/2021, end date 12/31/2021
  Strategy "Maximum Sharpe Ratio Portfolio from the start", value begin = $ 2142880.63, value end = $ 2248665.76
