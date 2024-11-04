---
title: 'Election Blog 8: Updated Prediction'
author: Shivali Korgaonkar
date: '2024-10-27'
slug: final-election-predictions
categories: []
tags: []
---

**Introduction**

As ballots begin to roll in, tension and excitement around the election are building. Donald Trump hosted a rally at Madison Square Garden with numerous speakers, building the MAGA spirit in a classic, controversial fashion. Kamala Harris has begun her final week campaigning with Barack Obama at her right hand. Polls continue to conflict, but one key factor remains: this election will be very tight.

In this final prediction blog, I will be editing my prediction model to be cohesive and thorough, based on the lessons I have learned over the past 8 weeks in this course. As a class, we have looked at different election indicators, including the economy, demographics, shocks, campaigning, and more. My final model will include some of these indicators that I deemed to be predictive of this election, and excluded others that I have previously calculated to be statistically insignificant. By doing this, I hope to curate the best prediction possible, especially in the swing states of this election, which are Arizona, Georgia, Michigan, Nevada, North Carolina, Pennsylvania, and Wisconsin.
  


**Analyzing State Party Preferences**

The map below lays out the party alignment of the states, based on how they voted in 2020. The identified Swing States are established through multiple sources, cited at the bottom of this blog. Assuming these state preferences continue, the current electoral college votes establish **226 votes for Kamala Harris and 219 votes for Donald Trump.** This leaves **93 votes up in the air from the swing states**.



<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />

**Updating My Prediction Model**

My prediction model is based on Alan Abramowitz's "Time for Change" model, which was extremely accurate in predicting the 2016 election. However, I expand into a few more variables, while also trying to avoid over-fitting. The variables I used, specifically, are historic two party vote share, latest polling averages, economic indicators (GDP, RDPI, unemployment), June approval rating, and incumbency.

I used a few different methods to try to create an accurate model. For starters, I used lagged vote share to enhance predictive power and better account for historic trends. I also used a Lasso regression, because Lasso simplifies model interpretation and enhances focus on the most important predictors. It handles multicollinearity well, which has more stable estimates and  predictive accuracy. Finally, after running this regression, I accounting for the weighted error to update my prediction.










|state          | D_pv2p_adjusted|Winner   |
|:--------------|---------------:|:--------|
|Arizona        |        56.78800|Democrat |
|Georgia        |        56.61543|Democrat |
|Michigan       |        58.16681|Democrat |
|Nevada         |        58.41200|Democrat |
|North Carolina |        56.98920|Democrat |
|Pennsylvania   |        57.93788|Democrat |
|Wisconsin      |        58.68235|Democrat |



The updated map below estimates how states will vote in the 2024 election, according to my model. Currently, it appears that all the swing states will turn blue.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-9-1.png" width="672" />

As you can see below, my prediction model this week shows that Kamala Harris will defeat Donald Trump by a landslide. Since this is highly unprobable, I will devote the next section to areas where my prediction can be improved for the final model next week.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-10-1.png" width="672" />

**Improvements for Next Week**

I am definitely not confident in my current model, despite the fact that I believe I used all the predictive indicators that I have found significant over the past 8 weeks. There are a few things that I would like to correct over the next week before Election Day arrives. For one, I would like to run the same regression on a state-level, as opposed to the national level. Additionally, I would like to review the variables we've discussed, including campaign spending, field offices, demographics, etc. On the other hand, I may have used too many variables, in which case I will simplify my model further to avoid over-fitting. 

**Sources**

https://www.nytimes.com/2024/10/28/us/politics/trump-msg-rally-speaker-remarks.html

https://centerforpolitics.org/crystalball/2024-president/ 

https://www.ibm.com/topics/lasso-regression#:~:text=Lasso%20regression%20is%20a%20regularization,regularization%20for%20linear%20regression%20models.
