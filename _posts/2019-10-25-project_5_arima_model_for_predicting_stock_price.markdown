---
layout: post
title:      "Project 5: Arima model for predicting stock price"
date:       2019-10-25 13:29:36 +0000
permalink:  project_5_arima_model_for_predicting_stock_price
---


## Introduction
In Project 5, the objective is to predict Apple Stock's closing price based past 1380 days of performance. Arima is one of the method being tested in the project. This blog will go into the detail of ARIMA prediction.

Intuition: only use the stocks closing price as input dataset to see if previous days momentum is sufficient to predict today’s closing price. Y = (Auto-Regressive Parameters) + (Moving Average Parameters)


## Data
Raw Data:
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images%20for%20Static%20vs%20Dynamic/data%20head().png)

For ARIMA, we only need the 'Last Price'. Let's understand the data a bit better with Auto Correlation test and ADF test.

Autocorrelation test: It is not too helpful, effectively anything less than 20 days lag seems to be relevant.
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images%20for%20ARIMA/Autocorrelation.png)

ADF Test: Intuitively, we know it is a non-stationary series, but let's have a ADfuller test anyway to verify.
Null Hypothesis (H0): If failed to be rejected, it suggests the time series has a unit root, meaning it is non-stationary. It has some time dependent structure.
p-value > 0.05: Fail to reject the null hypothesis (H0), the data has a unit root and is non-stationary.
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images%20for%20ARIMA/ADF%20test.png)

## Model
The biggest challenge for ARIMA is find the the right parameters p, d and q.
p = the number of autoregressive terms
d = the number of nonseasonal differences 
q = the number of moving-average terms 

In order to test different variations, few functions are built as below:

Evaluating individual ARIMA result with a given set of (p, d, q). Note the training set is dynamically expadning.
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images%20for%20ARIMA/Evaluate%20individual%20arima.png)

Evaluating different combination of (p, d, q) through 3 sets of loops.
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images%20for%20ARIMA/Evaluate%20different%20pdq.png)

Try different combination of (p, d, q).
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images%20for%20ARIMA/Try%20different%20pdq.png)

## Winning Model
The winning model is an ARIMA model with p=3, d=2, q=2 MSE=12.78

![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images%20for%20ARIMA/winning%20model.png)

As much as the graph looks good optically, a MSE of 12.78 represents an error of 3.6, which is ~1.5% daily error term. This may sound small, but given the daily movement on the stock is sub 1%. This model is definitely not sufficient for day trading. This model had effective assume that the stock has no intrinc charateristic or fundamental features, but simply a set of data, which is not how stock market behaves. However, I can see ARIMA being more useful for ETF or indices where it is a basket of all, and hence each individualism can be ignored.


