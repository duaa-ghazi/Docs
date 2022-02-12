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

