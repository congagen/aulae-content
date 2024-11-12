

### Receiving Chat Messages (AULAE -> REST API)

When the user sends a message, a `POST` request is made to your specified ("chat_url") 
endpoint with the following JSON payload:

```json
{
  "chat_msg": "", 
  "sid": "",
  "username": "",
  "lat": "",
  "lng": "" 
}
```


### Sending Chat Messages (REST API -> AULAE)

AULAE expects a response formatted like so:

```json
{
  "chat_msg": "This is a message from the API",
  "sid": "", 
  "username": "" 
}
```
