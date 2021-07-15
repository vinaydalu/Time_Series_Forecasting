# Web Traffic Time Series Forecasting
![timeseries](https://github.com/vinaydalu/Time_Series_Forecasting/blob/main/Images/Time-Series-Analysis.jpg)
# <u> Overview of Data
  The training dataset consists of approximately 145k time series. Each of these time series represent a number of daily views of a different Wikipedia article, starting from July, 1st, 2015 up until December 31st, 2016.
  The prediction is based on the daily views between September 13th, 2017 and November 13th, 2017 for each article in the dataset. 
  # <u> Understanding the data
  By using some plots we tried to drawn some insights of data to exploit and explain the data in visual form.
  
  ## Web Traffic of Months across weekdays - HeatMap.
  ![weekdays](https://github.com/vinaydalu/Time_Series_Forecasting/blob/main/Images/heatmap_weekdays.png)
  
  Comapre to other weekdays, in the month of november(11th) sunday and wednesday have more web traffic. 
  
  ## Web Traffic of Months across Days - HeatMap.
  
  ![days](https://github.com/vinaydalu/Time_Series_Forecasting/blob/main/Images/heatmap_days.png)
  
  From the above HeatMap, we see a lot of web Traffic on days 26,27 and 29 in the December month(12th).
  
  ## Website visit Count(Monthwise)
  ![visit_count](https://github.com/vinaydalu/Time_Series_Forecasting/blob/main/Images/visit_count.png)
  
  It's lucidly shown that on the 11th month 2016 year we have a incresead number of vistis on our site.
  
  ## Monthly and weekday visits - BarGraphs.
  
![monthly](https://github.com/vinaydalu/Time_Series_Forecasting/blob/main/Images/Monthly.png)  &nbsp; &nbsp; &nbsp; &nbsp;   ![week](https://github.com/vinaydalu/Time_Series_Forecasting/blob/main/Images/weekdays.png)
  
  ## TimeSeries Mean - Daily,Weekly,Monthly
  
  ![timeseries](https://github.com/vinaydalu/Time_Series_Forecasting/blob/main/Images/timeseries.png)
  
  We consider Daily Time series from our data as it is similar to time series pattern and is easy to analyze trends.
  
  # <u> Is data stationary or not ?
  We have exploit our data now it's time to check if our data is stationary or not. If it is stationary the data do not change over time. It won’t show any trend or seasonal effect. Mean and variance remains constant over time.
  
  ## Time series - Mean
  ![mean](https://github.com/vinaydalu/Time_Series_Forecasting/blob/main/Images/mean_timeseries.png)
  
  ## Time series - standard Deviation
  ![std](https://github.com/vinaydalu/Time_Series_Forecasting/blob/main/Images/std_timeseries.png)
  
  Here the both timeseries are constant over time and doesn't show any changes in its trends.So we can say our data is stationary but to make sure we calculate p-value using Dickey Fuller test and KPSS test.
  ## <u> Augmented Dickey Fuller Test
  Augmented Dickey Fuller test (ADF Test) is a common statistical test used to test whether a given Time series is stationary or not. It is one of the most commonly used statistical test when it comes to analyzing the stationary of a series.We can achieve this by defining the null and alternate hypothesis.

  The statsmodel package provides a reliable implementation of the ADF test via the adfuller() function in statsmodels.tsa.stattools. It returns the following outputs:
  
1.The p-value
  
2.The value of the test statistic
  
3.Number of lags considered for the test
  
4.The critical value cutoffs.
  
When the test statistic is lower than the critical value shown, you reject the null hypothesis and infer that the time series is stationary.
  
  ![dickeyfullertest](https://github.com/vinaydalu/Time_Series_Forecasting/blob/main/Images/dickeyFullerTest.png)
  
  The p-value is very less than the significance level of 0.05 and hence we can reject the null hypothesis and take that the series is stationary.
  
  ### Plot the original data, the trend, the seasonality, and the residuals 
  
  ![comparison](https://github.com/vinaydalu/Time_Series_Forecasting/blob/main/Images/comparison.png)
  
## <u> KPSS Test
  KPSS test is a statistical test to check for stationarity of a series around a deterministic trend. Like ADF test, the KPSS test is also commonly used to analyse the stationarity of a series.
  In python, the statsmodel package provides a convenient implementation of the KPSS test.

A key difference from ADF test is the null hypothesis of the KPSS test is that the series is stationary.

So practically, the interpretaion of p-value is just the opposite to each other.
That is, if p-value is < signif level (say 0.05), then the series is non-stationary. Whereas in ADF test, it would mean the tested series is stationary.
The output of the KPSS test contains 4 things:
                               
1.The KPSS statistic
                               
2.p-value
                               
3.Number of lags used by the test
                               
4.Critical values
                               
The p-value reported by the test is the probability score based on which you can decide whether to reject the null hypothesis or not. If the p-value is less than a predefined alpha level (typically 0.05), we reject the null hypothesis.
                               
![kpss](https://github.com/vinaydalu/Time_Series_Forecasting/blob/main/Images/kpss.png)
         
Now clearly, the p-value is so high that you cannot reject the null hypothesis. So the series is stationary.
                 
 ## <u> Auto Correlation Function(ACF)
  ACF is an (complete) auto-correlation function which gives us values of auto-correlation of any series with its lagged values. it describes how well the present value of the series is related with its past values. A time series can have components like trend, seasonality, cyclic and residual. ACF considers all these components while finding correlations hence it’s a complete auto-correlation plot.
  
  ![acf](https://github.com/vinaydalu/Time_Series_Forecasting/blob/main/Images/ACF.png)
  
  ## <u> Partial Auto Correlation Function (PACF)
  
  PACF is a partial auto-correlation function. Basically instead of finding correlations of present with lags like ACF, it finds correlation of the residuals (which remains after removing the effects which are already explained by the earlier lag(s)) with the next lag value hence ‘partial’ and not ‘complete’ as we remove already found variations before we find the next correlation.
  
  ![pacf](https://github.com/vinaydalu/Time_Series_Forecasting/blob/main/Images/PACF.png)
  
  ## <u> ARMA Model(AutoRegressive Moving Average)
   This model explains the relationship of a time series with both random noise (moving average part) and itself at a previous step (autoregressive part).You use ARMA if the series is stationary.Mathematically, the ARMA(p,q) now requires tho parameters:
  
  p: the order of the autoregressive process
  
  q: the order of the moving average process
  
  ![arma](https://github.com/vinaydalu/Time_Series_Forecasting/blob/main/Images/ARMA.png)
  
  ## <u> ARIMA Model(AutoRegressive Integrated Moving Average)
  This model is the combination of autoregression, a moving average model and differencing. In this context, integration is the opposite of differencing.
Differencing is useful to remove the trend in a time series and make it stationary.
  
It simply involves subtracting a point a t-1 from time t. Realize that you will, therefore, lose the first data point in a time series if you apply differencing once.
Mathematically, the ARIMA(p,d,q) now requires three parameters:
  
p: the order of the autoregressive process
  
d: the degree of differencing (number of times it was differenced)
  
q: the order of the moving average process
 
  with ARMA models, the ACF and PACF cannot be used to identify reliable values for p and q.
However, in the presence of an ARIMA(p,d,0) process:
  
* the ACF is exponentially decaying or sinusoidal
  
* the PACF has a significant spike at lag p but none after
  
Similarly, in the presence of an ARIMA(0,d,q) process:
  
* the PACF is exponentially decaying or sinusoidal
  
* the ACF has a significant spike at lag q but none after

 ![arima](https://github.com/vinaydalu/Time_Series_Forecasting/blob/main/Images/ARIMA.png)
  
  ## <u> SARIMA Model (Seasonal Autoregressive Integrated Moving Average)
  SARIMA or Seasonal ARIMA, is an extension of ARIMA that explicitly supports univariate time series data with a seasonal component.

It adds three new hyperparameters to specify the autoregression (AR), differencing (I) and moving average (MA) for the seasonal component of the series, as well as an additional parameter for the period of the seasonality. Mathematically it represent as SARIMA(p,d,q)(P,D,Q)m :
  
### Trend Elements
 
p: Trend autoregression order.
  
d: Trend difference order.
  
q: Trend moving average order.
  
### Seasonal Elements
  
P: Seasonal autoregressive order.
  
D: Seasonal difference order.
  
Q: Seasonal moving average order.
  
m: The number of time steps for a single seasonal period.
  
 ![sarima](https://github.com/vinaydalu/Time_Series_Forecasting/blob/main/Images/SARIMA.png)
  
 ## <u> PMDARIMA Model
  
  The advantage of using Auto ARIMA over the ARIMA model is that after data preprocessing step we can skip the next steps & directly fit our model. It uses the AIC (Akaike Information Criterion) & BIC(Bayesian Information Criterion) values generated by trying different combinations of p,q & d values to fit the model.
  
  ![pmdarima](https://github.com/vinaydalu/Time_Series_Forecasting/blob/main/Images/PMDARIMA.png)
  
  Histogram plus estimated density plot: The red KDE line follows closely with the N(0,1) line. This is a good indication that the residuals are normally distributed.
  
The Q-Q-plot: Shows that the ordered distribution of residuals (blue dots) follows the linear trend of the samples taken from a standard normal distribution with N(0, 1). This is an indication that the residuals are normally distributed.
  
The standardize residual plot: The residuals over time don’t display any obvious seasonality and appear to be white noise.
  
The Correlogram plot: Shows that the time series residuals have low correlation with lagged versions of itself.
  
  ## <u> Prophet 
  
Prophet is an additive regression model with a piecewise linear or logistic growth curve trend.It is a procedure for forecasting time series data based on an additive model where non-linear trends are fit with yearly, weekly, and daily seasonality, plus holiday effects. It works best with time series that have strong seasonal effects and several seasons of historical data.
  
  ![prophet](https://github.com/vinaydalu/Time_Series_Forecasting/blob/main/Images/prophet.png)
  
  ## <u> Conclusion
  ### Disclaimer 
  This is not an end-to-end project.What i have done is for purely knowledge purpose to get hands-on Time series forecasting and satistical models. Based on the models i have used ARIMA(p,d,q) i.e for the order ARIMA(1,0,2) got the less Mean Absolute Error (MAE) of 67.55% comparte to other models.
  
  ## <u> Future Improvements
  To gain more knowledge on Time series to get project done.
  
  ## <u> Reffered Links
  1. https://machinelearningmastery.com/time-series-forecasting-with-prophet-in-python/
  
  2. https://alkaline-ml.com/pmdarima/modules/generated/pmdarima.arima.auto_arima.html
  
  3. https://www.machinelearningplus.com/time-series/augmented-dickey-fuller-test/
  
  4. https://www.machinelearningplus.com/time-series/kpss-test-for-stationarity/
