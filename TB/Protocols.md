Protocols :

1- HTTP : 

 https://thingsboard.io/docs/reference/http-api/#telemetry-upload-api

https://thingsboard.io/docs/getting-started-guides/helloworld/

```bash
curl -v -X POST -d "{\"temperature\": 25}" $HOST_NAME/api/v1/$ACCESS_TOKEN/telemetry --header "Content-Type:application/json"
#access token device credentials 
```

```bash
curl -v -X POST -d "{\"temperature\": 25}" https://demo.thingsboard.io/api/v1/$ACCESS_TOKEN/telemetry --header "Content-Type:application/json" 
```



***********

* to run the LWM2M device . 

  1- login with tenant that was created by customer .

  2- in Resource library we must add the xml file (this used when connect) 

  called (3-1_1.xml)Note : the lwm2m version must be correct (1.1)

  3- create device profile with with lwm2m protocol and the xml model inside LWM2M model.

  4-   in transport config of device profile : 

     a- LWM2M model : check attributes and telemetry(this will show and get from xml file ) .

  ​	b- bootstrap : -> LWM2M Server  we choose pre shard key (this cahnge port to 5686) .  Bootstrap Server : we choose pre shard key (this cahnge port to 5688)

  . we use bootstrap server key if we choose  bootstrap server  when we connect the LWM2M device . if we not use it we will use the server direct (Note : keys for security) 

  

  5- create device and assign the created device profile to it .  

  6-  choose the client ( device that can connect to lwm2m server ) which we created in prevoius step so go to device then in manage credentials :

  ​	a- in client security config : 

  ​	  -  add endpoint client name

  ​	  - choose security config as we choose   it in servers (pre-shared key)

  ​	- client identity : ( it is generated) but we can change it (usualy as endpoint client   	   name) we use it when we connect this client (device) .

  ​	- client key : it is generated . we use it also when we connect device .

     b - in bootstrap client : in both bootstrap server and LWM2M FILL (pre-shared key )

  and the client public key or identity ( client identity as in point a).

  

  7- connect device ( in terminal )  , there is a jar file (simulater then use to connect the device with servers) so go to directory of this jar .

  ```shell
  $ java -jar ./leshan-client-demo.jar -u localhost:5688 -b -n li -i li -p 39cf425296ed574d39cf425296ed574d
  # -b : indicates that we choose bootstrap server 
  # -n : the endpoint client name
  # -i : the client identity 
  # -p : the client key . 
  ```

  

////////////////////

* to run coap :

   connect device ( in terminal )  

  ```sh
  //to send telemetry 
  $ cat telemetry-data-as-object.json | coap post coap://localhost/api/v1/$ACCESS_TOKEN/telemetry
  
  //to send attribute
  $ cat telemetry-data-as-object.json | coap post coap://localhost/api/v1/$ACCESS_TOKEN/attributes
  ```

  ```
  // the json body (this is the telemetry or attribute )
  {
    "stringKey": "value1",
    "booleanKey": true,
    "doubleKey": 42.0,
    "longKey": 73,
    "jsonKey": {
      "someNumber": 42,
      "someArray": [1,2,3],
      "someNestedObject": {"key": "value"}
    }
  }
  ```

