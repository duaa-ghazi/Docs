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

