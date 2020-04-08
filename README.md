# Analysis of a Brazilian e-Commerce Dataset
Olist is a marketplace that allows different companies to sell their products online. Many of them are small producers or traders with little experience in business administration. My goal is to help them identify potential ways to improve their sales and success on this specific marketplace. The client of this project are product sellers on olist and olist itself. The goal of my analysis is therefore to give some recommendations to the sellers on how to increase their sales on the platform.

## Questions
Some of the questions the analysis is trying to answer are:
### Products
* What are the most popular product categories?
* What is the most popular product?
* Are products with higher ratings more popular?
* Are some products more popular in some states?
* Seasonality in Sales?

### Payments
* What is the preferred payment method?
* Does the payment method depend on the state?
* Do people use more than one payment option at the same time?
* Do people use installments to pay for their orders?
* Correlation btw. purchase value, and installments

### Delivery
* What is the average delivery time? Does it depend on States?
* Is fast delivery correlated with higher reviews?
* Are reviews higher if the package arrives before the anticipated time?
* What is the average freight value?

### Sellers
* Revenue of the most successful seller?
* Revenue distribution of sellers?
* What do they sell on average?
* Do positive reviews lead to more sales?
* Where are sellers located?
* Do sellers sell more locally or over the entire country?

## Dataset
The dataset I’m using for my capstone project is available [here](https://www.kaggle.com/olistbr/brazilian-ecommerce). It is a dataset about an e-commerce marketplace in Brazil. It contains csv-files with information about around 100’000 purchase orders on the platform. The files come from a relational database and can be merge in the following way:

![alt text](https://i.imgur.com/HRhd2Y0.png "Database Structure")

### Data Preparation
1. The first thing in starting the project was to read in the csv-files from the olist database.
2. After reading in the datasets, they were merged into a master dataframe using the relationship visible in the graph above.
3. The dataset itself was already clean and complete, so it didn’t need a lot of preparation before starting with the descriptive analysis. The only challenge I faced was duplicate values in the master dataframe. The duplicate values exist in the database, because the customer may pay an order with more than one payment method. If she/he decided to pay with more than one payment method, the database created a sequence with the same order id. I dropped these duplicates, because for the business questions it was more important to have unique orders. When dropping the duplicate orders I kept the last in order to still keep the information about how many different types the person used. 
4. There were no missing values that needed to be replaced.
5. When analyzing the data it became clear that the dataset naturally has many outliers. The majority of customers and sellers on the platform are small and only have a couple of transactions during the period. There are however some customers and sellers that have large transactions which make data visualization difficult in many cases. The problem was addressed by using a log-scale on the variable in order to still display everything in a meaningful graph.

## Exploratory Analysis

![alt text](https://github.com/ldietsche/Springboard_Course/blob/master/Capstone%20Project%201/Pictures/Heatmap.png "Heatmap")
