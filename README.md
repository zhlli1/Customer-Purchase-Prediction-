# Customer Purchase Prediction 

## Introduction
The goal of this project is to develop a predictive model based on the order and online customer behavior data to forecast product category (prodcat1) a customer is likely to order.  The data was obtained from Shutterfly Inc. (source: https://github.com/sflydatascience/homework1/blob/master/data.zip). The data includes two time-series datasets, one is Non-Transactional Data (Online data), another is Transactional Data (Order Data). The Non-Transactional Data (Online data) starts from 2016-01-01 to 2017-12-31, while the Transaction Data starts from 2016-01-01 to 2019-01-02.

To make the customer purchase prediction model, this project included the following sections :
1.	Exploration and Understanding of the Data Sets
<br>
    1.1	Product Analysis
    <br>
        1.1.1	Popularity of prodast1 in terms of the number of orders.
        1.1.2	Popularity of prodast1 in terms of the number of browsing sessions.
        1.1.3	The revenue of each type of prodcast1
    1.2	Customer Behavior 
        1.2.1	Which channel is more popular in terms of event1 and event2
        1.2.2	Customer Purchase RFM (Recency, Frequency, Monetary value)  Analysis  
        1.2.3	Customer Segment with RMF 
2.	Model Design and Sampling 
    2.1	Training/ Testing Data Split 
    2.2	 Label Generation 
3.	Feature engineering & Selection 
    3.1	Non-Transaction Data Features 
        3.1.1	How the customer interacts with your website (online event1 and online event2 )
        3.1.2	How many times a customer browsing an item (No. of sessions) 
    3.2	Transaction Data Features
        3.2.1	Total Number of orders 
        3.2.2	Order Recency 
        3.2.3	Order Frequency of each category of procat1 
        3.2.4	Total order revenue
    3.3	Feature Correlation Matrix 
4.	Model Generation  
    4.1	Grid Search to find the best parameters 
    4.2	Random Forest Classification Model
    4.3	 Feature Importance Analysis 
5.	Model Evaluation 
    5.1	Confusion Matrix 
    5.2	 AUC
6.	Summary & Discussion 


## Customer Segmentation Analysis (RMF)
RMF stands for Recency, Frequency and Monetary value and the RMF metrics are calculated for each customer.  
- Regency: Who have purchased recently? The number of days since last purchased. 
- Frequency: who has purchased frequently? It means the total number of purchases. 
- Monetary Value: who have high purchase amount? It means the total money customer spend.

Generally, the lowest recency, highest frequency and monetary amounts are our best customers. 
![alt text](https://github.com/zhlli1/Customer-Purchase-Prediction-/blob/master/RMF.png)

The following steps are used to run the RMF Analysis : 
- Calculate the RMF metrics for each customer.
- Add segment numbers to RMF table based on the quantile values.
- Sort according to the RMF scores from the best customers.
- Label the customer for different segments based on their RFM scores.

## Prediction Model Design

### Training /Testing Data Split 
Considering the time frame of the dataset and the customer recency distribution, I will use one-year data for generating features and half-year data for generating labels.
![alt text](https://github.com/zhlli1/Customer-Purchase-Prediction-/blob/master/trainTestSplit.jpg)

### Label Generation 
Binary Labels for each category in procast1. 
1 : Purchased during the labeling time frame 
0 : Not Purchased during the labeling time frame

### Features Description: 
Non-Transactional Data:
- How the customer interacts with your website (online event1 and event2). Which channel attracts more customers?
 - Number of sessions for each category in event1 and event2 
   - event1_cat1 
   - event1_cat2 
   - event1_cat4 
   - event1_cat5 
   - event1_cat6 
   - event1_cat7 
   - event1_cat8 
   - event1_cat9 
   - event1_cat10
   - event1_cat11
   - event2_cat1 
   - event2_cat2 
   - event2_cat3 
   - event2_cat4 
   - event2_cat5 
   - event2_cat6 
   - event2_cat7 
   - event2_cat8 
   - event2_cat9 
   - event2_cat10

Transactional Data: 
- Total order number  
   - Total_Order : Total number of orders of each customer in the training phase 
- Order Regency 
   - Recency : Number of days since last purchased 
- Order Frequncy  : order frequency of each category in procast1 per customer in the training phase 
   - cat1_freq
   - cat2_freq
   - cat3_freq
   - cat4_freq
   - cat5_freq
   - cat7_freq
- Order Revenue 
   - Total_Revenue : total revenue of each customer in the training phase

## Results 
Since the purchasing rate is very low based on the previous data, the evaluation metrics used here is AUC, which accounts for both true- positive and false-positive rates.  

![alt text](https://github.com/zhlli1/Customer-Purchase-Prediction-/blob/master/auc.png)
The micro/macro-average AUC is around 0.60.  The highest AUC score for class3 in procast1, which his around 0.71.

## Summary 
The customer segmentation analysis indicated that most of the customers are inactive and purchase little. There’s a huge difference between best customers and lost cheap customers in terms of recency, frequency, and revenue.  The company should use different strategies to market each group of customers. 

- High Value: Improve Retention
- Mid Value: Improve Retention + Increase Frequency
- Low Value: Increase Frequency

The purchasing behavior is depended on the total number of order, total revenue, recency and previous purchasing behavior of each customer. The prediction results still show that most of the people will unlikely to make any purchase in the following half years. While among all the category, class 2 in procat1 is the most likely purchase category across all the customers.  Therefore, the marketing team still need to work on improving retention and frequency. 

## The problem of the Data : 

The online data only include 3 class in online browsing category (procat1), while proact1 has a total of 6 classes. The online data is not complete, making the model less robust. 

The more details can be checked in shutterfly.ipynb.


