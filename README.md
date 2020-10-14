# Stock Market Analysis Project
## Introdution
We'll be analyzing stock data related to a few car companies, from Jan 1 2012 to Jan 1 2017. We would be analyzing how these companies are related in an Oligopoly type environment. The companies are:
* TESLA
* FORD MOTORS
* GENERAL MOTORS

## Importing
We import data from the Google Finance API using pandas-datareader and put the data in a pandas-dataframe.

## Visualizing Data
We plot the data using matplotlib.pyplot and find the anomalies in the data and then drop the null values. 

We find that there was a sharp spike in volume traded for Ford Motors on 18th December, 2013. This was after the company [warned](https://money.cnn.com/2013/12/18/news/companies/ford-profit/index.html) the cost of its aggressive push to launch new products would cut into profits next year.

The Open Price Time Series Visualization makes Tesla look like its always been much more valuable as a company than GM and Ford. But to really understand this we would need to look at the total market cap of the company, not just the stock price. Unfortunately our current data doesn't have that information of total units of stock present. But what we can do as a simple calcualtion to try to represent total money traded would be to multply the Volume column by the Open price.

## Interrelation between companies
Finally lets see if there is a relationship between these stocks, after all, they are all related to the car industry. We can see this easily through a scatter matrix plot and through the candlestick plot.

## Financial Analysis
### 1.Daily Percentage Change
First we will begin by calculating the daily percentage change. Daily percentage change is defined by the following formula: r<sub>t</sub> = (p<sub>t</sub> / p<sub>t-1</sub>)-1
 
This defines r_t (return at time t) as equal to the price at time t divided by the price at time t-1 (the previous day) minus 1. Basically this just informs you of your percent gain (or loss) if you bought the stock on day and then sold it the next day. While this isn't necessarily helpful for attempting to predict future values of the stock, its very helpful in analyzing the volatility of the stock. If daily returns have a wide distribution, the stock is more volatile from one day to the next.

### 2.Cumulative Daily Returns
**Daily Return** : Daily return is the profit/loss made by the stock compared to the previous day. (This is what ew just calculated above). A value above one indicates profit, similarly a value below one indicates loss. It is also expressed in percentage to convey the information better. (When expressed as percentage, if the value is above 0, the stock had give you profit else loss). 
**Cumulative Return**: While daily returns are useful, it doesn't give the investor a immediate insight into the gains he had made till date, especially if the stock is very volatile. Cumulative return is computed relative to the day investment is made.  If cumulative return is above one, you are making profits else you are in loss.

The formula for a cumulative daily return is: i<sub>i</sub> = (1 + r<sub>t</sub>) * i<sub>t-1</sub>

Here we can see we are just multiplying our previous investment at i at t-1 by 1+our percent returns. Pandas makes this very simple to calculate with its cumprod() method. Using something in the following manner:

    df[daily_cumulative_return] = ( 1 + df[pct_daily_return] ).cumprod()
    
