# ARIMA-model
 Forecasting Malaysia COVID-19 Daily Cases Using ARIMA Model. ARIMA stands for Autoregressive Integrated Moving Average Model. It belongs to a class of models that explains a given time series based on its own past values. ARIMA Models are specified by three order parameters: (p, d, q). p is the order of the AR (autoregression) term, q is the order of the MA (Moving Average) term and d is the number of differencing required to make the time series stationary
 
This is one of my tasks as a research assistant. I had to forecast Malaysia's daily cases of COVID-19 in Malaysia using Python. I managed data of COVID-19 during my internship and the daily cases data is from the official Facebook of the Ministry of Health Malaysia. The data from 26/01/2020 until 11/07/2021.

# 1) Plot Malaysia's daily cases data
* I plotted daily cases data to check for the trend and seasonality

![Image of Trend](https://github.com/Izzan54/ARIMA-model/blob/main/Trend.png)

# 2) Checking for stationary

* I checked stationary of time series using Augmented Dickey Fuller test and ACF plotting
* Augmented Dickey Fuller test (ADF Test) is a common statistical test used to test whether a given time series is stationary or not.
* ADF Test p-value = 0.993922, P-value was greater than 0.05, which meant data is non-stationary

![Image of ACF](https://github.com/Izzan54/ARIMA-model/blob/main/ACF%20plot.png)

* I also checked whether the time series was stationary or not using ACF plot. 
* Autocorrelation Function (ACF) is a function that gives the values of auto-correlation of any series with its lagged values. When the ACF of the original data was plotted, we could see that the ACF plot dampened down to 0 very slowly. This meant that the time series was not stationary. Thus, differencing was required to obtain a stationary time series.

# 2) Differencing, d
* I differenced the time series once and checked stationary of the first differenced data with ADF test.
* ADF p-value: 0.000021, P-value was less than 0.05, which meant the data was stationary. So, our d term was 1.
* I also checked ACF plot for first order differenced data

![Image of ACF](https://github.com/Izzan54/ARIMA-model/blob/main/differencing.png)

# 3) AutoRegression Term, p and Moving Average term, q
* We would find out the required number of AR terms (p) by inspecting the Partial Autocorrelation (PACF) plot.

![Image of PACF](https://github.com/Izzan54/ARIMA-model/blob/main/PACF%20of%20differenced%20data.png)

* We would look at ACF plot for the number of MA terms (q).

![Image of ACF](https://github.com/Izzan54/ARIMA-model/blob/main/ACF%20of%20differenced%20data.png)

* From observation from the ACF and PACF plot, we could not decide the best p and q term because a few lags are well above the significance line. We only knew our d term is 1. So, I used auto_arima to find the best model.

# 4) Find the best model using auto_arima
* auto_arima() uses a stepwise approach to search the multiple ARIMA models and chooses the best model that has the least Akaike’s Information Criterion(AIC).
* The Akaike information criterion (AIC) is an estimator of prediction error and thereby relative quality of statistical models for a given set of data.
* From auto_arima, the best model was ARIMA(5,1,3)

# 5) Prediction and Forecasting daily cases
* Splitted the data to train and test data. Approximately 70% train (400) data and 30% test data (133).
* Plotted the prediction of daily cases.

![Image of predicted](https://github.com/Izzan54/ARIMA-model/blob/main/predicted%20daily%20cases.png)

* I plotted the prediction plot from 1/03/2021 until 11/07/2021 (test set)

![Image of predicted test](https://github.com/Izzan54/ARIMA-model/blob/main/prediction%20plot%20of%20test%20set.png)

* Checking for prediction error, RMSE = 4742.100508599653 
* Then, I forecasted Malaysia's daily cases 10 day onwards using ARIMA(5,1,3) with 95% confidence interval.

![Image of predicted test](https://github.com/Izzan54/ARIMA-model/blob/main/forecasting%20plot.png)
