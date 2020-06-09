# Analysis of a Macroeconomic Data
## Abstract

## Data
The dataset used is from quandl and can be obtained [here](https://www.quandl.com/data/WWDI-World-Bank-World-Development-Indicators/documentation). The Global Economic Indicators (ECD) data feed contains macroeconomic data for over 200 countries and regions. Over 200 indicators are available, with an average of 90 indicators per country. The data comes from official sources, such as central banks, statistical offices, finance ministries, stock exchanges, industry associations, and other government and semi-government bodies. Historical coverage varies by indicator, with some indicators going back as far as 1960.
Data is updated once daily at 2 pm GMT, Monday-Friday, with a lag of 1-2 business days. This allows an analysis of the present situation.

### Data Download
The data was imported to Python using the quandl API. Due to hourly limitations, and the quantity of data, the API calls were done in a different file, stored on github under: Capstone 2_Data Import.ipynb, it can be accessed [here](https://github.com/ldietsche/Springboard_Course/blob/master/Capstone%20Project%202/Capstone%202_Data%20Import.ipynb)

Using the Data Import File, all indicators available for all countries in the dataset were imported using the API. Upon downloading the data a local copy was stored as a csv in order to import it again. 

### Data Import
Once all of the data was downloaded, it was imported into the analysis notebook. In order to make reopening faster it was stored locally as a pickle as well. Exchange rates data was imported using the Yahoo Finance API. Upon downloading this data it was merged into the master dataframe and exported as a pickle to facilitate faster import in subsequent sessions.

### Data Preparation


## Questions
As all of the analysis in this projects are considering time series and the dependent variable has to be shifted in the rows, because we try to forecast something that happens in the future.

### Exchange Rates
* There are different theories about the determination of exchange rates, including purchasing power parity and interest rate parity. The project will investigate whether some of the economic variables of the dataset can be used to determine the long-term exchange rate fluctations. This would support companies to plan their currency hedging strategies. The impact of the variables on the exchange rates will be tested using a linear regression model or an LSTM.

### Money Supply
* A change in monetary supply can have different impacts, the research of this projects will investigate a potential linkage between monetary supply and stock returns, and the impact of the money supply of the united states on the gold price denominated in USD. The determination of the impact of monetary supply on the gold price and the stock prices will be done using a linear regression model or a LSTM.

### Recession Forecast
* The health of an economy is very important for businesses and investors, one of the goals is to use economic data to determine the probability of a recession in the subsequent quarter. A recession in economic terms is usually defined as two quarters of negative GDP growth rate. The probability of a recession will be determined using a logit-regression.

## Exploratory Analysis
### Stationarity
### PCA

## Future Work

