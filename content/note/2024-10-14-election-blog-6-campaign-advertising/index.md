---
title: 'Election Blog #6: Campaign Advertising'
author: Shivali Korgaonkar
date: '2024-10-14'
slug: election-blog-6
categories: []
tags: []
---

**Introduction**

With 3 weeks left until Election Day, American citizens are being bombarded by campaign advertisements on their TVs, social medias, and radio stations. In fact, recent reports showcase that a total half a billion dollars will be spent on advertisements by the two campaigns, with Vice President Kamala Harris dominating this spending amount with 63 percent of the total (The New York Times 2024). In the twentieth century, candidates have taken advantage of Americans' media usage to push their policy and personal agenda, which has coined the term "Air War," following the 2008 Election where John McCain ramped up attacks against Barack Obama leading up to election day. While ads sometimes focus on the differences in policy, other times they hit on personal discrepancies. In 1988, for example, George HW Bush called out Micheal Dukakis in the "Tank Ride" ad for being anti-war previously, yet pro-war for the sake of winning the election. This as is often credited as being the defining reason Dukakis' campaign failed (Schulte 2008). The ads are especially focused on the key battle states in an effort to convince them in these crucial next 21 days before Election Day, which can be viewed in the distribution below, detailing the 2012 spending by state. (Digiday 2024). 

In this blog, I will look at election ad spending starting in 2000 to investigate the purpose of these ads, their effect on vote choice, and finally, apply these trends to the 2024 election. 
  



<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-1.png" width="672" />

**Ads and Campaign Spending Over Time*

Before applying ad effects to the 2024 election model, it's important to understand the basic descriptive statistics of spending and content between 2000 and 2012, which emulate contemporary conditions of technology best. To begin, the graph below details the tone (attack, promote, contrast) of campaign ads in the twentieth century. The Democratic and Republican candidates in these four elections generally mimicked the tone of each others ads, meaning the percentage of promotional ads, for example, made up similar percentages in both parties. An important exception to this is in 2004, as the Republican advertisements were attacking over 50 percent of the time, while the Democratic advertisements were attacking about 27 percent of the time. The 2004 election was between John Kerry and the incumbent Geroge W. Bush, and Swift Vets and POWs for Truth had accused Kerry of exaggerating his military service during the Vietnam War, so they ran an extremely effective smear campaign with advertisements against him. Bush ultimately won this election. Though a close race, Bush is the last Republican to have won the popular vote, showcasing the power of the campaigning, as Bush was coming off a term that faced 9/11 aftermath and war in the Middle East. 

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />






Further, the content of campaign ads is also important to understanding political context, party priorities, and issues that matter to voters. I decided to look at data from 2004 and 2012 because they were both election years where Bush and Obama were incumbents running for reelection, respectively. As observed in Week 4, the incumbency effect is a good predictor variable, so observing the 2004 and 2012 descriptive statistics are especially important as Donald Trump is an incumbent, and Kamala Harris comes from the incumbent administration. One clear difference between ad content in 2012 is that the two parties touched on a greater variety of topics at least once, whereas in 2004, the Republican party focused on a much smaller variety than the Democrats. In 2004, the Democrats were generally focused on social issues (civil rights, welfare, child care, etc.), but they had an overwhelmingly emphasis on war and the Middle East, due to the War on Terror begun in Bush's previous administration. Interestingly, the Republicans framed their ads in 2004 as "defense" and 9/11, though this was not the focus of their ads. They focused on gambling, business, family, as well as civil liberty, which persisted as a trend into 2012. There was also many reactionary ads in response to the legalization of gay marriage under Obama's Supreme Court.In 2012, the Democrats continued to focus on war and terrorism, as well as civil rights. Campaign ads seem to focus heavily on current events, as well as issues that a political candidate has specific policy hoping to implement. 

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-6-1.png" width="672" /><img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-6-2.png" width="672" />





**Campaign Spending and Vote Share**

In order to estimate how vote share changes as campaign spending changes, I have run a regression that tracks how much more/less spending the Democratic party put into campaigning by state, as well as how this impacts a one point increase in the two party vote share of the 2008 and 2012 elections. The table below showcases the results of this regression. A few takeaways can be made from this table. To start, when Democrat campaign spending increases, their vote share generally does too. The exception to this is in historically red states, like Arkansas, North Dakota, Idaho, etc., where spending is not statistically significant, and the relationship is also inverse from the general trend.

Most importantly, campaign spending has has a statistically significant effect on vote share in this upcoming election's battleground states in the past two election. With this knowledge, it's crucial that I update my election prediction to include the effects of campaign spending. Unfortunately, I do not have a dataset detailing Harris' and Trump's campaign spending this year, but I can still use trends from 2008 and 2012 to predict this November's outcome. 


Table: <span id="tab:unnamed-chunk-9"></span>Table 1: Effect of Campaign Spending on Democratic Two Party Vote Share

|                            |   Estimate| Std. Error|    t value| Pr(>&#124;t&#124;)|
|:---------------------------|----------:|----------:|----------:|------------------:|
|(Intercept)                 | 37.5829796|   1.516939| 24.7755387|          0.0000000|
|contribution_receipt_amount |  0.0000000|   0.000000|  1.0003549|          0.3187606|
|factor(state)Alaska         |  4.3767716|   2.143360|  2.0420144|          0.0429137|
|factor(state)Arizona        |  9.5482330|   2.147299|  4.4466250|          0.0000169|
|factor(state)Arkansas       | -0.3482745|   2.143087| -0.1625107|          0.8711239|
|factor(state)California     | 22.7715965|   3.995781|  5.6989098|          0.0000001|
|factor(state)Colorado       | 16.2696071|   2.165159|  7.5142787|          0.0000000|
|factor(state)Connecticut    | 21.4508523|   2.158077|  9.9397984|          0.0000000|
|factor(state)Delaware       | 21.7840859|   2.143082| 10.1648401|          0.0000000|
|factor(state)Florida        | 11.5210381|   2.258862|  5.1003723|          0.0000010|
|factor(state)Georgia        |  9.8517025|   2.153792|  4.5741209|          0.0000100|
|factor(state)Hawaii         | 31.6393364|   2.143067| 14.7635806|          0.0000000|
|factor(state)Idaho          | -3.5270264|   2.143322| -1.6455888|          0.1019563|
|factor(state)Illinois       | 21.3866123|   2.257308|  9.4743880|          0.0000000|
|factor(state)Indiana        |  6.5424890|   2.143849|  3.0517483|          0.0026945|
|factor(state)Iowa           | 11.9791964|   2.143086|  5.5896945|          0.0000001|
|factor(state)Kansas         |  3.0277382|   2.143101|  1.4127840|          0.1598047|
|factor(state)Kentucky       |  0.1782500|   2.143082|  0.0831746|          0.9338243|
|factor(state)Louisiana      |  2.8849573|   2.143068|  1.3461808|          0.1802887|
|factor(state)Maine          | 18.0809919|   2.143075|  8.4369375|          0.0000000|
|factor(state)Maryland       | 26.1298886|   2.210126| 11.8228039|          0.0000000|
|factor(state)Massachusetts  | 25.7790679|   2.272577| 11.3435417|          0.0000000|
|factor(state)Michigan       | 15.7586287|   2.152981|  7.3194448|          0.0000000|
|factor(state)Minnesota      | 15.5884158|   2.149809|  7.2510703|          0.0000000|
|factor(state)Mississippi    |  4.9120604|   2.143508|  2.2915985|          0.0233301|
|factor(state)Missouri       |  6.6361866|   2.144823|  3.0940493|          0.0023585|
|factor(state)Montana        |  5.4540793|   2.143328|  2.5446777|          0.0119554|
|factor(state)Nebraska       |  1.8653760|   2.143348|  0.8703096|          0.3855312|
|factor(state)Nevada         | 15.3991829|   2.143233|  7.1850257|          0.0000000|
|factor(state)New Hampshire  | 15.2419739|   2.143142|  7.1119746|          0.0000000|
|factor(state)New Jersey     | 19.9708689|   2.183865|  9.1447351|          0.0000000|
|factor(state)New Mexico     | 18.0482298|   2.144644|  8.4154909|          0.0000000|
|factor(state)New York       | 24.5980509|   2.919853|  8.4244145|          0.0000000|
|factor(state)North Carolina | 11.2436402|   2.156511|  5.2138098|          0.0000006|
|factor(state)North Dakota   | -0.4782581|   2.143911| -0.2230774|          0.8237808|
|factor(state)Ohio           | 11.0201897|   2.152733|  5.1191634|          0.0000009|
|factor(state)Oklahoma       | -4.8185083|   2.143066| -2.2484179|          0.0260168|
|factor(state)Oregon         | 19.4445657|   2.151516|  9.0376108|          0.0000000|
|factor(state)Pennsylvania   | 13.9281854|   2.192645|  6.3522295|          0.0000000|
|factor(state)Rhode Island   | 24.1375827|   2.143082| 11.2630259|          0.0000000|
|factor(state)South Carolina |  6.5136983|   2.143207|  3.0392301|          0.0028021|
|factor(state)South Dakota   |  1.6725368|   2.143760|  0.7801883|          0.4365177|
|factor(state)Tennessee      |  1.4123537|   2.144453|  0.6586079|          0.5111640|
|factor(state)Texas          |  6.2265549|   2.270314|  2.7425961|          0.0068433|
|factor(state)Utah           | -3.2056010|   2.143069| -1.4957994|          0.1368210|
|factor(state)Vermont        | 30.0007175|   2.143073| 13.9989257|          0.0000000|
|factor(state)Virginia       | 15.1297907|   2.200837|  6.8745629|          0.0000000|
|factor(state)Washington     | 20.5637469|   2.214370|  9.2864998|          0.0000000|
|factor(state)West Virginia  | -3.1870160|   2.143472| -1.4868476|          0.1391681|
|factor(state)Wisconsin      | 14.8728339|   2.144667|  6.9348001|          0.0000000|
|factor(state)Wyoming        | -9.0819329|   2.143581| -4.2368041|          0.0000396|

**Updating 2024 Prediction Model**

Using data on advertisement contributions, I have updated my election model. In this model, I use the economy, incumbency, and polls to create the best accurate prediction. I do not use demographics because, as shown in Week 5, they do not accurately predict election results. My new model shows that Trump will win 8 out of the 15 states, which is the first model of this blog to give the Republicans an edge.I was unable to analyze the remaining states as the data was not available, but it would be a surreal achievement for Harris to which all remaining 35 states given my model. Given that this is nearly impossible, my updated model, for once, predicts that Trump will win.






Table: <span id="tab:unnamed-chunk-12"></span>Table 2: Updated Popular Vote State Predictions

|state          | year| simp_pred_dem.fit| simp_pred_dem.lwr| simp_pred_dem.upr| simp_pred_rep.fit| simp_pred_rep.lwr| simp_pred_rep.upr|winner.fit |winner.lwr |winner.upr |stateab | electors|
|:--------------|----:|-----------------:|-----------------:|-----------------:|-----------------:|-----------------:|-----------------:|:----------|:----------|:----------|:-------|--------:|
|Arizona        | 2024|          49.16147|          46.15511|          52.16782|          50.83853|          53.84489|          47.83218|Republican |Republican |Democrat   |AZ      |       11|
|California     | 2024|          64.08198|          60.51960|          67.64436|          35.91802|          39.48040|          32.35564|Democrat   |Democrat   |Democrat   |CA      |       54|
|Florida        | 2024|          47.06571|          43.81323|          50.31819|          52.93429|          56.18677|          49.68181|Republican |Republican |Democrat   |FL      |       30|
|Georgia        | 2024|          49.55999|          46.57547|          52.54450|          50.44001|          53.42453|          47.45550|Republican |Republican |Democrat   |GA      |       16|
|Michigan       | 2024|          50.12646|          47.10218|          53.15074|          49.87354|          52.89782|          46.84926|Democrat   |Republican |Democrat   |MI      |       15|
|Minnesota      | 2024|          52.66064|          49.68421|          55.63706|          47.33936|          50.31579|          44.36294|Democrat   |Republican |Democrat   |MN      |       10|
|Nevada         | 2024|          49.16991|          46.06581|          52.27400|          50.83009|          53.93419|          47.72600|Republican |Republican |Democrat   |NV      |        6|
|New Hampshire  | 2024|          53.62191|          50.64862|          56.59521|          46.37809|          49.35138|          43.40479|Democrat   |Democrat   |Democrat   |NH      |        4|
|North Carolina | 2024|          49.09009|          46.03230|          52.14788|          50.90991|          53.96770|          47.85212|Republican |Republican |Democrat   |NC      |       16|
|Ohio           | 2024|          44.34590|          41.19002|          47.50179|          55.65410|          58.80998|          52.49821|Republican |Republican |Republican |OH      |       17|
|Pennsylvania   | 2024|          49.74610|          46.67562|          52.81658|          50.25390|          53.32438|          47.18342|Republican |Republican |Democrat   |PA      |       19|
|Texas          | 2024|          46.32535|          43.22658|          49.42412|          53.67465|          56.77342|          50.57588|Republican |Republican |Republican |TX      |       40|
|Virginia       | 2024|          53.07380|          50.08165|          56.06595|          46.92620|          49.91835|          43.93405|Democrat   |Democrat   |Democrat   |VA      |       13|
|Wisconsin      | 2024|          50.49243|          47.41185|          53.57301|          49.50757|          52.58815|          46.42699|Democrat   |Republican |Democrat   |WI      |       10|
|New York       | 2024|          52.40015|          48.91375|          55.88654|          47.59985|          51.08625|          44.11346|Democrat   |Republican |Democrat   |NY      |       28|


Table: <span id="tab:unnamed-chunk-13"></span>Table 3: Electoral College Distribution

|winner.fit | States| Electorates|
|:----------|------:|-----------:|
|Democrat   |      7|         134|
|Republican |      8|         155|

**Sources**

https://www.nytimes.com/2024/09/17/us/elections/presidential-campaign-advertising-spending.html

https://digiday.com/media-buying/political-ad-spending-piles-up-in-key-states-less-than-a-month-until-election-day/

https://www.usnews.com/news/articles/2008/01/17/the-photo-op-that-tanked 









