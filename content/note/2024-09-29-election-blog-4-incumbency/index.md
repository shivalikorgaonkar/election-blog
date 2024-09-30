---
title: 'Election Blog #4: Incumbency'
author: "Shivali Korgaonkar"
date: "2024-09-29"
output: pdf_document
categories: []
tags: []
slug: "election-blog-4-incumbency"
---

**Introduction**

The 2024 Election holds a unique duel, being that it is between an incumbent president and a candidate from the incumbent administration. Many presidential models have special considerations when making election predictions based on incumbency adjustment. There are both advantages and disadvantages to incumbency. Generally, incumbents have an advantage when they have more media coverage (name recognition), campaign finance access, or "pork" (short term economic gains and credit-claiming). On the other hand, incumbents may be disadvantaged when there is a polarized electorate, recessions/disasters, or incumbency fatigue. 

In the context of this election, there are a few indicators that may impact the results relative to the candidates' respective incumbencies. For starters, Trump benefits for the name recognition and media attention, as well as the financial backing from wealthy donors that support his tax break causes. On the other hand, he has been criminally convicted in the last year, and left his presidency following the January 6th riots, which left many Republicans distasteful of having him in power. Harris comes from the incumbent party and also picked up the campaign while Biden had already begun. Since she entered the race before the Democratic party elected a nominee, she has access to all of Biden's remaining campaign funds, since he never officially won the nomination. 






**Historical Context to Incumbency Advantage**

Using data from all elections following World War II, we can look at how incumbent presidents and incumbent parties have performed in the past. There have been 18 elections in the time period, and the table below shows that six incumbent presidents won in these elections. 11 of these elections had an incumbent candidate running. Thus, 6 out of 11 incumbent presidents that have run for re-election, have won. In the 21st century, there have been three incumbents that ran (2004, 2012, and 2020), and two of them were successful. 


|President Re-Elected? | Number of Elections| Percent|
|:---------------------|-------------------:|-------:|
|Defeated              |                  12|   66.67|
|Re-Elected            |                   6|   33.33|

The table below indicates that the incumbent party has won 8 out of the 18 elections post-WWII. There seems to be a difference between an incumbent party and incumbent candidate running. One possible explanation could be that voters have party fatigue, meaning there has been too much of the same ideology, so either they are less motivated to vote without the dire need. Pew Research Center also reported in 2023 that only four percent of American adults believe their government is working extremely well or very well. With this in mind, any existing crises in the US are more likely to be blamed on the incumbent President who, by association, passes the blame into the hands of their successor. The party successor also doesn't benefit from the name recognition that an incumbent candidate has, so it makes sense that their campaigning process is more difficult. 

For party successors, those who served in the previous administration have won 27.8 percent of the past 18 elections. This point applies to Kamala Harris, who formerly served in President Joe Biden's administration as Vice President.


|Party Re-Elected? | Number of Elections| Percent|
|:-----------------|-------------------:|-------:|
|Defeated          |                  10|   55.56|
|Re-Elected        |                   8|   44.44|

**Pork Barrel Politics**

Another distinction between incumbent parties and candidates falls in spending. Congress is infamously known for having the "power of the purse," but the President has the power of proposal, which they strategically allocate before an election. Interestingly, the graph below shows that incumbent presidents spend most on swing states when they are running for re-election. The spend about the same amount (~ $145M) on swing states during non-election years and on swing states when their successor is running for election.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-5-1.png" width="672" /><img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-5-2.png" width="672" />

A multivariate regression was run to further analyze the relationship between federal grant spending and an incumbent's vote share in swing states. Additional independent variables were added to strengthen the regression, including media appearances, change in per capita income, change in population, and more. The regression identifies a statistically significant positive correlation between grant spending in competitive states and the incumbent's vote share in these states. When running state-level regression, it is also apparent that in 1996 and 2004, Bush's and Clinton's re-election campaign respectively, there was a greater amount of pork barrel spending than normal.







**Using Incumbency Advantage to Predict the Election**

Alan Abramowitz is a political scientist that uses incumbency advantage to predict election outcomes. His Time For Change model, which is his original model used to predict the 2016 race, also incorporates GDP and approval rating, alongside incumbency. I built a predictive model using Abramowitz's formula, and found that Harris was predicted to have 48.9 percent of the popular vote. 

Abramowitz also has a simplified model that he created in 2020 which only utilizes the June approval rating to predict the election. This Simplified Time for Change model predicts that Harris will win 47.4 percent of the popular vote.





|Prediction Models                | Predicted 2024 Vote Share| Lower Bound| Upper Bound|
|:--------------------------------|-------------------------:|-----------:|-----------:|
|Time for Change Model            |                  48.92874|    43.09807|    54.75942|
|Simplified Time for Change Model |                  47.39554|    40.52536|    54.26573|

**Looking Back at My Model**

In the spirit of simplified models, I will call back to my predictive model from Blog 1, which used the popular vote share from 2016 and 2020 (vote_2024 = 3/4vote_2020 + 1/4vote_2016) to predict this election. Under this model, I predicted that the Democrats would receive 49.28 percent of the vote, and Republicans would receive 50.72 percent of the vote. However, upon reducing this to the state level, my model did predict that Harris would win the electoral college with 272 electors.

Abramowitz has a much more basic model compared to other political scientists and organizations we've looked at, like FiveThirty Eight. My own model points out two issues with his model. First, his model is ineffective at predicting state level outcomes. Notably, however, it has generally done well in predicting national outcomes. Adding on, the ineffective state level prediction leaves the electoral college outcome unknown. This is significant, as many elections have defied the outcome shown by popular vote. In the future, it would be useful to have the Time for Change model improve its state level estimations.
         
**Sources** 

https://slcc.pressbooks.pub/attenuateddemocracy/chapter/chapter-55/

https://hls.harvard.edu/today/can-kamala-harris-access-biden-campaign-funds/ 
                             
https://www.pewresearch.org/politics/2023/09/19/americans-dismal-views-of-the-nations-politics/ 
                             
                             
