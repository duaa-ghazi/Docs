***Microservices using spring boot and spring cloud .***

![](/home/duaa/Downloads/m1.png)

if we start with monolithic projects and then this project big , it hard for us to deploy it . also when team need to push app to  production they will also will be taking the all tems changes to production .  so microservice allow us to focus on subset of entire application and deploy each subset independently be cause things are not coupled  .

* we use different databases/ technologies for each microservice (subset).

* in right of figure there is public internet and clients request we have load balancer . 

* load balancer is the main entry point ,client dont have directly talking with services , beacuse the services should be withen private network .

* load balancer is responsible to routing to the corresbonding service based on path , then the load balancer send requests to services .

* all of this is powered by eureka server , we will not deal with ports for services we need centerized place , where all clients register to server (here  it is the eurika server ) . to need to communicate with service we need to specify the name of service .

* config server : to store configuration of development ,predection ,test environment .

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

    *   the dependency management : this containes dependencies that all microservice(modules) can pick whatever dependency they need (same version from it ).  like "spring-boot-dependencies" and "spring-cloud-dependencies"

    * the dependencies that between dependenciese tag in parent pom ,the all sub modules by default have these dependencies without need to put them inside modules pom (it will be inside dependencies folder) like : lombok and spring test.

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

* create mocroservice (submodule) :

  1.  ->new module(from parent folder)-> mavenproject-> name of microservice .

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

  2- opern feign

  * rest template : we make bean then use it inside service (inside microservice) like this :

    ```java
    FraudCheckResponse fraudCheckResponse = restTemplate.getForObject(
                    "http://localhost:8081/api/vi/fraud-check/{customerId}",     //uri
                    FraudCheckResponse.class, // return response
                    customer.getId()); //uri variables
    ```

    ******************************************

    * the service may running in more than one port (more than instance can run ) but the other service if they want to connect with it , they  need to know all ports of it  this b*

    

    Eurika server : 

     this for service discovery , 

    register : when a service register to eureka server , eureka server will know the exact information where service is running (the host and the port).

    lookup then connect: when a service need to communicate with other service , it lookup to eureka server then it can connect to service they need , this how they connect to other 

    

