# Analysis of a Macroeconomic Data
## Abstract

## Data
The dataset used is from quandl and can be obtained here. The Global Economic Indicators (ECD) data feed contains macroeconomic data for over 200 countries and regions. Over 200 indicators are available, with an average of 90 indicators per country. The data comes from official sources, such as central banks, statistical offices, finance ministries, stock exchanges, industry associations, and other government and semi-government bodies. Historical coverage varies by indicator, with some indicators going back as far as 1960.
Data is updated once daily at 2 pm GMT, Monday-Friday, with a lag of 1-2 business days. This allows an analysis of the present situation.

The data will be imported to Python using the quandl API.

## Questions
### Exchange Rates
* There are different theories about the determination of exchange rates, including purchasing power parity and interest rate parity. The project will investigate whether some of the economic variables of the dataset can be used to determine the long-term exchange rate fluctations. This would support companies to plan their currency hedging strategies. The impact of the variables on the exchange rates will be tested using a linear regression model or an LSTM.

### Money Supply
* A change in monetary supply can have different impacts, the research of this projects will investigate a potential linkage between monetary supply and stock returns, and the impact of the money supply of the united states on the gold price denominated in USD. The determination of the impact of monetary supply on the gold price and the stock prices will be done using a linear regression model or a LSTM.

### Recession Forecast
* The health of an economy is very important for businesses and investors, one of the goals is to use economic data to determine the probability of a recession in the subsequent quarter. A recession in economic terms is usually defined as two quarters of negative GDP growth rate. The probability of a recession will be determined using a logit-regression.

## Future Work

