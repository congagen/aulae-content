
## Content

AULAE supports two ways to provide content:

* ****Static JSON files:**** You can host a JSON file containing your AR content on a web server.
* ****REST APIs:****  For more dynamic content, you can create a REST API that AULAE will query.

### JSON Feed Structure

Whether you use a static file or a REST API, the structure of the JSON data remains the same:

****1. Feed Metadata (Required)****
This section provides information about the feed as a whole.

```json
{
"id": "",  // Unique ID for the feed
"name": "",  // Feed name
"info": "",  // Feed description (Lib view feed subtitle)
"version": 0,  // Version number (Affects updates)
"updated_utx": 0,  // Unix timestamp of last update (Affects updates)
"thumb_url": ""  // URL of an image representing the feed
}
```

****2. Feed Content (Optional)****

The content field contains an object where each key represents an item to be displayed in the AR viewport and map.

Each content item has the following properties:

```json
{
    "content": {
        "1": {  // Key
            "name": "", // Object name (Action menu subtitle)
            "type": "", // Content type ("image", "gif", "usdz", "text", "marker", "audio")
            "url": "",  // Content URL
            "info": "", // Object information (Action menu item)
            "chat_url": "", // REST API endpoint (Action menu item)
            "world_position": true, // Controls lat/long/alt vs x/y/z positioning
            "lat": 0.0, // Object Latitude
            "lng": 0.0, // Object Longitude
            "alt": 0.0, // Object Altitude
            "x_pos": 0.0, // Object X Position (Left/Right)
            "y_pos": 0.0, // Object Y Position (Up/Down)
            "z_pos": 0.0, // Object Z Position (Front/Back)
            "billboard": true,  // Controls billboard object orientation
            "scale": 1.0, // Object scale
            "content_link": "https://www.google.com" // URL to open in a web browser (Action menu item)
        }
    }
}
```

****Example:****
```json
{
    "id":  "a1b2c3d4",
    "name":  "Demo Feed",
    "info":  "USDZ 3D Object",
    "version": 0,
    "updated_utx": 0,
    "thumb_url": "https://aulae-examples.s3.amazonaws.com/sources/usdz/FeedLogo.png",

    "content": {
        "01": {
            "name": "3D Model 1",
            "type": "usdz",
            "info": "",
            "url": "https://s3.amazonaws.com/aulae-examples/content/Usdz/LogoCube.usdz",
            "content_link": "https://www.timsandgren.com",
            "chat_url": "https://suoccr4nm0.execute-api.us-east-1.amazonaws.com/dev",
            "world_position": false,
            "billboard": false,
            "x_pos": 0,
            "y_pos": 0,
            "z_pos": 0,
            "world_scale": false,
            "scale":  20.0
        },

        "02": {
            "name": "3D Model 2",
            "type": "usdz",
            "info": "",
            "url": "https://s3.amazonaws.com/aulae-examples/content/Usdz/LogoCube.usdz",
            "content_link": "https://www.timsandgren.com",
            "chat_url": "https://suoccr4nm0.execute-api.us-east-1.amazonaws.com/dev",
            "world_position": false,
            "billboard": false,
            "x_pos": 0,
            "y_pos": 0,
            "z_pos": 0,
            "world_scale": false,
            "scale":  40.0
        }
    }
}

```

### Chat Endpoints

****Receiving Chat Messages (AULAE -> REST API)****

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

****Sending Chat Messages (REST API -> AULAE)****

AULAE expects a response formatted like so:

```json
{
    "chat_msg": "This is a message from the API",
    "sid": "",
    "username": ""
}
```
