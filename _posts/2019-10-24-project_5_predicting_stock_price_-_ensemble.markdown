---
layout: post
title:      "Project 5: Predicting stock price - Ensemble"
date:       2019-10-24 13:18:23 +0000
permalink:  project_5_predicting_stock_price_-_ensemble
---

## Introduction
In project 5, I am trying to predict closing stock price based on past 5 years of data and 11 variables. As an example, I have picked Apple stock for the project. The 11 variables can be described in 3 categories: 
1) Technical data: Open Price, Last Price, Volume.
2) Fundamental data: Financial Leverage, PE RATIO, Cash Flow per Share, Price to Book Ratio, Dividend Per Share. 
3) Macro data: SPX, VIX, PPUT. (Note: VIX - volatility index; PPUT - put option price for S&P; SPX - S&P price.)

Among many models I have tried DL/Linear/Ensemble/PCA, one strange result came out of Ensemble (Bagging/Random Forest, and Adaboost). I thought to share the method, result and open to any suggestion.

## Dataset
1380 days worth of data.  shape: 1380x11
y= Last Price
x={Open Price, Last Price, Volume, Financial Leverage, PE RATIO, Cash Flow per Share, Price to Book Ratio, Dividend Per Share, SPX, VIX, PPUT}

This is what raw data looks like:
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images/data%20head().png)

Data summary:
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images/data%20describe().png)








