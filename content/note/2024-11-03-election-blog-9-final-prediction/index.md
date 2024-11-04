---
title: 'Election Blog #9: Final Prediction'
author: Shivali Korgaonkar
date: '2024-11-03'
slug: election-blog-9-final-prediction
categories: []
tags: []
---

**Opening Remarks**

T-2 days until Election Day. It's been an absolutely crazy few months, and I can't believe the culmination of all the candidates' campaigning is coming to a close. This election result is so important, but my biggest hope is that voters turn out so different communities are represented. Tracking the election and its different variables has been unbelievably insightful, and I'm sad this blog will be coming to an end with this blog serving as the final cap. I want to take time to thank Professor Enos and Matthew Dardet for leading an incredible class this semester. Their guidance and instruction has been instrumental to this blog. 

**Introducing The Last Blog**

My model predicts the outcome of the seven swing states identified: Arizona, Georgia, Michigan, Nevada, North Carolina, Pennsylvania, and Wisconsin. The remaining states are assumed to align in the same outcome as the 2020 election. Assuming these preferences continue, the current electoral college votes establish **226 votes for Kamala Harris and 219 votes for Donald Trump.** This leaves **93 votes up in the air from the swing states**.







<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />






**My Final Election Model**

My model is a culmination of previous' weeks findings of important election indicators. Based on fears around over-fitting, I've decided to emphasize simplicity in the number of variables I use, as exemplified by Alan Abramowitz’s “Time for Change” model. My final model will contain the variables below: democratic two-party lagged vote share, latest and mean polling averages, second quarter GDP, unemployment, and incumbency. In Week 3, I found that GDP in the second quarter was the best economic indicator. Unemployment was also important, though, especially due to its negative correlation to incumbency, which I've included. Since last week, I've removed June approval rating because President Biden was still in office at this point, so I don't think this is representative of Harris' approval. However, I've maintained the incumbency effect because Harris served under President Biden so she has an immediate history in office. The other change from last week is that I have updated polling data. I considered adding in new variables, such as campaign spending and field offices, but, as discussed in Week 7, the campaigns generally cancel each other out, so it would be unhelpful.

I've decided to stick with a LASSO regression for prediction in my model. LASSO puts more emphasis on variables with greater impact, in order to reduce the likelihood of over-fitting, which is something to be cautious of with election predictions, since so much changes every 4 years. I also used lagged vote share to enhance predictive power and better account for historic trends. Finally, after running the regression, I accounting for the weighted error to update my prediction. **Election are hard to predict since the sample size is so small. For this reason, my mindset for this model is simplicity.**






```
## # A tibble: 1 × 7
##   format width height colorspace matte filesize density
##   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
## 1 PNG     1102    445 sRGB       TRUE     85205 57x57
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-1.png" width="551" />

Above, we can see that my model predicts Arizona and Georgia to be the only two swing states that turn red, ultimately leading to Kamala Harris winning the election. However, it's evident that the margin of victory is very minimal with a popular vote share between 49 and 51 percent. For this reason, I decided to see how much the results would be impacted with the inclusion of the 95% confidence interval.

Using the 95% confidence interval, we can see that the lower interval leads to a Republican win, and the upper interval leads to a Democratic win, both in landslides. This goes to show how close this election will be, and how limited models will be in predicting. 


```
## # A tibble: 1 × 7
##   format width height colorspace matte filesize density
##   <chr>  <int>  <int> <chr>      <lgl>    <int> <chr>  
## 1 PNG     2798    453 sRGB       TRUE    184541 57x57
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-8-1.png" width="1399" />



**Visualizing My Model**

For the sake of visualizing my prediction, I have looked at the adjusted vote share, instead of the lower and upper confidence intervals. Compared to last week, this map displays that Arizona and Georgia will both vote red. The remaining swing states will remain blue, as predicted last week.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-10-1.png" width="672" />

**My final model shows that Kamala Harris will defeat Donald Trump**. As I've emphasized throughout the past nine weeks, I don't think this election will be a landslide victory, so I am not completely confident in the results I have come to, since they give Harris a strong upper hand.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-11-1.png" width="672" />

My uncertainty can be explained through the numerous anomalies we've looked into that explain only this election. From the assassination attempt, to candidate switch, to campaign funding, this election has been composed of unpredictable factors. My gut tells me that Kamala Harris will win the election, albeit not by a lot. I believe this because I predict that voter turnout will be higher this year, compared to 2020. I also believe turnout among young people will be high, which is not otherwise true in US history.
