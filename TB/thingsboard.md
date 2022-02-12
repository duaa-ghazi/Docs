Thingsboard :

* IOT : products(cars , industrial copmponent , sensors) combined with internet with data analytic . then they beacome IOT devices . So the network and computing extends to objects .
* thingsboard is opensource , IOT cloud improving , serverside for IOT application .

* there are relations between devices /customers/assets.

* collect data from devices and assets . then analyze data then trigger alarm /charts with complex event processing .

*  we control the device using RPC (remote procedure calls) . There is a workflow building [device event ,RestfulAPI ,RPC requests]

* all entities in thingsboard require time based UUID compatable with postgres time uuid .

* MultiTenancy : single plateform instance may run multiple application instances simultaniously .

* ```
  tenancy  #ايجار , tenant مستاجر  
  ```

* each application instance is isolated from other called seperate **tenant** . each tenant data are not availablr to other tenant . each tenant is created by system adminstrator .

* 3 level of users : 

  ```
  1-System ADMINSTRATOR :
  	he create the tenants entities and thier adminstrator users .
  2-Tenant ADMINSTRATOR :
   	able to do all kinds of operations with all thier entities 
  3-Customer  : 
  	they created by tenant and they have limited permissions , Able to access and control assigned devices that assigned by tenant adminstrator .
  
  ```

  * Multi Tenancy : 

    there are UI for each Admin / tenant ..  

    we add the user based in usecase :

    1- if we need IOT Solution developer then we creat system Adm .account .

    2- if 2 companies need to use plateform , then each company have tenant account and it can manage thier companies . 

  * the sys admin create tenant and to manipulate the tenant data it must create tenant admin and determine email for it . 

    *************************

    **Entities and Relations : 

    thingsboard supports anumber of entities help you transfer physical world objects into virtual environment .

    * **tenant  entity** : tenant is considers as entity , tenant refer to someone who owns or produces other entities (companies) [entities like : assesst/devices/dashboards/rulechains/alarms/customer]

      each tenant entity is combined to multiple tenant adm's accounts .

    * **customer entity** : customer is someone who use tenants devices or assests .

      (so the devices and assests is owned by tenants , so tenant introduces devices for his potential customers) . customer entity may contain unlimited number of customer users accounts . users(customers) can view dashboards and supervise entities .

    * **device entity** : devices entity is the stream telemetry and handle remote commands and has attributes. in common the particular connected thing is a device (sensors/switches/actuators) . in order to connect to a device , each device has a credential with different credential types . ( so device is always assign to tenant because the tenant is owner of this device).

      ex : local sensor networl , sensors devices are connected via blutooth or protocol to central device that collecting and pushing data to thingsboard , since the sensors is constraint and dont have ip connectivity  but the central device is connected to the internet and can push the data via singleMQTT connection .

    * **asset entity** : assets represent the environment where device is being installed  . include the building that the devices are located inside .and the other things inside the envirnoment . for example the agriculture vheciles is an asset .the asset also has telemtry and attributes and each device/assets has a type , but assets are not able to perform RPC commands  . and also the asset is owned by tenant admin . the tenant admin should assign assets and devices to paticular customer to make this entities visible for customer users in this customer . 

    * **relations** : custom relation are managed . each asset we can determine  arelation for it (ex : for which building ..)

      

      ex:![](/home/duaa/Pictures/thinsg1.png)                 

    * **Telemetry** :  telemetry features allows us to report process to work query and visulize . ex : device can report battery level ( it is from latest telemtry) and thingsboard visulize it on the dashboard or trigger alarm [ALARMS] . 

      -to have a telemtry report , we must connect device to plateform through protocols (using TCP/UDP based protocols) . like : 

      1- HTTP 2- MQTT 3- COAP .  ex : push data of device usong mqt protocol from command then the data battary level will appear in LATEST TELEMETRY .

      -telemtry maybe derived from group of devices . ex : we have couple of tempereture sensors (each of them is a device ) in the warehouse(it is an asset) .

      these sensors report telemetry individualy by combing this data (thingsboead can calculate the min / max tempereture in warehouse [Tmax ,Tmin] these will be an assetr telemetry that is derived from readings.) 

      

    * **Attribute feature** : allows to associate certain key value (parameters/attributes) with entities . ex : device model/serial number /temperature freq  . there are shared attributes and server attributes . 

      *Http request/response protocol not perfect to recieve real-time update . it is recommended to use MQTT for attribute update especailly if updates are frequently .

      attribute scopes :

      -> server attributes : for all entities ex : address of asset /HW version model/

      longitude-latitude , active .... the app of firmware that running on device cannot access this server attributes .

      -> client attributes : available for devices. it is reported by the applicaion of firmware running on  a device (like current firmware version / current upload freq)

      -> shared attributes : available for devices .it is something controlled by the server side but available for application or firmware running on device .this type is used mostly for configuration of the device .



* **Rule Engine** : we can control the datastream(telemetry)

   with rule engine feature . so rule engine validates the incoming telemetry then either stores it to the database or generates the alarm in case the data is not valid . each telemetry record is identified bt a unique key and value (combination of entity id ,timestamp ,key value) . so then we can query it and inside Rest API's[data query API] .

  => it is determine the logic of plateform 

  => enable filter /enrich/ transform messages originated by IOT devices/assets .

  => reporting alarming /communication with external systems.

  => complex event processing system based on **rule chain** 

  => rule chain defines the flow of incoming messages

  => there is a main rule chain recives all incoming messages by default called **root rule chain** 

  => root rule chain may validate in current messages and forward them into alarm rule chain (trigger lawrance and send them to notification rule chain that handle delivering of notification about alarms) .

  * **aliases** :  it is key -parameters for creating dashboards.

    Alias is a reference to a single entity or group of entities that are used in the widgets. for example we can reference alias for single device or reference one alias for  devices of a certain type or related to a certain asset.

    -> many aliases for different usecase based on filter type :

    1- single entity  2- entity list 3-entity name 4- device type ... 

  * **dashboard** : this used for data visualization and the device can be controlled by the UI . it is created by  a tenant admin's to give customer users access to the dashboard . so the tenant admin should assign the dashboard to specific customer . it is based on attributes and telemetry of entities .

    => consists of multiple views (state) 

    =>each state has number of widgets (exists on widget library(there are widget from tb and we can create custom widget   , Widgets are grouped into widget bundles. Each widget has a data source)) . so all things in dashboard built with blocks represented by digits(widgets which provide end user features (data visulization , remote device control , alarm management , display custom html content))

    after create dashboard we can create widget(each widget configured to display like chart) from wedget bundle. when create widget we can see select widget from widget bundle (current bundle : card / chart/ alarm .... )and inside them we  can select the the alias and the type of widget. 

    5 major type of widgets : 

    => **latest value** :to display most actual (current value) of particular entty atttribute or telemetry key (current state of chosen entity) . 

    latest exist in these widgets bundles : 1- analogue qauges 2- cards 3- chart 4- digital guges 5- gateway widgets  6- input widgets 7- maps .

    => **timeseries** :to display historical data of specific entity in range of time (telemetry data) 

    latest timeseries in these widgets bundles : 1-chart . . 

    => RPC ,**control widget** : to send RPC commands to device manipulate and handle visualize response from the entity 

    => **ALarm widgets** : display alerts  related to specify entity  .
  
    => **static widgets** : is represented by HTML code (does not use any data source )







