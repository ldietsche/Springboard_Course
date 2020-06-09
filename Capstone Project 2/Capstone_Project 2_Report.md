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

### Data Selection
In order to get meaningful results, only the most frequently reported indicators were chosen and countries with little data were dropped. During this selection process the number of economic indicators was reduced to 116. During the initial analysis it became visible, that it is necessary to drop data before 2000. The reason for that is, that the data set before 2000 is very dispersed and the dataset often only contains good data of the countries afterwards.

## Questions
As all of the analysis in this projects are considering time series and the dependent variable has to be shifted in order to forecast something that happens in the future.

### Exchange Rates
* There are different theories about the determination of exchange rates, including purchasing power parity and interest rate parity. The project will investigate whether some of the economic variables of the dataset can be used to determine the long-term exchange rate fluctations. This would support companies to plan their currency hedging strategies. The impact of the variables on the exchange rates will be tested using a linear regression model or an LSTM.

## Exploratory Analysis
### PCA
Visualizing 116 variables is difficult and for that reason I chose to do a 2 Factor PCA to display the data visually. One time I used the country name as the color of the data points and once the date.

#### PCA - Countries
![alt text](https://github.com/ldietsche/Springboard_Course/blob/master/Capstone%20Project%202/Graphs/PCA_Countries.png)
* Similar to the sellers, the majority of buyers conduct very little purchases, there are some exceptions that buy a lot

#### PCA - Date
![alt text](https://github.com/ldietsche/Springboard_Course/blob/master/Capstone%20Project%202/Graphs/PCA_Years.png)
* Similar to the sellers, the majority of buyers conduct very little purchases, there are some exceptions that buy a lot


### Stationarity


## Future Work

