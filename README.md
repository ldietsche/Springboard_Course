# Analysis of a Brazilian e-Commerce Dataset
## Abstract
The following data science project investigates the sales data of Brazilian online market place called Olist. The marketplace  allows different companies to sell their products online. Many of them are small producers or traders with little experience in business administration. One of the main objectives is to find out about the business case of such platforms. It is of strong interests to analyze both sides of the market place, in order to find out whether it is possible to build a company on top of it or if the main winner is the marketplace itself.
The research result show one strong trend: there are a lot of small clients and resellers, but very few big ones. Most of the resellers are only able to generate little revenue.

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
* The strongest correlation can be examined between freight value and the price of the product, a potential explanation of that is that bigger products generally have a higher value.
* There is almost no correlation between the price and the review score - probably the expectations of the user are in line with the price paid and if the price is lower the customer already expects a lower quality.
* There is a low correlation between the number of installments and the price, a potential explanation would be that there are several customer groups: higher income customers that generally do not use installments, lower income customer that use installments more frequently - it would be interesting to investigate whether within this subgroup the relationship is different. Another possibility is that paying everything at once gives the user discounts and thus people are more incentivized to pay all up front.

### Products
![alt text](https://github.com/ldietsche/Springboard_Course/blob/master/Capstone%20Project%201/Pictures/Top_10_Categories_by_Revenue.png)
* Looking at the answers above shows, that the best categories for e-commerce are things that people use often but it is generally a specific size. One of the difficulties of e-commerce stores is still that it is hard to choose sizes for clothes for instance, therefore people are more likely to buy these things in a physical store and buy online things that they know what they are buying.
* The median revenue of a product is BRL 136.68 and the mean is 412.47 this shows not only that the average product does not generate a lot of revenue, but also confirms the hypothesis that there are many product that almost do not sell at all and some products that generate a lot of revenue.
* The best selling product generates BRL 63'885, as we only have the product_id we cannot investigate what product it is.
* There seems to be no correlation between the review score and the revenue of the product.

### Customers
![alt text](https://github.com/ldietsche/Springboard_Course/blob/master/Capstone%20Project%201/Pictures/Number_of_Units_Bought_by_Single_Customer.png)
* Similar to the sellers, the majority of buyers conduct very little purchases, there are some exceptions that buy a lot

### Installments
![alt text](https://github.com/ldietsche/Springboard_Course/blob/master/Capstone%20Project%201/Pictures/Comparison_of_Payment_Value_and_Number_of_Installments.png)
* It seems like there is no clear trend between the number of installments and the payment value of the order. It would be interesting to test whether the income has an impact on the number of installments chosen, but unfortunately due to the data available this is not possible.

### Seller
![alt text](https://github.com/ldietsche/Springboard_Course/blob/master/Capstone%20Project%201/Pictures/Distribution_Sellers_Revenue.png)
* There are many sellers on the platform, but a few of them are able to create a significant revenue, this can be seen in the distribution of the seller's revenue, the mean revenue and the median revenue. The median revenue is with BRL 821.48 substantially lower than the mean BRL 4'391.48. This means that there are some outliers that highly influence the mean, but do not have an impact on the median.
* It seems like there is no relationship between the order value and the total revenue of the seller.
* The largest seller created a revenue of BRL 229'472.63 in the examined period.

## Recommendation System
### Collaborative Filtering
* Unfornatuely the dataset does not give detailed insights about the customer such as age, gender so the only two variables that help to produce somewhat meaningful results are: the average review of the customer and the mean review a specific customer has given other products in the same category. Combining these two input factor and weighting them helps us to predict how likely a customer is to like the product(indicated by a potentially high rating).
* Accross all of the products if we create a collaborative filtering algorithm, we get a mean error of 1.12
* It should be mentioned that the ratings suffer a bias, because of two reasons, most of the people do not give a rating after an online purchase. If they do they give it because the product either exceeded or failed to meet their expecations. This leads to a sample bias. 

### Linear Regression
* Using a Linear Regression with the independent variables product_id, customer_state, product_category_name, product_photos_qty were not able to generate significant results and it would be better for Olist to use a collaborative filtering approach that learns over time.
* if one could include further characteristics such as age, income, gender, interests, a linear regression model might perform better than a collaborative filtering.

## Customer Lifetimevalue
* Knowing the customer lifetime value can help a company estimate the maximum customer acquisition cost for the company to be profitable. In order to estimate the customer lifetime value it would be good to have more than just two years of data, but there are some insights we can still gain from the data available.
* Using the package lifetimes can help us estimate the future transcation value per seller or customer, this will give us an idea, how much a customer is worth to the company/seller.
* Based on the average number of purchases and the purchase value one can estimate the overall customer lifetime value. The results show that the CLV of the analyzed period is around BRL 140 for the platform seller. 
* The revenue paid by the customer represents the overall revenue, as Olist only gets a commission on each transaction and a monthly subscription fee, the customer lifetime value of an Olist customer is much higher.

## Future Work
