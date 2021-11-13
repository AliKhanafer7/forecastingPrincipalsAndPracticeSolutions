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

## Question 4
