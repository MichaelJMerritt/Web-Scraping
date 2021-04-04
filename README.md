# 3. Web Scraping with Python

[Back to Portfolio](https://michaeljmerritt.github.io/Portfolio/)

For this analysis I will need to collect publicly availaable data 

Large amounts of data needs to be collected before many analyses can be made.  This can be public data downloaded or scraped from websites or it can be queried from private databases.  Often this data is not immediately in a useable form and must be processed in order to make sure that any missing data is accounted for and the data types are consistent.  In this case I've pulled nearly 600,000 lines of daily stock price and volume data of nearly 7,000 different stocks from Yahoo! Finance.  Each stock was pulled from a separate web page and then needed to be combined into a single data file.

![Image of DataFrame](https://michaeljmerritt.github.io/Portfolio/Images/bigdfa.jpg)

Once the data is in a useable form and well understood it can be used to find indicators that are shown to signal changes.  This can be accomplished with simple algorithms for data that is well understood or with machine learning techniques if there are many seemingly unrelated features that affect the decision.

In this case the indicator we want is a simple but effective indicator called on-balance volume that is a function of the stock's price and its trade volume.  It is calculated first instantaneously and then as a one week moving average and a two week moving average.  A crossing of the two averages is flagged as an important event, and we'll capture the volume data as an indicator of relative signal strength.  The data necessary for these indicators will be added as new columns to the data file that was just created.

![Image of DataFrame](https://michaeljmerritt.github.io/Portfolio/Images/tempdfb.jpg)

Once the calculations are complete it is a good idea to test the algorithm to make sure it is able to find the desired indicators.  Since the crossings are of importance and not the actual value the OBV data is scaled down to fit on the same chart as the stock price line in black for easier viewing.  In this case not every event that is flagged by the algorithm is important, however any general trajectory change in the stock price seems to be close to an indicator.  After a number of iterations I am happy with this set of curves and how they can indicate potential changes in the stock price.  

![Image of Chart](https://michaeljmerritt.github.io/Portfolio/Images/test.jpg)

Finally it is time to inspect all of the data and identify indicators for all of the stock tickers.  For this analysis I will upload the entire data set as a table into a new Microsoft PowerBI project.  I have also added a table that has summary information about each stock that will be used to subdivide the various stocks into categories of similar industries and sectors.  I created a third table within Power BI that duplicated the summary table and used it to create a new column that calculates how close each stock's latest closing price is to its recent high values, and another column that calculates the ratio of the price's two week moving average vs its four week moving average. 

![Image of Tables](https://michaeljmerritt.github.io/Portfolio/Images/PBIDesigna.jpg)

I have linked these tables by the TICKER columns and created a dashboard that allows me to quickly review business category performance and then drill down through the individual stocks.  In this case I can select any sector or industry and get a chart of the sector's performance as well as a table of all stocks that make up that slice of data.  I can then sort that table by any of the columns of data and finally select individual stocks to see the performance chart for that stock.

![Image of Dashboard](https://michaeljmerritt.github.io/Portfolio/Images/PBIReport.jpg)

This is helpful for looking at information that is already well understood, however when the data is not well understood a very simple way to separate meaningful data points from the pack is to plot two measurements in a scatter plot.  In the dashboard below I have done just that, by plotting the two calculated fields I created against each other:  how close the stock's last closing price is to its most recent high price and the stock's momentum as determined by its moving average ratio.  

![Image of Scatter Dashboard](https://michaeljmerritt.github.io/Portfolio/Images/PBIReport2a.jpg)

So a point high on the Y axis is stock with its price near a recent maximum and a point high along the X axis shows a price rising faster in the past two weeks than the past four.  So in this case points in the upper right quadrant of the chart will be of most interest to find new stocks that are showing strong momentum.
