# Flask Framework  

* **why we want  python Framework :** 

Deploying models should be the last stage in building any project in the field of machine learning(forecasting time series data in our case). So, it should expose the model as a REST service. 

There is a set of frameworks written in Python including Flask, Tornado, Pyramid,and Django,. A framework "is a code library that provides building reliable, scalable and maintainable web applications". 

- **Flask and Django**: 

Flask and Django are the most used . Django  is a high-level web framework which allows performing rapid development. The primary goal of this web framework is to create complex database-driven websites. URL dispatcher of the Flask web framework is a RESTful request on the other hand, URL dispatcher of Django framework is based on controller-regex so i decide to choose Flask .

The framework I chose is a flask, it is a micro-framework but easy to use, quick to learn, flexible with creating applications. Flask is not only a framework, but it also has an HTTP web server, also has APIs/functions using to create our REST API (service) in Python.

- **Flask startup and configuration:**

i installed python3, pip, Flask, and used them with PyCharm integrated development
environment (IDE). First, I create an Application object, which is an instance of the Flask
object that used to create functions. i created it by using decorator @ app. route ('/') to
define some routes (a compact set of API endpoints) to tell our flask app which URL should
trigger the requested function/API.



resources : 

https://flask.palletsprojects.com/en/2.0.x/

https://linuxconfig.org/how-to-install-pycharm-on-ubuntu-20-04-linux-desktop

https://medium.com/@mushtaque87/flask-in-pycharm-community-edition-c0f68400d91e

https://programminghistorian.org/en/lessons/creating-apis-with-python-and-flask
