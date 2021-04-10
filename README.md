# XYMA_Analytics

**Problem Statement for DS/ML Interns**
**The objective of this exercise is to the predict price for an agricultural commodity. Predict min, max and modal price for the commodity for next 30 days from last date in the data.**

data - https://drive.google.com/file/d/1udks0R6Qxa9LSdHwtroB4T1kd0sEn1K_/view?usp=sharing

**Algorithm and logic-** 

* minPrice, maxPrice, modalPrice of agricultural commodity sale is sorted and represented.
* missing data values are interpolated and the datasets on minPrice, maxPrice, modalPrice are visually represented.
* Moving average technique is employed, where the average is calculated by adding up all the data points during a specific period (say 30days) and dividing the sum by the number of time periods.
* The moving mean or the data of a feature for 31st day is the average of that feature for the previous 30days.
 Rolling averages of 30days is employed for minPrice, maxPrice, modalPrice for the entire period from 2005-04-11 to 2018-08-31 and represented visually.
* Now for Time Series Forcasting, which is is the process of making future predictions based on past and present data, the data has to be stationary and seasonal.
* For verifying the data to be stationary, Augmented Dickey Fuller test (ADF Test) is used and the p-value for the features are noted.
* If the p value is greater than 0.05 during the ADF test of the time series then the series is said to be Non-stationary and it accepts NULL hypothesis. If p value is less than 0.05, it rejects NULL hypothesis which is symbolized  as H0, and it is said to be stationary where data doesn't have unit root.
* For the given data on agricultural sale, the following are the p-values-
	1. modalPrice p-value: 0.0036
	2. minPrice p-value: 0.0072
	3. maxPrice p-value: 0.0025
	thus, all the features have p-value less than 0.05 and thus the data is stationary.
* ARIMA (Auto Regressive Integrated Moving Average) model is employed for the time series prediction.
* ARIMA Consists of-
	1. Auto regression, which is a time series model that performs regression in previous t-1 time steps to predict time t.
	2. MA stands for moving average which is also called as rolling mean and was employed previously.
* best stepfit orders of the auto arima model is identified for the features and are noted,
	1. modalPrice - ARIMA(2,1,2)(0,0,0)[0]
	2. minPrice - ARIMA(2,1,1)(0,0,0)[0] 
	3. maxPrice - ARIMA(0,1,1)(0,0,0)[0]
* the stepwisefit orders of ARIMA Model are of notation ARIMA(P,D,Q). P is the order of autoregression, D is the order of differencing the non-stationary model to a stationary model (if needed) and Q is the order of moving mean model.
* ARIMA model class objects were initiated for all the 3 features with their respective stepfit orders.
* featureset datas('modalPrice' , 'minPrice' and 'maxPrice') were fed to the ARIMA Models respectively.
* models were tested on the last 30 days and were trained on the start day to the last 30th day from the end.
* future index dates were set to the next 30days from the given data (2018-09-01 to 2018-09-30).
* 30 days forcasting predictions were made for 'modalPrice' , 'minPrice' and 'maxPrice' from the 3 Arima models which were fitted on 'modalPrice' , 'minPrice' and 'maxPrice' previously.
* The 30Days forcasted predictions of 'modalPrice' , 'minPrice' and 'maxPrice' were concatenated into a single dataframe with their adjacent priceDates.

**Possible Improvements-**

*  ARIMA can be limited in forecasting extreme values. While the model is adept at modelling seasonality and trends, outliers are difficult to forecast for ARIMA for the very reason that they lie outside of the general trend as captured by the model. Thus LSTM model can be used to overcome this limitation.
*  If we don’t have time series data, the ARIMA package will not work.



