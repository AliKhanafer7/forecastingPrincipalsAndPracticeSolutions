# Chapter 1
## Question 1
In order to answer this question, we first have to understand what a *predictor variable* is. Predictor variables are variables that influence or describe the behaviour of the variable we're trying to forecast for. This is synonomous to the term *independent variable* in calculus, *covariate* in statistics, or *feature* in machine learning.

Useful predictor variables for case 3:
* Amount of mileage on the car
* Number of times it was leased
* Car age
* Location

Useful predictor variables for case 4:
* Time of year
* Destination 
* City departing from
* Flight duration

## Question 2
1. **Problem Definition:** Large car fleet companies don't have a metric to base their car prices off of. This can cause a situation where their cars are either overpriced, causing low sales volumes, or their cars are underpriced, limiting their profits. They also don't know what internal and external factors impact the price of their cars, again resulting in a situation where their profits aren't maximised. With a forecasting model, car fleet companies will be able to get a better understanding of the price they should place on their cars, depending on different variables such as age, mileage and number of past users. Forecasts will also give them a better understanding of what factors impact the price of a car, and allow them to adjust their policies accordingly.
2. **Gathering Information:** In the case of a car fleet company, gathering information means gathering data on cars that were either previously leased, currently leased, previously sold and neither leased nor sold (still on the lot). Information needed are those described in question 1, along with others. It would also be beneficial to talk to the group of specilists, if they're willing to give any valuable information.
3. **Preliminary (exploratory) analysis:** Examples of graphs that can be used to draw valuable information:
   * Car price vs mileage
   * Car price vs number of leasers
   * Car brand vs number of buyers 
   * Car price vs time of year

4. **Choosing and Fitting Models:** Depending on the results from the first three steps, the decision of which model to choose will change. Examples of models we can try include linear regression, ridge regression, lasso. But all will depend on the kind and shape of your data.
5. **Using and Evaluating a Forecasting Model:** We can now use the model we've selected in step 4. to give our customers better baselines for how much they should price a car they plan on reselling. At this point, we anticipate some unforeseen issues to arise due to the unpredictable nature of forecasting problems, but we also anticipate that going through the first four steps help reduce the number of uncertainties we'll have to deal with. 
