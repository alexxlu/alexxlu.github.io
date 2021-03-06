---
layout: post
title:      "Project 2 "
date:       2019-04-17 10:53:26 -0400
permalink:  testing_testing_testing
---

### Question 1: Do discounts have a statistically significant effect on the number of products customers order? If so, at what level(s) of discount?

**Step 0: inspect the sql contents and see if the tables names are as expected from the ERD diagram.**

It seems the ERD diagram is different from the actual sql extraction: 1)Employee vs Employees 2)EmployeeTerritory vs EmployeeTerritories ... it seems all the tables are singlar vs plural in the ERD table

![Northwind ERD](https://raw.githubusercontent.com/alexxlu/dsc-2-final-project-online-ds-pt-100118/master/Northwind_ERD.png)

**Step 1: construct Hypothesis:**

Null Hypothesis (H0): Discount has no statistical significant relationship to number of products customer orders. mu_fp=mu_disc (mu_fp is the mean of full price quantity. mu_disc is the mean of discount quantity.) 

Alternative(H-alpha): Discount has a statistically significant impact to the number of products customer orders. Alpha is set to 0.05. mu_fp!=mu_disc

**Step 2:**
- **extracts relevant data to form a data frame**
- **seperate the dataset into two sets (one with discount, and one without discount)**
- **visualize the two datasets**

```
#OrderDetail table has all the revelant data we need (Discount and Quanity)
df_OD=pd.read_sql_query("select * from OrderDetail", engine)

#data set where there is no discount or full price (fp), or control
df_fp=pd.read_sql_query("select * from OrderDetail where Discount=0", engine)
df_disc=pd.read_sql_query("select * from OrderDetail where Discount!=0", engine)

```

![Visualizing the datasets](https://raw.githubusercontent.com/alexxlu/dsc-2-final-project-online-ds-pt-100118/master/Q1graph.png)


**Step 3: calculating p-value with T-Test function**
```
#Calculating p-value with inbuilt T-test function
stats.ttest_ind(df_disc.Quantity, df_fp.Quantity)
Ttest_indResult(statistic=6.4785631962949015, pvalue=1.1440924523215966e-10)
```


**As pvalue is smaller than alpha, we reject hypothesis, but how significant is the difference? We'll further perform Cohen-D test**
```
def Cohen_d(sample1, sample2):
    diff=sample1.mean()-sample2.mean()
    n1,n2=len(sample1), len(sample2)
    var1, var2=sample1.var(), sample2.var()
    pooled_var=(n1*var1+n2*var2)/(n1+n2)
    d=diff/np.sqrt(pooled_var)
    return d
Cohen_d(df_disc.Quantity, df_fp.Quantity)
0.2862724481729283
```


**Step 4: Tukey test to see which discount value is most effective**

![Tukey Test](https://raw.githubusercontent.com/alexxlu/dsc-2-final-project-online-ds-pt-100118/master/Q1%20Tukey.png)

**Step 5: Conclusion and Interpretation of the Results**

1) p-value=1.1e-10
p< alpha: reject null hypothesis. there is a statistical significance between discount and quantity purchase

2) Cohen D test =0.286 
Cohen d value seems to suggest that there is a small to medium effect difference.

3) Tukey Test
From the Tukey test,  only 5%, 15%, 20% and 25% are significant. among those, the mean difference in 15% is the greatest, so it is saying that 15% makes the biggest difference, however it is marginal. 

4) Business implication
If the company's KPI is to sell as much quantity as possible, then they should certainly apply discount promotion, and 15% seems to be the most effective. However without knowing the net profit margin after discount (or amount of mark up before discount), it is difficult to make a recommendation to what discount should be applied. The company should further investigate what % discount would have the greatest effect and yet bring in the highest net profit.

