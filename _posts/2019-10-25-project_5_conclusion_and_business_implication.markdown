---
layout: post
title:      "Project 5: Conclusion and Business Implication"
date:       2019-10-25 14:19:09 +0000
permalink:  project_5_conclusion_and_business_implication
---


In Project 5, the objective is to predict Apple Stock's closing price based past 1380 days of data. There 11 data points per day. Some are technical, some are fundamental, and some are macro. (Technical data: Open Price, Last Price, Volume.
Fundamental data: Financial Leverage, PE RATIO, Cash Flow per Share, Price to Book Ratio, Dividend Per Share. 
Macro data: SPX, VIX, PPUT. (Note: VIX - volatility index; PPUT - put option price for S&P; SPX - S&P price.))

A number of methods are used: Deep Learning, Ensemble Machine learning (Bagging, Random Forest, Adaboost), Linear Regressioin (Lasso, Ridge, Linear), ARIMA, PCA, Dynamic Model, and Static Model, and even Prophet (facebook algorithm).

The best result was Lasso Linear Regression with Dynamic training set. It produced a MSE of 5.4. A MSE of 5.5 implies about 1% variability from actual data. This is a pretty good guidance, however, might not be granular enough for day trading given daily movement is often sub 1%.

The model needs to be refined further, and here are what could be done next: 
* For Linear Regression: Introducing similar stocks into the dataset
One could introduce the FANG group (Google/Facebook/Amazon): For each day in the training set, randomly decide if one should pick the data for that day from Apple/Google/... This way, we allow fundamental data to play a bigger role in deciding stock valuation

* For Linear Regression: Tuning parameters in Lasso/Linear/Ridge
Given Lasso has the best outcome followed by Ridge and Linear Regression, we could further testing parameters in Lasso to see if that would improve the MSE

* For all the model tested: Change the target from ‘closing price’ to ‘change in price’ (ie closing price –open). Change input variable from absolute price/value to first derivative ‘change on the day’
This is to solve the first derivative problem instead which could improve granularity.

* Introducing more Option pricing on the stock itself
Option pricing often reflects the stock sentiment.

* Introducing more granular daily information
Rather than just Open price and volume, one could introduce more intra day data points.

* Introducing more technical analysis such as Moving average 
This is to combine some of the concept in ARIMA to ML



