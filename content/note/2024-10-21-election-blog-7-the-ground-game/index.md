---
title: 'Election Blog #7: The Ground Game'
author: Shivali Korgaonkar
date: '2024-10-20'
slug: election-blog-7-the-ground-game
categories: []
tags: []
---

**Introduction**

Last week, we investigated the impact of campaign advertisements. This week, we will look at campaign events as a strategy for candidates. The 2024 election has been extraordinary in many ways, but one of the most jarring moments traces back to a campaign event from this summer, when Donald Trump survived an assassination attempt. In-person events have a powerful effect on voters, as they carry contagious energy and rally supporters who unite in their excitement over a candidate. They also allow voters to see the way candidates deal speak to an audience and dominate a space. Oftentimes, the bigger rallies lead to an opportunity for candidates to visit local restaurants or meet with different communities. Earlier today, in fact, Trump put in a shift at a McDonald's in Pennsylvania. Joe Biden was often seen at ice cream shops across the country. And, most importantly, a candidate's greatest test was witnessed in their interactions with babies passed to them in rallies.

In this blog, we will investigate historical data on the Ground Game, as well as how it can be used to predict voter turnout this year.





**Binomial Simulations and Probabilistic Models**

The first two visualizations this week track the relationship between poll support and hypothetical vote share in state-level polls between 1948 and 2020. The second visual looks specifically and California and Florida, for an easier viewing at the trends that can be found in linear regression models.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" />
There are a few issues that can be seen from a linear regression model in the context of polling and vote share. For one, these graphs visualize a vote share prediction that exceeds 0%-100%, which is an impossible reality. For example, if a candidate in Florida was able to reach 90% support in the polls, they would be expected to win over 100% of the vote. Additionally, both Nevada and Mississippi have counter-intuitive data displayed, as the former has extremely high variance, and the latter displays a negative slope.

In order to address some of these issues in the linear regression model, it could be useful to see how a logistic regression model interprets the same correlation. Immediately, it is clear that the y-axis fits a more realistic trend with bounds between 0% and 100%, matching an actual election.




<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-6-1.png" width="672" />


```r
state_glm_forecast_outputs |>
  filter(state_abb == "CA" | state_abb == "FL") |>
  ggplot(aes(x=x, y=y, ymin=ymin, ymax=ymax)) + 
  facet_wrap(~ state_abb) +
  geom_line(aes(color = party)) + 
  geom_ribbon(aes(fill = party), alpha=0.5, color=NA) +
  coord_cartesian(ylim=c(0, 100)) +
  geom_text(data = d |> filter(state_abb == "CA", party=="DEM"), 
            aes(x = poll_support, y = D_pv, ymin = D_pv, ymax = D_pv, color = party, label = year), size=1.5) +
  geom_text(data = d |> filter(state_abb == "CA", party=="REP"), 
            aes(x = poll_support, y = D_pv, ymin = D_pv, ymax = D_pv, color = party, label = year), size=1.5) +
  geom_text(data = d |> filter(state_abb == "FL", party=="DEM"), 
            aes(x = poll_support, y = D_pv, ymin = D_pv, ymax = D_pv, color = party, label = year), size=1.5) +
  geom_text(data = d |> filter(state_abb == "FL", party=="REP"), 
            aes(x = poll_support, y = D_pv, ymin = D_pv, ymax = D_pv, color = party, label = year), size=1.5) +
  scale_color_manual(values = c("blue", "red")) +
  scale_fill_manual(values = c("blue", "red")) +
  xlab("Hypothetical Poll Support") +
  ylab('Probability of\nState-Eligible Voter\nVoting for Party') +
  ggtitle("Binomial Logit") + 
  theme_bw() + 
  theme(axis.title.y = element_text(size=6.5))
```

```
## Warning in geom_text(data = filter(d, state_abb == "CA", party == "DEM"), :
## Ignoring unknown aesthetics: ymin and ymax
```

```
## Warning in geom_text(data = filter(d, state_abb == "CA", party == "REP"), :
## Ignoring unknown aesthetics: ymin and ymax
```

```
## Warning in geom_text(data = filter(d, state_abb == "FL", party == "DEM"), :
## Ignoring unknown aesthetics: ymin and ymax
```

```
## Warning in geom_text(data = filter(d, state_abb == "FL", party == "REP"), :
## Ignoring unknown aesthetics: ymin and ymax
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-1.png" width="672" />
The binomial logistic regression is a non-linear relationship, so we can see that many of the data points don't have a line drawn through them, as seen in th elinear regression. However, a ogistic regression is typically used when the outcome is binary. Since we want to see vote share, though, we can think of each percentage point as a probability of winning a certain share of votes, which works better with the binomial logistic regression framework better.

**Field Offices**

Every campaign has field offices scattered throughout the country to ensure that specific states are receiving enough attention. Campaigns obviously have a strategy as to where they want these field offices to be placed, so it's helpful to look at past data and detect trends. 

The table below displays information from the 2012 election between Barack Obama and Mitt Romney. This regression highlights a few variables as statistically significant in influencing the placement of field offices. For one, there are more field offices from one candidate in counties where the other candidate is situated, too. Also, if the county was a core republican state, for example, Obama was less likely to place a field office there, and vice versa for democrats. Interestingly, Obama placed more field offices in battle states, but Romney did not.


```
## 
## Placement of Field Offices (2012)
## =======================================================
##                             Dependent variable:        
##                     -----------------------------------
##                         obama12fo        romney12fo    
##                            (1)               (2)       
## -------------------------------------------------------
## romney12fo          2.546*** (0.114)                   
## obama12fo                             0.374*** (0.020) 
## swing                 0.001 (0.055)    -0.012 (0.011)  
## core_rep              0.007 (0.061)                    
## core_dem                                0.004 (0.027)  
## battle              0.541*** (0.096)    0.014 (0.042)  
## medage08                                               
## romney12fo:swing    -0.765*** (0.116)                  
## romney12fo:core_rep -1.875*** (0.131)                  
## obama12fo:swing                       -0.081*** (0.020)
## obama12fo:core_dem                    -0.164*** (0.023)
## Constant             -0.340* (0.196)    0.001 (0.079)  
## =======================================================
## =======================================================
```
Further, it's important to look at the impact these field offices have on voter turnout and vote choice. The chart below explains that democrats had a statistically significant increase in both turnout and vote share in battle states with field offices. 


```
## 
## Effect of DEM Field Offices on Turnout and DEM Vote Share (2004-2012)
## =========================================================
##                                Dependent variable:       
##                         ---------------------------------
##                          turnout_change   dempct_change  
##                               (1)              (2)       
## ---------------------------------------------------------
## dummy_fo_change         0.004*** (0.001) 0.009*** (0.002)
## battle                  0.024*** (0.002) 0.043*** (0.003)
## as.factor(state)Arizona                                  
## dummy_fo_change:battle   -0.002 (0.002)  0.007** (0.003) 
## Constant                0.029*** (0.002) 0.022*** (0.003)
## ---------------------------------------------------------
## Observations                 6,224            6,224      
## Adjusted R2                  0.419            0.469      
## =========================================================
## Note:                         *p<0.1; **p<0.05; ***p<0.01
```
**Campaign Events**

The timeline of candidates hosting events has varied between the 2016, 2020, and 2024 elections. More generally, events shoot up in frequency as Election Day approaches, which can be seen in the 2016 and 2020 elections. This is useful in predicting that this year, a similar spike will occur in the next two weeks. Republicans have a more consistent exponential trajectory from August to November. Democrats have sharp upward/downward curves around September, which is hard to explain. Perhaps they spend October focusing on other aspects of campaigning besides events. 

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-10-1.png" width="672" />

**Campaign Events vs Campaign Ads**

With all the time and money put into campaign events, it's crucial to recognize the impact they have on a candidate's state level vote share. The table below shows that events have a statistically significant impact on vote share. For democrats, events boost their vote share, while for republicans, they reduce their vote share. 


```
## 
## Association Between Campaign Events and Voting Outcomes of Interest
## ============================================================
##                                     Dependent variable:     
##                                -----------------------------
##                                Dem Vote Share Rep Vote Share
##                                     (1)            (2)      
## ------------------------------------------------------------
## Dem Events                        0.126***                  
##                                   (0.034)                   
##                                                             
## D - R Event Diff                   0.105                    
##                                   (0.067)                   
##                                                             
## Rep Events                                      -0.126***   
##                                                  (0.034)    
##                                                             
## R - D Event Diff                                 0.230***   
##                                                  (0.078)    
##                                                             
## Constant                         48.189***      51.810***   
##                                   (0.369)        (0.369)    
##                                                             
## ------------------------------------------------------------
## Observations                        714            714      
## R2                                 0.021          0.021     
## Adjusted R2                        0.019          0.019     
## Residual Std. Error (df = 711)     7.508          7.509     
## F Statistic (df = 2; 711)         7.778***       7.776***   
## ============================================================
## Note:                            *p<0.1; **p<0.05; ***p<0.01
```

Looking back to last week's model, we can compare the effects of campaign events versus advertisements and decide which initiative is more effective and worth investing in. If I were a campaign manager for Harris, based on the past two weeks' findings, I would throw the most funding into in-person events in swing states. This would ensure that vote share increases in contentious places where the election will likely end up being reliant on in November.

**Sources**

https://www.foxnews.com/politics/trump-makes-fries-pennsylvania-mcdonalds-ive-now-worked-15-minutes-more-than-kamala

https://ash.harvard.edu/articles/the-real-numbers-tracking-crowd-sizes-at-presidential-rallies/
