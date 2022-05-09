prediction Io

* Apache PredictionIO® is an **open source Machine Learning Server**

*  is built atop Spark and Hadoop

* Apps send data to PredictionIO’s event server to train a model, then query the engine for predictions based on the model.

* Data can be stored in a variety of back ends: JDBC, Elasticsearch ..

* PredictionIO’s  has templates  ,Some existing templates include:

  - [A universal recommendation engine.](https://github.com/actionml/universal-recommender)

  - [Text classification](https://github.com/apache/incubator-predictionio-template-text-classifier).

  - [Survival analysis](https://github.com/goliasz/pio-template-sr) (for time-between-failure predictions).

  - [Labeling topics using Wikipedia as a knowledge base.](https://github.com/peoplehum/template-Labelling-Topics-with-wikipedia)

  - [Similarity analysis.](https://github.com/ramaboo/template-scala-parallel-similarproduct-with-rating)

    

  Hadoop is an open-source framework that allows to store and process big data in a distributed environment across clusters of computers using simple programming models. It is designed to scale up from single servers to thousands of machines, each offering local computation and storage.

  This brief tutorial provides a quick introduction to Big Data, MapReduce algorithm, and Hadoop Distributed File System.

Spark was introduced by Apache Software Foundation for speeding up the Hadoop computational computing software process.

Spark uses Hadoop in two ways – one is **storage** and second is **processing**. Since Spark has its own cluster management computation, it uses Hadoop for storage purpose only.

in order to provide the best recommendations engine, we decided to make a plugin for PredictionIO.

step1: install PredictionIO with the Universal Recommender We’ll use one of its templates called Recommendation to build a working recommendation engine .

The [template gallery](https://predictionio.incubator.apache.org/gallery/template-gallery) consists many templates for recommendation, classification, regression, natural language processing, and many more. 

https://predictionio.apache.org/datacollection/eventapi/#note-about-properties

https://predictionio.apache.org/templates/ecommercerecommendation/dase/

http://clouddatafacts.com/pio/recommendation-als.html#recommendation-engine

https://github.com/apache/predictionio/tree/develop/docker#tutorial

https://predictionio.apache.org/install/install-docker/

https://docs.huihoo.com/predictionio/docs.prediction.io/install/install-linux/index.html

https://predictionio.apache.org/datacollection/

https://predictionio.apache.org/appintegration/

https://predictionio.apache.org/templates/javaecommercerecommendation/quickstart/







http://localhost:7070/events.json?accessKey=dSW-HsymjfURJD8lCweVteJ4JAnYwmTCrgQu5AiLwofnNT8-x_Ewcfd5EZSDsc9U&limit=-1