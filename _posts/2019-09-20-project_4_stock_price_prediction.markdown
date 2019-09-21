---
layout: post
title:      "Project 4: Stock price prediction"
date:       2019-09-20 10:33:08 -0400
permalink:  project_4_stock_price_prediction
---


**Problem**: Prediction today's stock price based on past 7 days performance: High, low, open, close and volume.
In this project, I have picked Apple stock as an example, as it is a liquid stock with a good trading volume.

**Data**: Data was taken from Kaggle S&P500 dataset.

Raw Data at first glance:
![](https://raw.githubusercontent.com/alexxlu/Project4/master/Pictures/Raw%20data%20preview.png)

Reformat the data: set date as index and shifting the columes preparing for modeling later on
![](https://raw.githubusercontent.com/alexxlu/Project4/master/Pictures/Reformat%20the%20raw%20data.png)

Take a look a the data for sanity check:
![](https://raw.githubusercontent.com/alexxlu/Project4/master/Pictures/Graph%20raw%20data.png)

This is a very clean dataset. The graphs on the first glance passes common sense test.

To solve the problem at hand, I chose LSTM model here for the following reasons: 
1) Stock price is a sequential problem. Previous days price actions give a good indication of market supply and demand.
2) LSTM is used for solve longer time lag, and it is often used for time series applicatioin.

In this project, I chose 7 day as the lag time for prediction. Depending on style of trading (high frequency, medium or low frequency), numbere of the day lag should be adjust according along with a human judgement call. 

There are 5 input variables on any given day: high, low, open, close and volume price. Over 7 days, there are 35 input variables to the model. After bringing all data to 0 to 1 scale metrics, re-produce the dataset for modeling, this is what it looks like:
![](https://raw.githubusercontent.com/alexxlu/Project4/master/Pictures/Dependent%20variables.png)

**Models:**
Model 1:
I started with a simple model: 1x LSTM layer with 20 nodes and 1x Dense layer. 
![](https://raw.githubusercontent.com/alexxlu/Project4/master/Pictures/Model%201%20code%20and%20summary.png)
To my surprise, the Mean Squred Error (MSE) is very low, and good convergence on training set loss value.
![](https://raw.githubusercontent.com/alexxlu/Project4/master/Pictures/Model1%20loss%20graph%20and%20MSE.png)
Bringing prediction value from 0 to 1 scale back to its original $/share stock price, and compare last 120days actual price, we get a very good looking graph suggesting that the model 1 does a very decent job.
![](https://raw.githubusercontent.com/alexxlu/Project4/master/Pictures/Model%201%20actual%20vs%20pred.png)

Model 2:
Adding a bit more complexity:

1x Lstm 50 nodes
1x Dense layer with relu activation
1x Dense layer with linear activation

![](https://raw.githubusercontent.com/alexxlu/Project4/master/Pictures/Model%202%20code%20and%20summary.png)

Disappointingly, MSE result is very high.
![](https://raw.githubusercontent.com/alexxlu/Project4/master/Pictures/Model%202%20loss%20graph%20and%20MSE.png)

Plotting the predicted value vs actual test set value, it is pretty bad - there seems to be a consistent downward bias in the model.
![](https://raw.githubusercontent.com/alexxlu/Project4/master/Pictures/Model%202%20actual%20vs%20predict.png)

Could 'relu activation' be the problem here given we are solving a linear problem rather than categorization problem?
I decided to try the exact same model with linear activation.

Model 3:

Same as Model 2 except activation linear. The result is better than model 2, which suggests that 'linear' activation is more approporiate than 'relu' in this case. It is also interesting to see that it still shows a downard bias, same as Model 2.

![](https://raw.githubusercontent.com/alexxlu/Project4/master/Pictures/Model%203%20code%20and%20summary.png)

![](https://raw.githubusercontent.com/alexxlu/Project4/master/Pictures/Model%203%20%20loss%20and%20mse.png)


![](https://raw.githubusercontent.com/alexxlu/Project4/master/Pictures/Model%203%20actual%20vs%20pred.png)

Model 4:

I decided to try a even more complicated model. Instead of guessing how many nodes to have, I ran through a loop testing 30 nodes, 40 nodes and 50 nodes for Model 4. It turned out that on average lower number nodes results are better, which is consistent with our findings so far with this case - simplicity is a beauty.

![](https://raw.githubusercontent.com/alexxlu/Project4/master/Pictures/Model%204%20code.png)

Without displaying each one of the result, the MSE results ranged from 20 to 200. 

**Conclusion**

The best model in this case is the simplest model with one LSTM layer and one Dense layer, with consistent MSE around 9 to 12. To translate this MSE number into something tangible: this is saying that the price deviation between true and predicted is aroudn +/-3 to +/-3.5. Given the stock price started in $60s/share and went up to $185/share, a $3 deviation is a 1.5% to 5% deviation from the price, which is quite good. 

In addtion, It is worth point out that the model has a undervalue (predict < actual)  tendency in the bull market, and overvalues vs actual when the market is selling off. 

To be clear, the model is a good guidance in a normal market trading environment. The model is not suitable for prediction in unprecedented major event, such as Asian crisis, 9/11 or financial crisis 2007. When trading with this model, stop loss trigger should be implemented, especially in a bearish market. 


