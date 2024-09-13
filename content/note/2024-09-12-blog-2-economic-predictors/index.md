---
title: 'Blog #2: Economic Predictors'
author: Shivali Korgaonkar
date: '2024-09-12'
slug: blog-2-economic-predictors
categories: []
tags: []
---














  An incumbent president running for re-election reaps both benefits and barriers. For one, they are a candidate that the American people are familiar with and normalized to. That being said, the American people also have four years of work to analyze and interpret. The condition of the United States is put on the sitting Commander-in-Chief who is already in the position to lead the economy, culture, and social circumstances of their country. In the past decade, we've seen Former President Barack Obama benefit in his re-election campaign against Mitt Romney, having been in a post-Hurricane Sandy relief era and reviving the economy after a significant bump during his mid-terms. On the other end, we saw Former President Donald Trump face the repercussions of controversial foreign relations, poor COVID-19 relief, and high unemployment in 2020.
  With this in mind, my second blog post will focus on different independent variables that can be used to predict the outcome of the 2024 election. Specifically, I will use economic variables to analyze their predictive abilities in elections between 1948 and 2020, in order to see the variable(s) best suited to predict the election in November. 


```r
####----------------------------------------------------------#
#### Understanding the relationship between economy and vote share. 
####----------------------------------------------------------#

# Create scatterplot to visualize relationship between Q2 GDP growth and 
# incumbent vote share. 
d_inc_econ |> 
  ggplot(aes(x = GDP_growth_quarterly, y = pv2p, label = year)) + 
  geom_text() + 
  geom_hline(yintercept = 50, lty = 2) + 
  geom_vline(xintercept = 0.01, lty = 2) +
  labs(title = "Relationship Between GDP Growth and Incumbent Voter Share",
       subtitle = "1948-2020",
       x = "Second Quarter GDP Growth (%)", 
       y = "Incumbent Party's National Popular Vote Share") + 
  my_blog_theme()
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-1-1.png" width="672" />










```r
# Can add bivariate regression lines to our scatterplots. 
d_inc_econ |> 
  ggplot(aes(x = GDP_growth_quarterly, y = pv2p, label = year)) + 
  geom_text() + 
  geom_smooth(method = "lm", formula = y ~ x) +
  geom_hline(yintercept = 50, lty = 2) + 
  geom_vline(xintercept = 0.01, lty = 2) + 
  labs(x = "Second Quarter GDP Growth (%)", 
       y = "Incumbent Party's National Popular Vote Share", 
       title = "Y = 51.25 + 0.274 * X") + 
  my_blog_theme() + 
  theme(plot.title = element_text(size = 18))
```

```
## Warning: The following aesthetics were dropped during statistical transformation: label
## ℹ This can happen when ggplot fails to infer the correct grouping structure in
##   the data.
## ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
##   variable into a factor?
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-1.png" width="672" />

```r
d_inc_econ_2 |> 
  ggplot(aes(x = GDP_growth_quarterly, y = pv2p, label = year)) + 
  geom_text() + 
  geom_smooth(method = "lm", formula = y ~ x) +
  geom_hline(yintercept = 50, lty = 2) + 
  geom_vline(xintercept = 0.01, lty = 2) + 
  labs(x = "Second Quarter GDP Growth (%)", 
       y = "Incumbent Party's National Popular Vote Share", 
       title = "Y = 49.38 + 0.737 * X") + 
  my_blog_theme() + 
  theme(plot.title = element_text(size = 18))
```

```
## Warning: The following aesthetics were dropped during statistical transformation: label
## ℹ This can happen when ggplot fails to infer the correct grouping structure in
##   the data.
## ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
##   variable into a factor?
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-2-2.png" width="672" />

```r
# Evaluate the in-sample fit of your preferred model.

summary(reg_econ)$r.squared
```

```
## [1] 0.1880919
```

```r
summary(reg_econ_2)$r.squared
```

```
## [1] 0.3248066
```

  The first data set has a R squared value of 0.1881,while the second data set, which excludes the 2020 election year, has a R squared value of 0.3248. The R squared value helps identify how strongly the independent variable can be predicted by the dependent variable. In this case, the regression seeks to find out the relationship between GDP growth in the second quarter and the incumbent party's popular vote share. The Y variable (vote share) can be better predicted based on the X variable (GDP growth) when 2020 is excluded.



```r
plot(d_inc_econ$year, d_inc_econ$pv2p, type="l", 
  main = "True Y (Line), Predicted Y (Dot) for each year")
points(d_inc_econ$year, predict(reg_econ_2, d_inc_econ))
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-3-1.png" width="672" />

```r
# Summarize mean squared error

mse <- mean((reg_econ_2$model$pv2p - reg_econ_2$fitted.values)^2)
mse
```

```
## [1] 17.7027
```


```r
# Model Testing: Leave-One-Out
(out_samp_pred <- predict(reg_econ_2, d_inc_econ[d_inc_econ$year == 2020,]))
```

```
##        1 
## 28.75101
```

```r
(out_samp_truth <- d_inc_econ |> filter(year == 2020) |> select(pv2p))
```

```
## # A tibble: 1 × 1
##    pv2p
##   <dbl>
## 1  47.7
```

```r
out_samp_pred - out_samp_truth # Dangers of fundamentals-only model!
```

```
##        pv2p
## 1 -18.97913
```

```r
# https://www.nytimes.com/2020/07/30/business/economy/q2-gdp-coronavirus-economy.html

# Model Testing: Cross-Validation (One Run)
years_out_samp <- sample(d_inc_econ_2$year, 9) 
mod <- lm(pv2p ~ GDP_growth_quarterly, 
          d_inc_econ_2[!(d_inc_econ_2$year %in% years_out_samp),])
out_samp_pred <- predict(mod, d_inc_econ_2[d_inc_econ_2$year %in% years_out_samp,])
out_samp_truth <- d_inc_econ_2$pv2p[d_inc_econ_2$year %in% years_out_samp]
mean(out_samp_pred - out_samp_truth)
```

```
## [1] 2.262913
```

```r
# Model Testing: Cross-Validation (1000 Runs)
out_samp_errors <- sapply(1:1000, function(i) {
  # TODO
})
```


```r
####----------------------------------------------------------#
#### Predicting 2024 results using simple economy model. 
####----------------------------------------------------------#
# Sequester 2024 data.
GDP_new <- d_fred |> 
  filter(year == 2024 & quarter == 2) |> 
  select(GDP_growth_quarterly)

# Predict.
predict(reg_econ_2, GDP_new) 
```

```
##        1 
## 51.58486
```

```r
predict(reg_econ_2, GDP_new, interval = "prediction") #provides 95% confidence interval
```

```
##        fit      lwr     upr
## 1 51.58486 41.85982 61.3099
```

```r
# Predict uncertainty.
# TODO 
```



```r
### Relationship between CPI and vote share

# Create scatterplot to visualize relationship between CPI and incumbent vote share. 
d_inc_econ |> 
  ggplot(aes(x = CPI, y = pv2p, label = year)) + 
  geom_text() + 
  geom_hline(yintercept = 50, lty = 2) + 
  labs(title = "Relationship between CPI and Incumbent Vote Share",
       subtitle = "1948-2020",
       x = "Consumer Price Index (CPI)", 
       y = "Incumbent Party's National Popular Vote Share") + 
  my_blog_theme()
```

<img src="{{< blogdown/postref >}}index_files/figure-html/CPI cor-1.png" width="672" />

```r
d_inc_econ |> 
  ggplot(aes(x = CPI, y = pv2p, label = year)) + 
  geom_text() + 
  geom_smooth(method = "lm", formula = y ~ x) +
  geom_hline(yintercept = 50, lty = 2) + 
  labs(title = "Relationship between CPI and Incumbent Vote Share",
       subtitle = "Y = 53.76 - 0.017 * X",
       x = "Consumer Price Index (CPI)", 
       y = "Incumbent Party's National Popular Vote Share") + 
  my_blog_theme() + 
  theme(plot.title = element_text(size = 18))
```

```
## Warning: The following aesthetics were dropped during statistical transformation: label
## ℹ This can happen when ggplot fails to infer the correct grouping structure in
##   the data.
## ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
##   variable into a factor?
```

<img src="{{< blogdown/postref >}}index_files/figure-html/CPI cor-2.png" width="672" />

```r
# Compute correlations between CPI and incumbent vote 2-party vote share.
cor(d_inc_econ$CPI, 
    d_inc_econ$pv2p)
```

```
## [1] -0.2762669
```

```r
cor(d_inc_econ_2$CPI, 
    d_inc_econ_2$pv2p)
```

```
## [1] -0.2218343
```

```r
# Fit bivariate OLS. 
reg_cpi <- lm(pv2p ~ CPI, 
               data = d_inc_econ)
reg_cpi |> summary()
```

```
## 
## Call:
## lm(formula = pv2p ~ CPI, data = d_inc_econ)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -8.5915 -3.6807 -0.5288  2.9385  8.7491 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept) 53.76136    2.04701  26.263 3.35e-15 ***
## CPI         -0.01734    0.01463  -1.185    0.252    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 5.156 on 17 degrees of freedom
## Multiple R-squared:  0.07632,	Adjusted R-squared:  0.02199 
## F-statistic: 1.405 on 1 and 17 DF,  p-value: 0.2522
```

```r
reg_cpi_2 <- lm(pv2p ~ CPI, 
                         data = d_inc_econ_2)
reg_cpi_2 |> summary()
```

```
## 
## Call:
## lm(formula = pv2p ~ CPI, data = d_inc_econ_2)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -8.4949 -3.7923 -0.1371  3.1621  8.8106 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept) 53.60353    2.15372   24.89 3.21e-14 ***
## CPI         -0.01503    0.01651   -0.91    0.376    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 5.296 on 16 degrees of freedom
## Multiple R-squared:  0.04921,	Adjusted R-squared:  -0.01021 
## F-statistic: 0.8281 on 1 and 16 DF,  p-value: 0.3763
```

```r
#2024 Prediction
# Sequester 2024 data.
CPI_new <- d_inc_econ |>
  filter (year == 2020 & quarter == 2) |>
  select(CPI)

# Predict.
predict(reg_cpi, CPI_new) 
```

```
##        1 
## 49.31611
```

```r
predict(reg_cpi, CPI_new, interval = "prediction") #provides 95% confidence interval
```

```
##        fit      lwr      upr
## 1 49.31611 37.32375 61.30847
```

```r
### Relationship between unemployment and vote share

# Create scatterplot to visualize relationship between CPI and incumbent vote share. 
d_inc_econ |> 
  ggplot(aes(x = unemployment, y = pv2p, label = year)) + 
  geom_text() + 
  geom_hline(yintercept = 50, lty = 2) + 
  geom_vline(xintercept = 0.01, lty = 2) +
  labs(title = "Relationship between Unemployment and Incumbent Vote Share",
       subtitle = "1948-2020",
       x = "Unemployment Rate (%)", 
       y = "Incumbent Party's National Popular Vote Share") + 
  my_blog_theme()
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-6-1.png" width="672" />

```r
d_inc_econ |> 
  ggplot(aes(x = unemployment, y = pv2p, label = year)) + 
  geom_text() + 
  geom_smooth(method = "lm", formula = y ~ x) +
  geom_hline(yintercept = 50, lty = 2) + 
  labs(title = "Relationship between Unemployment and Incumbent Vote Share",
       subtitle = "Y = 53.63 - 0.312 * X",
       x = "Unemployment Rate (%)", 
       y = "Incumbent Party's National Popular Vote Share") + 
  my_blog_theme() + 
  theme(plot.title = element_text(size = 18))
```

```
## Warning: The following aesthetics were dropped during statistical transformation: label
## ℹ This can happen when ggplot fails to infer the correct grouping structure in
##   the data.
## ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
##   variable into a factor?
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-6-2.png" width="672" />

```r
# Compute correlations between CPI and incumbent vote 2-party vote share.
cor(d_inc_econ$unemployment, 
    d_inc_econ$pv2p)
```

```
## [1] -0.1368118
```

```r
cor(d_inc_econ_2$unemployment, 
    d_inc_econ_2$pv2p)
```

```
## [1] 0.006522146
```

```r
# Fit bivariate OLS. 
reg_unemp <- lm(pv2p ~ unemployment, 
               data = d_inc_econ)
reg_unemp |> summary()
```

```
## 
## Call:
## lm(formula = pv2p ~ unemployment, data = d_inc_econ)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -7.9906 -2.6616 -0.9256  2.4016  9.9399 
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)    
## (Intercept)   53.6260     3.4614  15.493 1.85e-11 ***
## unemployment  -0.3117     0.5475  -0.569    0.577    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 5.314 on 17 degrees of freedom
## Multiple R-squared:  0.01872,	Adjusted R-squared:  -0.03901 
## F-statistic: 0.3243 on 1 and 17 DF,  p-value: 0.5765
```

```r
reg_unemp_2 <- lm(pv2p ~ unemployment, 
                         data = d_inc_econ_2)
reg_unemp_2 |> summary()
```

```
## 
## Call:
## lm(formula = pv2p ~ unemployment, data = d_inc_econ_2)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -7.2394 -2.9835 -0.7848  2.5555  9.7788 
## 
## Coefficients:
##              Estimate Std. Error t value Pr(>|t|)    
## (Intercept)  51.88452    4.84160  10.716 1.04e-08 ***
## unemployment  0.02205    0.84527   0.026     0.98    
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 5.431 on 16 degrees of freedom
## Multiple R-squared:  4.254e-05,	Adjusted R-squared:  -0.06245 
## F-statistic: 0.0006806 on 1 and 16 DF,  p-value: 0.9795
```

```r
#2024 Prediction
# Sequester 2024 data.
unemp_new <- d_inc_econ |>
  filter (year == 2020 & quarter == 2) |>
  select(unemployment)

# Predict.
predict(reg_unemp_2, unemp_new) 
```

```
##       1 
## 52.1712
```

```r
predict(reg_unemp_2, unemp_new, interval = "prediction") #provides 95% confidence interval
```

```
##       fit      lwr      upr
## 1 52.1712 34.30039 70.04202
```

```r
lm(formula = pv2p ~ GDP_growth_quarterly + 
     dpi,
   data = d_inc_econ)
```

```
## 
## Call:
## lm(formula = pv2p ~ GDP_growth_quarterly + dpi, data = d_inc_econ)
## 
## Coefficients:
##          (Intercept)  GDP_growth_quarterly                   dpi  
##            5.218e+01             2.523e-01            -3.289e-05
```

