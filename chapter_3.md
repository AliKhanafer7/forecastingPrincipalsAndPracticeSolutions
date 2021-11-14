# Chapter 3 
## Question 1
We can use the `BoxCox.lambda` function to find the appropriate lambda value, then `autoplot(Boxplot(some_dataset,lambda))` to draw the plot of the dataset with stabalised variance
```
> (lambda <- BoxCox.lambda(usnetelec))
[1] 0.5167714
> autoplot(BoxCox(usnetelec,lambda)) + ggtitle("Annual US net electricity generation") + xlab("year") + ylab("electricity generation")
```
![Screen Shot 2021-11-13 at 11 31 26 AM](https://user-images.githubusercontent.com/39031299/141651434-24e770a0-ef5c-4207-99ae-b29c57b841a9.png)

In this case the data before the Box-Cox transformation didn't have much variance to start with, so the Box-Cox transformation isn't much different then the original plot without any transformations

```
> (lambda <- BoxCox.lambda(usgdp))
[1] 0.366352
> autoplot(BoxCox(usgdp,0.2)) + ggtitle("Quarterly US GDP") + xlab("Quarter") + ylab("GDP")
```
![Screen Shot 2021-11-13 at 11 37 55 AM](https://user-images.githubusercontent.com/39031299/141651637-e94a9323-4788-477a-86eb-73cb0416e0ba.png)

Although `BoxCox.lambda` gave a value of 0.366, it looks like 0.2 reduces the variance slightly more. In general, I tried testing values +/- 0.1 of whatever `BoxCox.lambda` estimates to see if there can be better values.

```
> (lambda <- BoxCox.lambda(mcopper))
[1] 0.1919047
> autoplot(BoxCox(mcopper,lambda)) + ggtitle("Monthly copper prices") + xlab("Month") + ylab("Price")
```
![Screen Shot 2021-11-13 at 11 46 55 AM](https://user-images.githubusercontent.com/39031299/141651935-e543b794-cf85-4e0d-98d6-5cd4741d7e09.png)

## Question 2
The entire point behind a Box-Cox transformation is to transform our data so that the distribution of errors follows somewhat of a normal distribution. If we check the residuals of the `cangas` dataset, we see that the distribution of the errors already follows a normal distribution with mean zero, and so a Box-Cox transformation isn't needed 
```
checkresiduals(naive(cangas))
```

![Screen Shot 2021-11-14 at 9 43 53 AM](https://user-images.githubusercontent.com/39031299/141685972-e0319f31-324a-4657-b65b-5cf1bf84e467.png)

## Question 4

For the `dole` dataset, we're dealing with monthly values. So we can remove variation between the months by computing the average number of people on unemployement benefits, rather than the total.

```
> dframe <- cbind(Monthly = dole, DailyAverage = dole/monthdays(dole))
> autoplot(dframe, facet=TRUE) + xlab("Years") + ylab("People") + ggtitle("Monthly total of people on unemployment benefits")
```
![Screen Shot 2021-11-14 at 10 09 04 AM](https://user-images.githubusercontent.com/39031299/141686821-d2f9035a-4a09-497a-a563-72d14f018bd8.png)

The same applies for the `usdeaths` dataset

```
> dframe <- cbind(Monthly = usdeaths, DailyAverage = usdeaths/monthdays(usdeaths))
> autoplot(dframe, facet=TRUE) + xlab("Years") + ylab("Deaths") + ggtitle("Monthly accidental deaths in USA")
```
![Screen Shot 2021-11-14 at 10 11 10 AM](https://user-images.githubusercontent.com/39031299/141686904-be438005-d82c-4743-b3dd-14901b302813.png)

The `monthdays` function also returns the number of days in each quarter, so we can apply the same logic to the `bricksq` dataset

```
> dframe <- cbind(Quarterly = bricksq, DailyAverage = bricksq/monthdays(bricksq))
> autoplot(dframe, facet=TRUE) + xlab("Years") + ylab("Brick Production") + ggtitle("Australian quarterly clay brick production")
```

![Screen Shot 2021-11-14 at 10 15 49 AM](https://user-images.githubusercontent.com/39031299/141687065-33db5d47-3306-4bcd-8fd4-e9f3442ec746.png)

## Question 5
![Screen Shot 2021-11-14 at 10 49 52 AM](https://user-images.githubusercontent.com/39031299/141688174-38148e97-c738-481f-9f21-8d4342473f42.png)

```
	Ljung-Box test

data:  Residuals from Seasonal naive method
Q* = 32.269, df = 8, p-value = 8.336e-05

Model df: 0.   Total lags used: 8
```
At lag 4, the ACF shows a spike that is outside the bounds, indicating that the residuals are not white noise. We also see from the histogram that the residuals are not perfectly normally distributed, but close. We can conclude that the seasonal naive forecast applied to the quarterly Australian beer production time series needs more work to capture all information in the data and get a better fit

## Question 6
```
> checkresiduals(naive(bricksq))

	Ljung-Box test

data:  Residuals from Naive method
Q* = 244.43, df = 8, p-value < 2.2e-16

Model df: 0.   Total lags used: 8
```
![Screen Shot 2021-11-14 at 11 28 19 AM](https://user-images.githubusercontent.com/39031299/141689518-4526e458-f291-4cae-8019-87b548dbc8ed.png)
The residuals for the `bricksq` dataset are much more autocorrelated, with multiple spikes outside the bounds. This again indicates that the residuals do not follow the behaviour of a white noise series, thus the `naive` forecasting method isn't grabbing all the information necessary for a good fit. The residual distribution is far off from a normal one

## Question 7
a. True. White noise is normally distributed, and we want our residuals to resemble white noise, indicating that we've captured all possible information from our data

b. False. If the model is overfitted then small residuals means that the model will not generalize well to new data

c. False. Although it's the most commonly used, it's generally best to calculate a number of accuracy measures and compare them

d. False. It's not always the case that a more complicated model will give better forecasts. Your model could be overfitting, in which case you'd have to make it less complicated

e. True. Assuming we're not considering cross-validation, the test set is a good indicator of how well your model is forecasting

## Question 9
```
> train1 <- window(visnights[, "QLDMetro"], end = c(2015, 4))
> train2 <- window(visnights[, "QLDMetro"], end = c(2014, 4))
> train3 <- window(visnights[, "QLDMetro"], end = c(2013, 4))
> fc1 <- snaive(train1, h=1)
> fc2 <- snaive(train1, h=2)
> fc3 <- snaive(train1, h=3)
> test1 <- window(visnights[, "QLDMetro"], start=c(2016, 1))
> test2 <- window(visnights[, "QLDMetro"], start=c(2015, 1))
> test3 <- window(visnights[, "QLDMetro"], start=c(2014, 1))
> accuracy(fc1,test1)
                     ME      RMSE       MAE        MPE     MAPE      MASE       ACF1
Training set 0.02006107 1.0462821 0.8475553 -0.2237701 7.976760 1.0000000 0.06014484
Test set     0.30637474 0.3063747 0.3063747  2.5799546 2.579955 0.3614805         NA
> accuracy(fc2,test2)
                     ME      RMSE       MAE        MPE     MAPE      MASE        ACF1  Theil's U
Training set 0.02006107 1.0462821 0.8475553 -0.2237701 7.976760 1.0000000  0.06014484         NA
Test set     0.01362599 0.2930657 0.2927487 -0.2506566 2.830611 0.3454037 -0.50000000 0.09910268
> accuracy(fc3,test3)
                     ME      RMSE       MAE        MPE     MAPE      MASE        ACF1 Theil's U
Training set 0.02006107 1.0462821 0.8475553 -0.2237701 7.976760 1.0000000  0.06014484        NA
Test set     0.17418714 0.3728746 0.3602690  1.3022926 3.356471 0.4250684 -0.63017665 0.1762485
```
The MAPE value gets higher as we increase the number of years to forecast for. FC3 has the highest MAPE on the testing set since we want to forecast three years into the future, and FC1 has the lowest MAPE one the testing set since we're forecasting only one year into the future.
