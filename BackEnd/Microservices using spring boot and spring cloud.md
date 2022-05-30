---
typora-copy-images-to: microservice-img
typora-root-url: microservice-img
---

***Microservices using spring boot and spring cloud .***

![](/ms1.png)

if we start with monolithic projects and then this project big , it hard for us to deploy it . also when team need to push app to  production the y will also will be taking the all terms changes to production .  so microservice allow us to focus on subset of entire application and deploy each subset independently be cause things are not coupled  .

* we use different databases/ technologies for each microservice (subset).

* in right of figure there is public Internet and clients request we have load balancer . 

* load balancer is the main entry point ,client don't have directly talking with services , because the services should be withen private network .

* load balancer is responsible to routing to the corresponding service based on path , then the load balancer send requests to services .

* all of this is powered by eureka server , we will not deal with ports for services we need centralized place , where all clients register to server (here  it is the eureka server ) . to need to communicate with service we need to specify the name of service .

* config server : to store configuration of development ,prediction ,test environment .

* config server and eurika server is taken by kubernates .

  ****************************************************

  *** Maven : 

  * Maven's primary goal is to allow a developer to comprehend the complete state of a development effort in the shortest period of time.  Maven deals with several areas of concern:

    - Making the build process easy
    - Providing a uniform build system
    - Providing quality project information
    - Encouraging better development practices

  * Maven builds a project using its project object model (POM) and a set of plugins. 

  * create a maven project from cmd :

    ```sh
    $ mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4 -DinteractiveMode=false
    #artifactId:  project Name 
    #groupId: organization name
    
    $tree 
    #the output is a folder structure .
    ```

    *   the dependency management : this contains dependencies that all microservice(modules) can pick whatever dependency they need (same version from it ).  like "spring-boot-dependencies" and "spring-cloud-dependencies"

    * the dependencies that between dependencies tag in parent pom ,the all sub modules by default have these dependencies without need to put them inside modules pom (it will be inside dependencies folder) like : lombok and spring test.

      ```xml
        <!-- in parent pom.xml -->
      <dependencyManagement>
          <dependencies>
            <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-dependencies</artifactId>
              <version>${spring.boot.dependencies.version}</version>
              <scope>import</scope>
              <type>pom</type>
            </dependency>
          </dependencies>
        </dependencyManagement>
      
       <dependencies>
          <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
          </dependency>
          <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
          </dependency>
        </dependencies>
      ```

      ```xml
      <!-- in modeule pom.xml-->
      <dependencies>
              <dependency>
                  <groupId>org.springframework.boot</groupId>
                  <artifactId>spring-boot-starter-web</artifactId>
              </dependency><!--from parent-->
              <dependency>
                  <groupId>org.springframework.boot</groupId>
                  <artifactId>spring-boot-starter-data-jpa</artifactId> <!--from parent-->
              </dependency>
          </dependencies>
      ```

      * the same concept for plugins . plugin dependency management contains  dependencies that can modules pick from it . ..

        



****************************************

* create microservice (submodule) :

  1.  ->new module(from parent folder)-> maven project-> name of microservice .

  2. this module will be added inside <modules> inside parent pom.xml.

  3. inside module pom.xml the <parent> will be added with its info .

     

* ****************

  create application.yml: we put server info and port . and spring  datasourse with info for db . put it inside resource folder . this application.yml is for each microservice

* create banner.txt , from springboot banner generator editer put it inside resource folder.

* we can create docker-compose.yml and put inside it all services (sql,kafka...) and run it in one command 

  ```bash
  $docker-compose up . 
  ```

  or create yaml file for each service and run each yaml by 

  ```bash
  $docker-compose -f (pathto)nameofyanl.yml up. 
  ```

  * we put mysql service . and put the image version (this service used to connenct tho sql server and then wa can make a dbs (schemas) and connect to it ).

    

  

  

*************

*  in pom.xml in each module we pick these dependencies from parent . 

  spring-boot-starter-web : to make us make restfull api's .

  spring-boot-data-jpa : to allows us to perform queries and interact with db 

  ```yaml
  <dependencies>
  <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-web</artifactId>
   </dependency>
  <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
        </dependencies>
  
  ```

* in pom.xml in each module we pick these dependencies from parent , we put the driver of the db that we used .

  ```yaml
      <dependencies>
          <dependency>
              <groupId>mysql</groupId>
              <artifactId>mysql-connector-java</artifactId>
          </dependency>
      </dependencies>
  ```

  *****************

  * make Module 2 : name (Fruad)

  * database service in docker-compose.yml we can use it in different microservice (module)  and connect each module to defferent(schema) or same schema .

  * ```java
    //Note
    customer =...
    repository.saveAndFlush(customer) //this save the customer and get the id to it . without need to define new one .
    ```

**********

* if 2 modules(2 services) need to communicate with each other (using apis) we can use

  ![](/home/duaa/Desktop/communicate.png)

  1- rest template 

  2- open feign

  * rest template : we make bean then use it inside service (inside microservice) like this :

    ```java
    FraudCheckResponse fraudCheckResponse = restTemplate.getForObject(
                    "http://localhost:8081/api/vi/fraud-check/{customerId}",     //uri
                    FraudCheckResponse.class, // return response
                    customer.getId()); //uri variables
    ```

    ******************************************

    * the service may running in more than one port (more than instance can run ) but the other service if they want to connect with it , they  need to know all ports of it  this b*

      ![](/ms1.png)

    

    



Note : in java 15 we can use record instead of class ( we can put fields as argument to class in header this similar to lombok but build in java 15 and above so we don't need dependency ... , this create constructor with this fields + getter as the name of them ) like following . 

 

```java
public record CustomerRegistrationRequest(
        String firstName, String lastName ,String email) {
}
request.firstName() // as get method

```

```java
    
// but we will not use it because we use java 11 like this
@Data
@Builder
public class CustomerRegistrationRequest {
    String firstName;
    String lastName ;
    String email;
}

```

**Eureka server :** 

 this for service discovery , 

**register** : when a service register to eureka server , eureka server will know the exact information where service is running (the host and the port).

**lookup then connect**: when a service need to communicate with other service , it lookup to eureka server then it can connect to service they need , this how they connect to other 



![](/ms2.png)

******************



![](/ms3.png)



*******************

![](/ms6.png)



![](/ms7.png)



![](/ms8.png)



![](/ms9.png)



***************

note #Z1 : If `spring-cloud-sleuth-zipkin` is available then the app will generate and report [Zipkin](https://zipkin.io/)-compatible traces via HTTP. By default it sends them to a Zipkin collector service on localhost (port 9411). Configure the location of the service using `spring.zipkin.baseUrl`

https://docs.spring.io/spring-cloud-sleuth/docs/current/reference/html/getting-started.html#getting-started-terminology

![](/ms10.png)



![](/mss1.png)                                                                                                                                                                                                                                                                                                                       

***********

docker logs zipkin 

![](/mss2.png)

![](/mss3.png)



![](/mss5.png)

*************

![](/mss6.png)

![](/mss7.png)

![](/mss8.png)



![](/mss9.png)



////////

![](/mss10.png)



![](/mss11.png)



![](/mss13.png)

![](/mss14.png)

![](/mss15.png)

![](/mss16.png)

![](/mss18.png)

![](/msss1.png)

**Links**

- [https://kafka.apache.org](https://kafka.apache.org/)
- [https://www.rabbitmq.com](https://www.rabbitmq.com/)
- https://aws.amazon.com/sqs





RabbitMQ is a solid, general-purpose **message broker** that supports several protocols such as AMQP, MQTT, STOMP, etc. It can handle high throughput. A common use case for RabbitMQ is to handle background jobs or long-running task, such as [file scanning](https://www.cloudamqp.com/blog/2019-01-18-softonic-userstory-rabbitmq-eventbased-communication.html), image scaling or PDF conversion. RabbitMQ is also used between microservices, where it serves as a means of communicating between applications, avoiding bottlenecks passing messages.

Kafka is a message bus optimized for **high-throughput ingestion data streams** and replay. Use Kafka when you have the need to move a large amount of data, process data in real-time or analyze data over a time period. In other words, where data need to be collected, stored, and handled. An example is when you want to track user activity on a webshop and generate suggested items to buy. Another example is data analysis for tracking, ingestion, logging or security.

Kafka can be seen as a **durable message broker** where applications can process and re-process streamed data on disk. Kafka has a very simple routing approach. RabbitMQ has better options if you need to route your messages in complex ways to your consumers. Use Kafka if you need to support batch consumers that could be offline or consumers that want messages at low latency. 

In order to understand how to read data from Kafka, we first need to understand its consumers and consumer groups. Partitions allow you to parallelize a topic by splitting the data across multiple nodes. Each record in a partition is assigned and identified by its unique offset. This offset points to the record in a partition. In the latest version of Kafka, Kafka maintains a numerical offset for each record in a partition. A consumer in Kafka can either automatically commit offsets periodically, or it can choose to control this committed position manually. RabbitMQ will keep all states about consumed/acknowledged/unacknowledged messages. I find Kafka more complex to understand than the case of RabbitMQ, where the message is simply removed from the queue once it's acked.

RabbitMQ's queues are fastest when they're empty, while Kafka retains large amounts of data with very little overhead - Kafka is designed for holding and distributing large volumes of messages. (If you plan to have very long queues in RabbitMQ you could have a look at [lazy queues](https://www.rabbitmq.com/lazy-queues.html).)

Kafka is built from the ground up with horizontal scaling (scale by adding more machines) in mind, while RabbitMQ is mostly designed for vertical scaling (scale by adding more power).

RabbitMQ has a built-in user-friendly interface that lets you monitor and handle your RabbitMQ server from a web browser. Among other things, queues, connections, channels, exchanges, users and user permissions can be handled - created, deleted and listed in the browser and you can monitor message rates and send/receive messages manually. Kafka has a number of [open-source tools, and also some commercial ones](https://medium.com/@giorgosmyrianthous/overview-of-ui-monitoring-tools-for-apache-kafka-clusters-9ca516c165bd), offering the administration and monitoring functionalities. I would say that it's easier/gets faster to get a good understanding of RabbitMQ.

In general, if you want a simple/traditional pub-sub message broker, the obvious choice is RabbitMQ, as it will most probably scale more than you will ever need it to scale. I would have chosen RabbitMQ if my requirements were simple enough to deal with system communication through channels/queues, and where retention and streaming is not a requirement.

**There are two main situations where I would choose RabbitMQ; For long-running tasks, when I need to run reliable background jobs. And for communication and integration within, and between applications, i.e as middleman between microservices**; where a system simply needs to notify another part of the system to start to work on a task, like ordering handling in a webshop (order placed, update order status, send order, payment, etc.).

**In general, if you want a framework for storing, reading (re-reading), and analyzing streaming data, use Apache Kafka.** It’s ideal for systems that are audited or those that need to store messages permanently. These can also be broken down into two main use cases for analyzing data (tracking, ingestion, logging, security etc.) or real-time processing.

![](/msss2.png)

