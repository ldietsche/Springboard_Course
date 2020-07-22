# Analysis of a Macroeconomic Data
## Abstract

## Data
The dataset used is from quandl and can be obtained [here](https://www.quandl.com/data/WWDI-World-Bank-World-Development-Indicators/documentation). The Global Economic Indicators (ECD) data feed contains macroeconomic data for over 200 countries and regions. Over 200 indicators are available, with an average of 90 indicators per country. The data comes from official sources, such as central banks, statistical offices, finance ministries, stock exchanges, industry associations, and other government and semi-government bodies. Historical coverage varies by indicator, with some indicators going back as far as 1960.
Data is updated once daily at 2 pm GMT, Monday-Friday, with a lag of 1-2 business days. This allows an analysis of the present situation.

### Data Download
The data was imported to Python using the quandl API. Due to hourly limitations, and the quantity of data, the API calls were done in a different file, stored on github under: Capstone 2_Data Import.ipynb, it can be accessed [here](https://github.com/ldietsche/Springboard_Course/blob/master/Capstone%20Project%202/Capstone%202_Data%20Import.ipynb)

Using the Data Import File, all indicators available for all countries in the dataset were imported using the API. Upon downloading the data a local copy was stored as a csv in order to import it again. 

### Data Import
Once all of the data was downloaded, it was imported into the analysis notebook "Capstone 2_Data Analysis", which can be accessed [here](https://github.com/ldietsche/Springboard_Course/blob/master/Capstone%20Project%202/Capstone%202_Data%20Import.ipynb). In order to make reopening faster it was stored locally as a pickle as well. Exchange rates data was imported using the Yahoo Finance API. Upon downloading this data it was merged into the master dataframe and exported as a pickle to facilitate faster import in subsequent sessions.

### Data Selection
In order to get meaningful results, only the most frequently reported indicators were chosen and countries with little data were dropped. During this selection process the number of economic indicators was reduced to 116. During the initial analysis it became visible, that it is necessary to drop data before 2000. The reason for that is, that the data set before 2000 is very dispersed and the dataset often only contains good data of the countries afterwards. After analyzing the results of the Dickey Fuller test and the exploratory analysis, indicators with insufficient data were dropped. Unfortunately many countries do not report indicators on a frequent basis and thus cannot be considered for the training of the exchange rate forecast.

### Missing Data
Most of the missing data was dropped in the selection of the indicator or the countries. Nevertheless there were missing data entries, some of them due to the lack of data for a specific country or different reporting frequencies(some countries report certain indicators monthly, others quartely, and some even just annually. Because a macroeconomic indicator is essentially a backward looking number, the missing numbers were backfilled.

## Questions
As all of the analysis in this projects are considering time series and the dependent variable has to be shifted in order to forecast something that happens in the future.

### Exchange Rates
* There are different theories about the determination of exchange rates, including purchasing power parity and interest rate parity. The project will investigate whether some of the economic variables of the dataset can be used to determine the long-term exchange rate fluctations. This would support companies to plan their currency hedging strategies. The impact of the variables on the exchange rates will be tested using a linear regression model or an LSTM.

## Exploratory Analysis
### PCA
Visualizing 116 variables is difficult and for that reason I chose to do a 2 Factor PCA to display the data visually. One time I used the country name as the color of the data points and once the date.

#### PCA - Countries
![alt text](https://github.com/ldietsche/Springboard_Course/blob/master/Capstone%20Project%202/Graphs/PCA_Countries.png)
* Using the countries as different colors shows the majority of them is centralized, but some of them are moving to the outside of the graph. Looking at the most extreme cases: ID (Indonesia), IR (Iran), SN (Senegal), ER (Eritrea), TR (Turkey), CN (China), TW (Taiwan), US (United States), ZM (Zambia), LY (Lybia), KR (South Korea). What is surprising is to find the US and Korea in this list, because it seems like countries that moved from the center to the outside are economies with higher volatility and growth due to their development or political circumstances.

#### PCA - Date
![alt text](https://github.com/ldietsche/Springboard_Course/blob/master/Capstone%20Project%202/Graphs/PCA_Years.png)
* Using the date as a color indicator is very helpful too, because it shows clearly, that all countries start in the middle and then some of them are moving more towards the outside as time progresses.

### Stationarity
Stationarity in time series analysis is important, because stationary processes are easier to analyze as the range doesn't change through time, 
### Augmented Dickey Fuller Test
In order to identify stationary time series an augmented Dickey Fuller test was conducted for each of the indicators.
The Augmented Dickey Fuller test is essentially a hypothesis testing with:
* H0: Time series is not stationary
* HA: Time series is stationary

The ADF values between the countries for specific indicators varied significantly. For that reason I considered the distribution of the values and took a decision considering the meaning of the indicator and its time series chart for each country. 

![alt text](https://github.com/ldietsche/Springboard_Course/blob/master/Capstone%20Project%202/Graphs/ADF_Results_Indicator%2025.png)

After the analysis, the non-stationary indicators were differenced in order to be stationary, in other words instead of considering the GDP the change in GDP was considered.

## Machine Learning Models
### Linear Model with 
The baseline model used for estimating the forecasts was an OLS that used independent variables (economic variables at t-1) to forecast the dependent variable (exchange rate at t). The time shift is necessary, because the idea is to forecast the future change in exchange rates. Please find below the standard statistical output:

| Model | Df Model |  R-squared |Adj. R-squared  | F-statistic |Prob (F-statistic)|AIC       |BIC      |
| :-:   | :-:      | :-:        | :-:            | :-:         |:-:               |:-:       |:-:      |
| OLS   | 108      |  0.002     |-0.002          | 0.5478      |1.00              |2.702e+05 |2.711e+05|

### Linear Model with 22 Factors and Subsequent Quarter Return
After the baseline model the independent factors were reduced to the 22 most relevant ones. Relevancy in this context included both theoretical relevancy based on economical theory and statistical relevancy in the baseline model. In addition to that a country dummy variable was introduced in order to account for geographical differences between countries. In the phase of the exploratory analysis it became clear, that there is a huge difference between countries, especially if they are in different stages of economic development. 

| Model | Df Model |  R-squared |Adj. R-squared  | F-statistic |Prob (F-statistic)|AIC       |BIC      |
| :-:   | :-:      | :-:        | :-:            | :-:         |:-:               |:-:       |:-:      |
| OLS   | 185      |  0.034     |0.028           | 5.990       |1.61e-128         |3.666e+05 |3.682e+05|

As one can see in the statistical output, increasing the forecasting horizon and introducing country dummies increases the explanatory power of a model even though we have less independent factors. This is very favorable, because it allowed for a reduced complexity. The increased F-statistic further shows that the second model is far more likely to have a better forecasting power than a model with no independent variable. That being said, an R2 adjusted of 2.3% is not sufficient enough in order to use this model in order to forecast exchange rates close enough to reduce hedging costs or even trade on it. For that reason a VAR model will be developed in order to see if it is possible to increase explanatory power by increasing a time-dependency.


### VAR with 22 Factors & Subsequent Quarter Price Change
Introducing time dependency into the model may help, because the development of economic variables through time is important. A VAR model can account for that, because it can capture the linear interdependencies among multiple time series. In the case at hand we are however only interested in forecasting one variable. Country dummies are introduced using exogenous variables and help to account for geographical differences.<br>
The model was estimated using lags from 1 to 9. The table below shows the development of the AIC, BIC, FPE, and HQIC from lag 1 through 5.

| Lag   | 1       |  2      |3        | 4       |5       |
| :-:   | :-:     | :-:     | :-:     | :-:     |:-:     |
| AIC   | -204.82 | -204.80 |-204.77  | -204.74 |-204.71 |
| BIC   | -203.31 | -203.10 |-202.87  | -202.65 |-202.43 |
| FPE   | 1.12    |  1.13   |1.17     | 1.20    |1.24    |
| HQIC  | -204.33 | -204.24 | -204.15 | -204.06 |-203.97 |

Considering the statistical output above it makes sense to select the model with lag 1. The reason for that is that FPE increases with the lags, whereas the AIC, BIC, and HQIC stays more or less constant.

## Results
In the following graphs the VAR model with lag 1 was used to forecast the exchange rate between the local currency and the USD. After the forecast the inverse transformation on the data is applied in order to get them into the original range. Three countries were picked to get an estimate on how accurate the forecast would be in a real life setting.
### Brazil
![alt text](https://github.com/ldietsche/Springboard_Course/blob/master/Capstone%20Project%202/Graphs/BR.png)
### Germany
![alt text](https://github.com/ldietsche/Springboard_Course/blob/master/Capstone%20Project%202/Graphs/DE.png)
### Russia
![alt text](https://github.com/ldietsche/Springboard_Course/blob/master/Capstone%20Project%202/Graphs/RU.png)

The graphs show, that for some countries the VAR model workes better than for others. It does perform better than a random guess, but its accuracy is not as high as expected in the beginning. There are several potential reasons for this, amongst them:
- **Publication Date:** economic data is never published on the end of the month/quarter. In order to be exact when analzying the impact of the economic variables on the exchange rate one therefore would need to have the exact publication date. Unfortunately, this information is not available for this study and it would exceed the purpose of this study to find the individual publication date. It is therefore possible that the explanatory power of the models are bigger when accounting for this time-shift.
- **Variance:** As models are trained accross different countries with different economic development the variance of certain indicators is very different. Having a big variance between training samples leads to lower forecasting power.
- **Data:** During the data wrangling and exploration phase it became clear that the economic data is not always available for all countries and that makes it difficult to use it.

## Future Work
- **LSTM**
- model for one country.

