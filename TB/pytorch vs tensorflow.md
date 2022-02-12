# **pytorch** and **tensorflow** : 

pytorch and tensorflow both are deep learning frameworks .  

- pytorch vs tensorflow

| pytorch                                      | Tensorflow                                                   |
| -------------------------------------------- | ------------------------------------------------------------ |
| native python support                        | python , Layered component .                                 |
| easy to use api                              | easy to train .                                              |
| actively used in facebook                    | actively used in google                                      |
| dynamic generation of computational Graphs . | flexible and Detail Graphic Visualliser .                    |
| widely used in research projects.            | Keras with TensorFlow. to make things faster and build AI-related products ,much popular for learners |
| opensource                                   | opensource                                                   |
| has less features compared to tensorflow.    | has features like Flipping to check for a NAN and infinity . has packages . |

- **deep learning frameworks (packages)** : 

![](/home/duaa/Downloads/pyhon_packages.jpg)

* **Scikit-learn** is  user-friendly framework that contains a great variety of useful tools: **classification**, **regression** and **clustering** models. so it is the base Package 

* **Keras** is a high-level library that’s built on top of Theano or TensorFlow. It provides a scikit-learn type API (written in Python) for building Neural Networks. Developers can use Keras to quickly build neural networks .Keras supports almost all the models of a neural network – fully connected, convolutional, pooling, recurrent, embedding, 

* **Which one we can use** ? based on case we have. 

  i.e , If we  want to predict people’s opinion in movie reviews, then a deep learning approach using Keras with tensorflow  or PyTorch makes sense . or if we want to make classification base in images(input) so keras with tensorflow is better choice because it is provides layers and functions .

  but   if we  want to predict the price of future game tickets, then scikit-learn’s ability to crunch structured data is all you need.

* There are **pretrained models** (ML /DL)was built we can use it instead of build models from scratch. like CNN that used in image processing  (we can use it with keras_tensoflow) . etc..

- **OUR CASE** : 

what we want to do is **forecasting timeseries**  , The basic object of forecasting is the **time series**, which is a set of observations recorded over time. the observations are typically recorded with a regular frequency, like daily or monthly. A series is time dependent if its values can be predicted from the time they occured

- **linear regression model ** is widely used in practice and adapts naturally to even complex forecasting tasks.

The **linear regression** algorithm learns how to make a weighted sum from its input features. For two features, we would have:

```
target = weight_1 * feature_1 + weight_2 * feature_2 + bias
```

Linear regression with the time dummy produces the model:

```
target = weight * time + bias
```

The procedure for fitting a linear regression model follows the standard steps for scikit-learn. 

There are built Models(algorithms) that used in time series forcasting .

- **Time series forcasting models :**

1. ###### **Naïve, SNaïve**

2. **Seasonal decomposition (+ any model)**
3. **Exponential smoothing**
4. **ARIMA, SARIMA**
5. **GARCH**
6. **Dynamic linear models**
7. **TBATS**
8. **Prophet**
9. **NNETAR**
10. **LSTM**

the most 3 best algorithm for forecasting is ARIMA  , LSTM neural network, Facebook Prophet model.

| ARIMA                                                        | LSTM                                                         | PROPHET                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------- |
| 'AutoRegressive Integrated Moving Average' .The hard part of modeling Arima is to find the right parameters combination . | 'long-short term memory' is a type of recurrent neural netwok  built usin keras_tensoflow .during training it learns  . we need some processing. | follows the `sklearn` model API |

#### * we used prophet model .

#### **PROPHET**

is a procedure for forecasting time series data based on an  additive model where non-linear trends are fit with yearly, weekly, and  daily seasonality, plus holiday effects. It works best with time series  that have strong seasonal effects and several seasons of historical  data. Prophet is robust to missing data and shifts in the trend, and  typically handles outliers well.

Prophet follows the `sklearn` model API, We create an instance of the `Prophet` class and then call its `fit` and `predict` methods.

The Facebook Prophet model is composed of 3 componentes:

> y = trend + seasonality + holidays

Prophet.  We create an instance of the `Prophet` class and then call its `fit` and `predict` methods. the package takes a data frame as input (not a pandas Series) with 2 columns (ds with dates and y with values) The `y` column must be numeric, and represents the measurement we wish to forecast.



resources :

https://facebook.github.io/prophet/docs/quick_start.html

https://medium.com/analytics-vidhya/time-series-forecasting-arima-vs-lstm-vs-prophet-62241c203a3b

https://neptune.ai/blog/arima-vs-prophet-vs-lstm

https://www.kaggle.com/learn/time-series

