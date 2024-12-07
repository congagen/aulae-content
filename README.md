
## Content

AULAE supports two ways to provide content:

* ****Static JSON files:**** JSON files on web servers.
* ****REST APIs:**** REST APIs that AULAE can query.

### Feed Structure

Whether you use a static file or a REST API, the structure of the JSON data remains the same:

****1. Feed Metadata (Required)****
This section provides information about the feed as a whole.

```json
{
"id": "",  // Unique ID for the feed
"name": "",  // Feed name (Appears throughout the app)
"info": "",  // Feed subtitle (Lib view feed subtitle)
"version": 0,  // Version number (Effects updates)
"updated_utx": 0,  // Unix timestamp of last update (Effects updates)
"thumb_url": ""  // URL of an image representing the feed (Visible in feed managemnt views, Optional)
}
```

****2. Feed Content (Optional)****

The content field contains an object where each key represents an item to be displayed in the viewport and map.
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
            "world_scale": true, // Toggles distance based/static scaling
            "world_position": true, // Toggles lat/long/alt vs x/y/z item positioning
            "radius": 100, // The distance from which the item will be visable in the viewport (Requires lat/long)
            "text": "", // Text for text items
            "font": "", // Font name for text items
            "extrusion": 1, // Extrusion depth for text items
            "hex_color": "7122e8", // Color for text and marker items
            "lat": 0.0, // Item Latitude
            "lng": 0.0, // Item Longitude
            "alt": 0.0, // Item Altitude
            "x_pos": 0.0, // Item X Position (Left/Right) 
            "y_pos": 0.0, // Item Y Position (Up/Down)
            "z_pos": 0.0, // Item Z Position (Front/Back)
            "billboard": true, // Toggles billboard item orientation
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
            "name": "3D Object",
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
            "name": "Text Object",
            "info": "",
            "type": "text",
            "text": "(ﾉ◕ヮ◕)ﾉ*:･ﾟ✧",
            "extrusion": 2,
            "url": "",
            "chat_url": "https://suoccr4nm0.execute-api.us-east-1.amazonaws.com/dev",
            "content_link": "https://www.timsandgren.com",
            "world_position": false,
            "billboard": false,
            "x_pos": 0,
            "y_pos": 0,
            "z_pos": 3,
            "world_scale": false,
            "scale":  1
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
    "client_username": "", 
    "chat_msg": "",
    "sid": "", 
    "lat": "0.0", 
    "lng": "0.0", 
    "alt": "0.0"  
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
