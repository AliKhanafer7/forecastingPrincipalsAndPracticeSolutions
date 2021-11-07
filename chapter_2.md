# Chapter 2
## Question 1
* **Gold:** Daily morning gold prices in US dollars. 1 January 1985 – 31 March 1989.
* **Woolyrnq:** Quarterly production of woollen yarn in Australia: tonnes. Mar 1965 – Sep 1994.
* **Gas:** Australian monthly gas production: 1956–1995.

### Question 1 a)
`autoplot(gold) + ggtitle("Daily morning gold prices in US dollars")`
![gold](https://user-images.githubusercontent.com/39031299/140650264-82de563b-82ac-438b-bc0d-8f751678da6d.jpg)

`autoplot(woolyrnq) + ggtitle("Quarterly production of woollen yarn in Australia: tonnes")`
![wool](https://user-images.githubusercontent.com/39031299/140650332-b94558c0-038b-4244-abdc-e401427390c4.jpg)

`autoplot(gas) + ggtitle("Australian monthly gas production")`

![gas](https://user-images.githubusercontent.com/39031299/140650392-e0c1c1c6-7ded-472d-bc45-79cad84e2f26.jpg)
### Question 1 b)
We can use the table in section 2.1, along with the `frequency` function to come up with the results:
```
> frequency(gold)
[1] 1
```
Meaning the frequency of the gold time series is annual i.e. the seasonal pattern of gold repeats every year
```
> frequency(woolyrnq)
[1] 4
```
Meaning the frequency of the woolyrnq is quarterly i.e. the seasonal pattern of woolen yarn in Australia repeats every three months

```
> frequency(gas)
[1] 12
```
Meaning the frequency of the woolyrnq is monthly i.e. the seasonal pattern of Australian gas production repeats every month

### Question 1 c)
`which.max` will print the index of the maximum value in the time series. So `which.max(gold)` will print the index of the observation with the highest daily morning gold price in the US
```
> which.max(gold)
[1] 770
```
And we can check the value of gold at 770
```
> gold[770]
[1] 593.7
```
so the outlier is 593.7 at observation 770
## Question 2
Autoplot with `facets=TRUE`:
![facet](https://user-images.githubusercontent.com/39031299/140651991-f518f549-352f-4d43-bc3a-ca5f9c1e1dd6.jpg)

Autoplot with `facets=FALSE`:
![nofacet](https://user-images.githubusercontent.com/39031299/140651883-1759cda5-6096-4bce-859c-91e684f1fed9.jpg)

The difference is in the way the plot seperates the different columns. With facets, the plot is seperated into different lanes, with each lane representing a different variable (Sales, AdBudjet or GDP). With no facets, the seperation between variables is done using a legend and different colors.

## Question 3
I chose category with ID `A3349335T`

`autoplot(myts) + ylab("A3349335T") + ggtitle("Retail Sales For Category A3349335T in Australian Cities")`

![Rplot](https://user-images.githubusercontent.com/39031299/140652461-a618b83b-d5d5-4ffd-aaf6-0c6ca2d87b84.jpg)

We can extract from this plot that there is a clear upward trend in the sales of items in category A3349335T accross Australia. We also see seasonality, but no cycles.

`ggseasonplot(myts) + ggtitle("Seasonal plot: A3349335T")`

![A3349335T](https://user-images.githubusercontent.com/39031299/140652558-aac82118-4c30-48c5-9191-c803bf49caf3.jpg)

We can extract from the seasonality plot some important information. For example, there seems to have been a constant drop in sales between March and June of 2011 (third line from the top). We also notice that there's always a drop in sales in the month of February.

## Question 4
## Question 5
* **Fancy:** Monthly sales for a souvenir shop on the wharf at a beach resort town in Queensland, Australia.
![fancy](https://user-images.githubusercontent.com/39031299/140653446-ed6293f8-7302-4afc-bcaf-af7b2cd45633.jpg)
![fancy2](https://user-images.githubusercontent.com/39031299/140653458-0b7c391d-3c94-4935-a99a-97f411c302c8.jpg)
  * Sales seem to be trending upwards on a yearly basis
  * Annual decrease in sales in the month of February
  * Annual increase in sales in the month of March
  * Odd descrease in sales in the month of May in 1993 and 1992

* **a10:** Monthly government expenditure (millions of dollars) as part of the Pharmaceutical Benefit Scheme for products falling under ATC code A10 as recorded by the Australian Health Insurance Commission. July 1991 - June 2008.






