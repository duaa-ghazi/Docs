thingsboard - terminal : 

1- to install db , first we create it then we run this file from target/install/bin : 

```
sudo chmod +x  install_dev_db.sh 
sudo ./install_dev_db.sh 
```

2- to make upgrade to db : from data /upgrade (there are sql scripts files) , inside target/install/bin :

```
sudo chmod +x upgrade_dev_db.sh 
sudo ./upgrade_dev_db.sh --fromVersion=3.3.2
```



***************************

to run thingsboard for first time  : 

1- we must create keycloak db in postgres(this for save user and realm data) , then  run docker compose keycloack.yml without the realm config (without comments) . then we must comment them when we run it again to avoid override the realm config . there is a  config folder that keycloak has a volums with it . (Note : inside folder called docker tb) . to login to keyclaok we must create the admin of the realm which is created and assign to it the mappers and credential (realm-admin@emaas.net pass : root@124Asc) (this user , real-managemaent + account : select all things )

2- create thingsboard2 db (as in application.yml) then install db with all sql as note 1 above

3- mvn clean install -DskipTests -pl '!ui-ngx','!:web-ui' for all app (Thingsboard not application)

***************

to run ui 

```
$yarn start clean && yarn install && yarn start 
#for first time (this clean and remove the ngmodule and install dependecies and build+start the project) 
$yarn start # for later

```



************

* to install coap

  ```
  npm i coap
  ```

* the node version must be 16.13.x

  ```
  $nvm install 16.13 # to install node 
  $node --version  # version of node
  $ng --version #version of angular
  $nvm use 16.13.2 # to use it inside project
  $nvm alias default 16.13.2 # to make it use globally as default
  
  
  ```

  

* there are system admin ( we can login to ui with it to create tenant ) , when we create tenant ,it will be added to users . then we can login with this tenant to create device ,etc.. 

  ( system admin : sysadmin@emaas.net , pass:123) for all .

  created tenant (for me) :  (duaa@emaas.net ,  pass:123)

  

