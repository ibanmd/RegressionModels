# An Analysis of Fuel Efficiency by Transmission Type   

## Summary
The purpose of this analysis was to determine in what manner the type of transmission an automobile has affects its fuel efficiency in miles per gallon (MPG).  In addition to examining what effect transmission type has on MPG, the effects from other variables were also considered.  This was necessary because many of the variables were related.  For example, consider the variables Weight and Transmission Type.  Luxury cars are often large and heavy and come with automatic transmissions, so it may appear that automatic transmissions lead to lower MPG values, while it is in fact due to the high weight of the car.  What was found that in general, automobiles with manual transmission tend to have higher MPG than automatic transmission automobiles, but that this difference is not likely due to the transmission type.  Variables such as engine horse power and automobile weight are stronger predictors for MPG than transmission type.

## Exploring the data



The analysis will begin with some visual exploration of the data.  The box plot below immediately gives us a possible indication that automobiles with manual transmissions appear to be more fuel efficient.  Automobiles with automatic transmissions have a median MPG of about 17.3 while automobiles with manual transmissions have a median MPG of about 22.8.  

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2.png) 

However, though automobiles with manual transmissions appear to be more fuel efficient in general, it is not possible to conclude at this point that this difference is due to transmission type solely.  It may be that all cars with manual transmissions happen to also be very light and have small engines.  In the Appendix is a pairs plot of some of variables in order to see how they relate to each other.



A few expected correlations are immediately seen, for example, that Displacement and Horsepower are positively correlated.  Neither is it surprising that Weight and MPG have a negative correlation.  Another interesting relationship is that between Transmission Type and Gears (number of forward gears in the transmission).  We see that all automobiles with three gears are automatics, and all with five gears are manuals.  Automobiles with four gears are primarily manuals.  

## Fitting a linear model

Six predictors will be used in order to understand how transmission type relates to fuel efficiency.  Those six predictors are:
- TransType
- Cylinders
- Displacement
- Horsepower
- Weight
- Gears

A linear model is fitted for the following six combinations of the six predictors, and then the anova() function in R is used to compare the six linear models.  The R output for these tests can be found in the long version of this report.





The results of the anova test indicate that the model including TransType, Horsepower, and Weight would be a reasonable model to select, due to the fact that the next largest model has a large p-value, indicating that it is not very different from our selection.  Furthermore, it is reasonable that engine horsepower and the weight of the automobile are important predictors.  Leaving Displacement out of model is also justified due to the fact that it is highly correlated with both Weight and Horsepower, which were included.

## Diagnostics

For a plot of diagnostics, please refer to the Appendix.  The first plot, Residuals by Fitted values, shows that the constant variance assumption is reasonably met and that the data is reasonably linear.  The second plot (going by rows) confirms that the residuals have an approximately normal distribution.  Conducting the Shapiro-Wilk test for the normality of the residuals gives a p-value of 0.1059, meaning that there is not quite enough evidence to suggest the residuals are non-normal.  These plots also highlight a few outliers, namely the Chrysler Imperial, the Toyota Corolla, and the Fiat 128.  For now, since the model assumptions are being met and since the value of R^2 is 0.8399 with just three predictors, we can leave further investigation for another time.



## Results & Conclusions

Let us take a look again at the chosen model, which uses TransType, Horsepower, and Weight to predict MPG.


```
## 
## Call:
## lm(formula = MPG ~ TransType + Horsepower + Weight, data = data)
## 
## Residuals:
##    Min     1Q Median     3Q    Max 
## -3.422 -1.792 -0.379  1.225  5.532 
## 
## Coefficients:
##                 Estimate Std. Error t value Pr(>|t|)    
## (Intercept)     34.00288    2.64266   12.87  2.8e-13 ***
## TransTypeManual  2.08371    1.37642    1.51  0.14127    
## Horsepower      -0.03748    0.00961   -3.90  0.00055 ***
## Weight          -2.87858    0.90497   -3.18  0.00357 ** 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 2.54 on 28 degrees of freedom
## Multiple R-squared:  0.84,	Adjusted R-squared:  0.823 
## F-statistic:   49 on 3 and 28 DF,  p-value: 2.91e-11
```



We see that on average an automobile with a manual transmission gets 2.08 more MPG than an automobile with an automatic transmission, if the amount of horsepower and the weight of the automobile are held constant.  However, this estimate has a p-value of 0.14, which is higher than ideal (meaning not very significant).  It is the case that on average, each additional 10 horsepower translates into 0.4 fewer MPG.  Likewise, each additional 100 pounds the car weighs leads to a drop in MPG of 0.288.

### answering our two questions...

1) **Is an automatic or manual transmission better for MPG?**
- Answer: The data suggests that when ignoring all other variables and focusing solely on transmission type, a car with a manual transmission will get more MPG than a car with an automatic transmission.  Running a t-test on the MPG values:


We can say that a typical manual automobile gets about 7.24 more MPG than automatic one, and this value is significantly different than 0.  However, if an automobile's horsepower and weight are taken into account, that difference in MPG drops to 2.08, and that difference is no longer considered significant.  If the question refers to the vehicle in general, then yes, driving an automobile with a manual transmission will very likely secure you a higher MPG.  If the question refers to specifically the transmission, then though a manual transmission appears to give you about 2.08 extra MPG, it cannot be confidently said that this difference is significantly different than a difference of 0. 

2) **Quantify the MPG difference between automatic and manual transmissions.**
- Answer: Basically reiterating from the previous question and answer, automobiles with manual transmissions tend to have get about 7.24 more MPG than automobiles with automatic transmissions.  However, for a given weight and horsepower, a manual transmission will deliver about 2.08 more MPG than an automatic transmission.

# Appendix

### Pairs Plot
![plot of chunk unnamed-chunk-11](figure/unnamed-chunk-11.png) 

<!--### Model fitting and anova test-->




### Diagnostics

![plot of chunk unnamed-chunk-14](figure/unnamed-chunk-14.png) 

### Linear model visualization

![plot of chunk unnamed-chunk-15](figure/unnamed-chunk-15.png) 

