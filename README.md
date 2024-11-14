
## Content

AULAE supports two ways to provide content:

* ****Static JSON files:**** You can host a JSON file containing your AR content on a web server.
* ****REST APIs:****  For more dynamic content, you can create a REST API that AULAE will query.

### Feed Structure

Whether you use a static file or a REST API, the structure of the JSON data remains the same:

****1. Feed Metadata (Required)****
This section provides information about the feed as a whole.

```json
{
"id": "",  // Unique ID for the feed
"name": "",  // Feed name
"info": "",  // Feed description (Lib view feed subtitle)
"version": 0,  // Version number (Effects updates)
"updated_utx": 0,  // Unix timestamp of last update (Effects updates)
"thumb_url": ""  // URL of an image representing the feed ()
}
```

****2. Feed Content (Optional)****

The content field contains an object where each key represents an item to be displayed in the AR viewport and map.

Each content item has the following properties:

```json
{
    "content": {
        "1": {
            "name": "", // Item name (Action menu subtitle and chat username)
            "type": "", // Content type ("image", "gif", "usdz", "text", "marker", "audio")
            "url": "",  // Content URL
            "info": "", // Item information (Action menu item)
            "chat_url": "", // REST API chat endpoint (Action menu item)
            "world_scale": true, // Toggles distance scaling / static
            "world_position": true, // Controls lat/long/alt vs x/y/z positioning
            "radius": 100, // The distance from which the item will be visable in the viewport (requires lat/long)
            "text": "", // Text for text items
            "font": "", // Font name for text items
            "hex_color": "7122e8", // Color for text and marker items
            "lat": 0.0, // Item Latitude
            "lng": 0.0, // Item Longitude
            "alt": 0.0, // Item Altitude
            "x_pos": 0.0, // Item X Position (Left/Right)
            "y_pos": 0.0, // Item Y Position (Up/Down)
            "z_pos": 0.0, // Item Z Position (Front/Back)
            "billboard": true,  // Toggles billboard item orientation
            "scale": 1.0, // Item scale
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
    "thumb_url": "",

    "content": {
        "01": {
            "name": "3D Model 1",
            "info": "",
            "type": "usdz",
            "url": "https://s3.amazonaws.com/aulae-examples/content/Usdz/LogoCube.usdz",
            "chat_url": "https://suoccr4nm0.execute-api.us-east-1.amazonaws.com/dev",
            "content_link": "https://www.timsandgren.com",
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
            "info": "",
            "type": "usdz",
            "url": "https://s3.amazonaws.com/aulae-examples/content/Usdz/LogoCube.usdz",
            "chat_url": "https://suoccr4nm0.execute-api.us-east-1.amazonaws.com/dev",
            "content_link": "https://www.timsandgren.com",
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


## Chat Endpoints

****Receiving Chat Messages (AULAE -> REST API)****

When the user sends a message, a `POST` request is made to your specified ("chat_url") endpoint with the 
following JSON payload:
  
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
