# Module_11_Challenge
## Forecasting Net Prophet

![MercadoLibre](../Screenshots/MercadoLibre.png)

## Background

With over 200 million users, MercadoLibre is the most popular e-commerce site in Latin America. I've been tasked with analysing the company's financial and user data in clever ways to help the company grow. So, I have had to find out if the ability to predict search traffic can translate into the ability to successfully trade the stock.

## What I've created

In a bid to drive revenue, I have produces a Jupyter notebook that contains the data preparation,  analysis, and my visualisations for all the time series data that the company needs to understand. This notebook contains the following:

- Visual depictions of seasonality (as measured by Google Search traffic) that are of interest to the company.

- An evaluation of how the company stock price correlates to its Google Search traffic.

- A Prophet forecast model that can predict hourly user search traffic.

- Answers to the questions in the instructions that are writen in the Jupyter notebook.

- (The optional) A plot of a forecast for the company’s future revenue.

And of course a README.md file that has summarised my models and findings.

## Step 1: Find Unusual Patterns in Hourly Google Search Traffic


Read the search data into a DataFrame, and then slice the data to just the month of May 2020. (During this month, MercadoLibre released its quarterly financial results.) Use hvPlot to visualise the results. Do any unusual patterns exist?

Calculate the total search traffic for the month, and then compare the value to the monthly median across all months. Did the Google Search traffic increase during the month that MercadoLibre released its financial results?


#### Results of slicing the data into the month of May 2020.

![Screenshot1_2](../Screenshots/Screenshot1_2.png)

#### HvPlot results for the month of May 2020.

![Screenshot1_3](../Screenshots/Screenshot1_3.png)

Using the formula:  traffic_may_2020 = df_may_2020["Search Trends"].sum()
- traffic_may_2020 totalled 38181

- Also for median_monthly_traffic averaged 35172.5 visits

Therefor using: traffic_may_2020 >= median_monthly_traffic
- Traffic confirm an obvious "True" result 

## Step 2: Mine the Search Traffic Data for Seasonality

The marketing department realises that they can use the hourly search data, too. If they can track and predict interest in the company and its platform for any time of day, they can focus their marketing efforts around the times that have the most traffic. This will get a greater return on investment (ROI) from their marketing budget.

To that end, I was tasked to mine the search traffic data for predictable seasonal patterns of interest in the company. To do so, I completed the following steps:

Group the hourly search data to plot the average traffic by the day of the week (for example, Monday vs. Friday).

Using hvPlot, visualise this traffic as a heatmap, referencing index.hour for the x-axis and index.dayofweek for the y-axis. Does any day-of-week effect that you observe concentrate in just a few hours of that day?

Group the search data by the week of the year to find if the search traffic tended to increase during the winter holiday period (Weeks 40 through 52).

#### Below, Group the hourly search data and plot the average traffic by the day of the week, Monday = 0 to Sunday = 6.

![Screenshot2_1](../Screenshots/Screenshot2_1.png)

#### A hvPlot to visualize this traffic as a heatmap, referencing the index.hour as the x-axis and the index.dayofweek as the y-axis.

![Screenshot2_2](../Screenshots/Screenshot2_2.png)

Question: Does any day-of-week effect that you observe concentrate in just a few hours of that day?

Answer: From the above heat map, it appears to be consentrated in the late evening to early morning hours of the day from 22:00 to 01:00 hours, possibly suggesting after work searches.

#### Hourly Search data grouped for the Ave search Traffic by Week or the Year.
![Screenshot2_3](../Screenshots/Screenshot2_3.png)

Question: Does the search traffic tend to increase during the winter holiday period (weeks 40 through 52)?

Answer: Traffic does increase however traffic is low in the preceding period. Week 42 has the lowest search traffic through to a period high in week 51. Notably, the line graph shows a steep drop off at week 52 which should be expected, likely due to the Christmas holiday period.

## Step 3: Relate the Search Traffic to Stock Price Patterns
 The finance group want to know if any relationship between the search data and the company stock price exists, and they asked if I could investigate.

To do so, I completed the following steps:

- Read in and plot the stock price data. Concatenate the stock price data to the search data in a single DataFrame.

#### Results table of Stock price csv head and tail.

![Screenshot3_1](../Screenshots/Screenshot3_1.png)

#### MercadoLibre Closing price hvPlot.
![Screenshot3_2](../Screenshots/Screenshot3_2.png)

#### Concatenated Dataframes results head and tail.

![Screenshot3_3](../Screenshots/Screenshot3_3.png)
- Market events emerged during the year of 2020 that many companies found difficult. But, after the initial shock to global financial markets, new customers and revenue increased for e-commerce platforms. Slice the data to just the first half of 2020 (2020-01 to 2020-06 in the DataFrame), and then use hvPlot to plot the data. Do both time series indicate a common trend that’s consistent with this narrative?

#### Sliced result of the concatenated dataframe to first half of 2020
![Screenshot3_4](../Screenshots/Screenshot3_4.png)

#### First half search trends hvPlots
![Screenshot3_5](../Screenshots/Screenshot3_5.png)



Question: Do both time series indicate a common trend that’s consistent with this narrative?

Answer: Yes, it could be considered inter-related. I note that there may be a reporting issue with the data for March in both sets. At this time, we can see a considerable pause due to the lack of volitality during this period. Interestingly the drop in share price corelates to a drop in overall search trends until the lead up to the reporting period and a substanital spike after the positive Q1 May financials were released all leading to the all time highs by the end of June.

- Create a new column in the DataFrame named “Lagged Search Trends” that offsets, or shifts, the search traffic by one hour. Create two additional columns:

#### HvPlot to visualise stock volatility
![Screenshot3_6](../Screenshots/Screenshot3_6.png)
- “Stock Volatility”, which holds an exponentially weighted four-hour rolling average of the company’s stock volatility

- “Hourly Stock Return”, which holds the percent change of the company's stock price on an hourly basis

#### Head and Tail outputs of the Hourly Stock Return dataframe
![Screenshot3_7](../Screenshots/Screenshot3_7.png)

####Correlation Table of Stock Volatility, Lagged Search Trends and Hourly Stock Return
![Screenshot3_8](../Screenshots/Screenshot3_8.png)

- Review the time series correlation, and then answer the following question:

Question: Does a predictable relationship exist between the lagged search traffic and the stock volatility or between the lagged search traffic and the stock price returns?

Answer: The correlation table above demonstrates a very low correlation and would be considered unrelated. I note also that the Search Trends and Stock Volitality are slightly negatively (or inversely) correlated suggesting that they would move opposite to each other.

## Step 4: Create a Time Series Model with Prophet
I produced a time series model that analyses and forecasts patterns in the hourly search data. To do so, I completed the following steps:

- Set up the Google search data for a Prophet forecasting model.

- After estimating the model, plot the forecast. How's the near-term forecast for the popularity of MercadoLibre?

#### Resetting the index for Prophet syntax
![Screenshot4_1](../Screenshots/Screenshot4_1.png)

#### A plot of the Prophet forecast for the Mercado trends data
![Screenshot4_2](../Screenshots/Screenshot4_2.png)

Question: How's the near-term forecast for the popularity of MercadoLibre?

Answer: The forecast trends shows an initial decline to the centre of the forecast period before recovering to levels near the start of the prediction.
####Setting the index in the forecast_mercado_trends dataframe to the ds datetime column.
![Screenshot4_3](../Screenshots/Screenshot4_3.png)

#### A hvPlot visualisation of the yhat, yhat_lower and yhat_upper   
![Screenshot4_4](../Screenshots/Screenshot4_4.png)

#### Forecast results for the forecast_mercado_trends dataframe
![Screenshot4_5](../Screenshots/Screenshot4_5.png)


- Plotted the individual time series components of the model to answer the questions...

Question: What time of day exhibits the greatest popularity?

Answer: As per the previous results, the daily charts shows the late evening to early morning period has the greatest search traffic.

Question: Which day of week gets the most search traffic?

Answer: From the weekly chart it appears that Tuesday has the greatest volume of search traffic.

Question: What's the lowest point for search traffic in the calendar year?

Answer: From the yearly chart above, mid October appears to have the lowest traffic over the calendar year.

## Step 5 (Optional): Forecast Revenue by Using Time Series Models

The finance group wants a forecast of the total sales for the next quarter. This will dramatically increase their ability to plan budgets and to help guide expectations for the company investors.

To do so, I completed the following steps:

- Read in the daily historical sales (that is, revenue) figures, and then apply a Prophet model to the data. The daily sales figures are quoted in millions of USD dollars.

- Interpret the model output to identify any seasonal patterns in the company's revenue.

- Produced a sales forecast for the finance group. Give them a number for the expected total sales in the next quarter. Include the best- and worst-case scenarios to help them make better plans.

#### A review of the df_mercado_sales dataframe
![Screenshot5_1](../Screenshots/Screenshot5_1.png)


#### HvPlot of daily sales figures 
![Screenshot5_2](../Screenshots/Screenshot5_2.png)

#### Plot_componets results to analyse seasonal patterns in revenue
![Screenshot5_3](../Screenshots/Screenshot5_3.png)

#### Predictions of the Mercado sales
![Screenshot5_4](../Screenshots/Screenshot5_4.png)

Question: For example, what are the peak revenue days? (Mondays? Fridays? Something else?)

Answer: From the weekly chart it is clear that the peak revenue day is Wednesday.

#### A sample of the results of the forecast quarter Dataframe for the period 1 July 2020 to 30 September 2020
![Screenshot5_5](../Screenshots/Screenshot5_5.png)

#### A hvPlot of the summed values in the forecast_quarter dataframe
![Screenshot5_6](../Screenshots/Screenshot5_6.png)

Based on the forecast information generated above, the best and worst case scenarios, to better help the finance team plan.

Answer: From the above plot, we can see a gradual increase in sales is predicted most likely achieving $23.462 Million in sales revenue. That said, the worst case is $21.433 Million and the best case would be $25.34 Million.