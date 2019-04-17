---
layout: post
title:      "testing testing testing "
date:       2019-04-17 14:53:25 +0000
permalink:  testing_testing_testing
---

***Step 2: 
- extracts relevant data to form a data frame
- seperate the dataset into two sets (one with discount, and one without discount)
- visualize the two datasets***

#OrderDetail table has all the revelant data we need (Discount and Quanity)
df_OD=pd.read_sql_query("select * from OrderDetail", engine)

#data set where there is no discount or full price (fp), or control
df_fp=pd.read_sql_query("select * from OrderDetail where Discount=0", engine)
df_disc=pd.read_sql_query("select * from OrderDetail where Discount!=0", engine)



![Visualizing the datasets](https://raw.githubusercontent.com/alexxlu/dsc-2-final-project-online-ds-pt-100118/master/Q1graph.png)



**Step 3: calculating p-value with T-Test function**
# testing

The content of your blog post goes here.
