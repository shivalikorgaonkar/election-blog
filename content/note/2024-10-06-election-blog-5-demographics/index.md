---
title: 'Election Blog #5: Demographics'
author: Shivali Korgaonkar
date: '2024-10-06'
slug: election-blog-5-demographics
categories: []
tags: []
---

**Introduction**

There are many stereotypes surrounding voter demographics and how they can predict presidential candidate support. Whether it be sexuality, occupation, or immigration status, Americans often mentally associate different identities with different parties. In an attempt to break these stereotypes, we've seen groups like "Gays for Trump," which attempt to break oxymoronic identity alignments. We've also seen backlash to such beliefs among communities who believe that their specific needs won't get represented properly. 

In this blog, I attempt to identify how demographic affects voter turnout, and I use this information to create an election prediction model.







**Demographics and Vote Choice**

Using American National Voter File (ANES) data that was cleaned up by Matthew Dardet, we can begin investigating the relationship between voter demographic and their vote choice, and replicate Kim & Zilinsky's (2023) research. Using a logistic regression, a training dataset and testing data set were created. A training dataset teaches the model by allowing it to learn patterns and relationships from the given ANES data. A testing dataset is used to evaluate the model's performance on new, unseen data to ensure that it can generalize well beyond the training data. The summary displaying in-sample goodness of fit highlights an important conclusion that **gender, race, education, religion, and geography are the most significant indicators.**



```
## 
## Call:
## glm(formula = pres_vote ~ ., family = "binomial", data = anes_train)
## 
## Coefficients: (1 not defined because of singularities)
##                 Estimate Std. Error z value Pr(>|z|)    
## (Intercept)    4.3583814  0.4366803   9.981  < 2e-16 ***
## age            0.0006984  0.0028117   0.248  0.80383    
## gender        -0.4294732  0.0934585  -4.595 4.32e-06 ***
## race          -0.5482380  0.0605982  -9.047  < 2e-16 ***
## educ          -0.3398141  0.0613322  -5.541 3.02e-08 ***
## income         0.0494349  0.0468039   1.056  0.29087    
## religion      -0.2148136  0.0421012  -5.102 3.36e-07 ***
## attend_church -0.2109916  0.0331518  -6.364 1.96e-10 ***
## southern      -0.4096051  0.1051603  -3.895 9.82e-05 ***
## region                NA         NA      NA       NA    
## work_status    0.0955178  0.0458378   2.084  0.03718 *  
## homeowner     -0.1765531  0.0822755  -2.146  0.03188 *  
## married       -0.0715981  0.0276917  -2.586  0.00972 ** 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## (Dispersion parameter for binomial family taken to be 1)
## 
##     Null deviance: 2890.2  on 2087  degrees of freedom
## Residual deviance: 2564.3  on 2076  degrees of freedom
## AIC: 2588.3
## 
## Number of Fisher Scoring iterations: 4
```

When measuring the accuracy of this machine learning model, we can use a Confusion Matrix to examine how the testing dataset performed. In both the in-sample and out-of-sample accuracy measures, there was a 67 percent accuracy. The number of trues positives and false negatives can be seen below. 











**Demographics and Voter Turnout**

Since we do not have demographic data or vote choice available for the 2024 election, we cannot build a regression model for 2024. However, we can observe if there is a difference in how demographics play a role in blue states, red states, and swing states. To do this, I've created distribution models for different demographic indicators. I singled out three states' voterfile data, in order to specifically visualize party alignment and voter turnout based on demographic. I choose Wyoming as a representation of a red state, Vermont as a representation of a blue state, and Arizona as a representation of swing state, due to its particular importance in the 2024 election.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-9-1.png" width="672" />

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-10-1.png" width="672" />


<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-11-1.png" width="672" />


<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-12-1.png" width="672" />

The following trends are noticeable from this distribution charts:

*Women have a higher voter turnout rate.

*The age group with the highest voter turnout is 60+ year olds.

*Race as an indicator has the greatest voter turnout variation between the three states analyzed.

*Voters that went to grad school have a higher turnout rate; vocatational workers in VT are the only subgroup that closely compare.

A more formal regression was run to verify that **most demographic variables and turnout are not significant for Democrats, but they are for Republicans.** However, it is significant to look at polling at 2 party vote share in order to predict the 2024 outcome.






**2024 Election Model**

Using the simple average of voter turnout and relevant demographic variables, the data below summarizes how each party would perform among the 15 swing states. The table shows that the significant indicators give Kamala Harris an edge in winning the presidential election. When using a 95% confidence interval, though, it becomes evident that the results are not as black and white as this makes it seem.

For my final model, I now know the importance of voter turnout for either party. Looking back at Week 1, I could combine these effects with fundamental economic factors to have a more accurate model to predict the outcome of the 2024 election results.


|Winner     | States| Electoral Votes|
|:----------|------:|---------------:|
|Democrat   |     12|             202|
|Republican |      3|              87|

**Sources**

https://electionstudies.org/data-center/

https://www.usnews.com/news/elections/articles/7-swing-states-that-could-decide-the-2024-presidential-election
