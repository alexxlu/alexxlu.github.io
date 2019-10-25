---
layout: post
title:      "Project 5: Predicting stock price - Ensemble"
date:       2019-10-24 09:18:24 -0400
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

## Static Model
Static Model: 80% training 20% testing

Static Model Train test split:
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images/Set%20initial%20training%3Atesting%20set.png)

Testing Model:
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images/Test%20Stactic%20Model.png)

Try all Models: 
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images/Static%20try%20all%20models.png)

Results: Very strange results!!! makes very little sense why it has 'butterfly wings'! very puzzling
Bagging
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images/Static%20Bagging.png)

Random Forest
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images/Static%20Random%20Forest.png)

Adaboost
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images/Static%20Adaboost%20.png)

Model results Mean Squared Error comparison:
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images/Static%20Model%20Score.png)

## Dynamic Model
Dynamic Model: initial 80% training, 20% testing, and as we predict each of the testing dates at day T, we add previous T-1 actual data back to the training set. As such, the training set grows with time. This makes intuitive sense. If one tries to predict today's stock price, one would use all the information before today to form an opinion.

Dynmaic Initial Train Test Split:
Initiation is the same as static above.

Testing Model:
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images/def%20Dynamic%20Model%20fitting%20.png)

Try all Models:
Same as static above.

Results: Very different! this makes a lot of sense

Bagging
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images/Dynamic%20Bagging%20p1.png)
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images/Dynamic%20Bagging%20p2.png)

Random Forest
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images/Dynamic%20RF%20p1.png)
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images/Dynamic%20RF%20p2.png)

Adaboost
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images/Dynamic%20Adaboost.png)

Model MSE score: Ensemble scores improved by 10 folds!
![](https://raw.githubusercontent.com/alexxlu/Project5/master/Images/Dynamic%20Model%20Score.png)

## Conclusion
Static Model vs Dynamic Model produced very different results for Ensemble methods. Intuitively, Dynamic model outperformance makes sense as one takes in more training data each step of the way. They model could be further fine tuned with parameters. However, I can't explain the 'butterfly wing' effect on the static model. Open to suggestion or if anyone could point out what I am doing wrong.
