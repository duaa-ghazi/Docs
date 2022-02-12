ML- analysis task : 

1- install the needed packages .

2- read about : 

* numPy : NumPy is a Python library used for working with arrays.NumPy aims to provide an array object that is up to 50x faster than  traditional Python lists.The array object in NumPy is called `ndarray`,  it provides a lot of supporting functions that make working with  `ndarray` very easy.

   *Why is NumPy Faster Than Lists? NumPy arrays are stored at one continuous place in memory unlike  lists, so processes can access and manipulate them very efficiently.

  This behavior is called locality of reference in computer science.

  https://www.w3schools.com/python/numpy/default.asp

* Pandas : is a Python library.

  Pandas is used to analyze data.,cleaning the data and plotting data .

  also for read csv,json.

  https://www.w3schools.com/python/pandas/default.asp

* Matplotlib:  is a low level graph plotting library in python that serves as a visualization utility.

  https://www.w3schools.com/python/matplotlib_scatter.asp

  https://matplotlib.org/stable/gallery/style_sheets/ggplot.html

  ****************************************

  * fit ml model  : in statistics, a fit refers to **how well you approximate a target function**. This is good terminology to use in machine learning

  

  What is sklearn:

  Scikit-learn (Sklearn) is the most **useful and robust library for machine learning in Python**. It provides a selection of efficient tools for machine learning and  statistical modeling including classification, regression, clustering  and dimensionality reduction via a consistence interface in Python.

  

  

  Prophet :

  is a procedure for forecasting time series data based on an  additive model where non-linear trends are fit with yearly, weekly, and  daily seasonality, plus holiday effects. It works best with time series  that have strong seasonal effects and several seasons of historical  data. Prophet is robust to missing data and shifts in the trend, and  typically handles outliers well.

  Prophet follows the `sklearn` model API, We create an instance of the `Prophet` class and then call its `fit` and `predict` methods.

  

  The input to Prophet is always a dataframe with two columns: `ds` and `y`.  The `ds` (datestamp) column should be of a format expected by Pandas, ideally  YYYY-MM-DD for a date or YYYY-MM-DD HH:MM:SS for a timestamp. The `y` column must be numeric, and represents the measurement we wish to forecast.

  

  https://facebook.github.io/prophet/docs/quick_start.html

  ************************

  ```bash
  #to run python script , go to directory 
  $python3 closePlot.py
  
  #install pip from python 3  :
  $sudo apt install python3-pip
  
  #to install package :
  $pip  install seaborn
  ```

  

  **************************************

  ```
  
  
  import pandas as pd
  import numpy as np
  from prophet import Prophet
  from pyspark.sql import *
  from pandas import read_csv
  from pandas import to_datetime
  from IPython.display import display
  import matplotlib.pyplot as plt
  from pandas import to_datetime
  from datetime import datetime
  import seaborn as sns
  
  plt.style.use('ggplot')
  
  
  # Data Source 
  path = '/home/duaa/ML/forecasting-main/EnergyLinear.csv'
  df = read_csv(path, header=0)
  #df = pd.pivot_table(pi,index=['Date'],aggfunc={'Energy':np.sum})
  df = df.groupby('Date', as_index=False)['Energy'].sum().rename(columns={'Date':'ds','Energy' : 'y'})
  print(df)
  df.info()
  df['ds']= to_datetime(df['ds'])
  
  
  df = df.set_index('ds').asfreq('D').reset_index(0)
  df['y'] = df['y'].fillna(0)
  
  
  df=df.sort_values(by='ds')
  
  print(df)
  
  df['y'] = df['y'].cumsum()
  
  print(df)
  print(df.describe())
  
  
  sns.lineplot(x='ds', y='y', data=df)
  
  dataList = df['ds'].values.tolist()
  dataLen = len(dataList)
  forecastedData = [] 
  
  
  
  # instantiate the model and set parameters
  
  
  
  
  
  model = Prophet()
   
  
   
  # fit the model to historical data
  model.fit(df)
  
  # define a dataset including both historical dates & 90-days beyond the last available date, using Prophet's built-in make_future_dataframe method
  future_pd = model.make_future_dataframe(
   periods=30, freq='d' , include_history=False
  )
  
  
  future_pd.tail()
  # predict over the dataset
  #Prophet(interval_width=0.95,weekly_seasonality=28, daily_seasonality=True ,changepoint.prior.scale=0.01)
  forecast_pd= model.predict(future_pd)
  
  print(forecast_pd[["ds","yhat",'yhat_lower', 'yhat_upper']])
  
  print(forecast_pd.describe())
  # listt = forecast_pd[["yhat"]].values.tolist()
  # return only the forecasted Data
  # while dataLen < len(listt):
  #   forecastedData.append(listt[dataLen])
   #  dataLen = dataLen + 1
  
  print(forecastedData)
  predict_fig = model.plot(forecast_pd, xlabel='date', ylabel='Energy')
  
  fig = model.plot_components(forecast_pd)
  plt.show()
  ```

  