## Content

### Supported File Formats

* Images: JPG, PNG
* Animation: GIF, USDZ
* 3D Models: USDZ
* Audio: MP3

### JSON File Structure

AULAE understands content with the following fields:

**Collection Metadata**

| Field        | Type   | Default | Description                      |
|--------------|--------|---------|----------------------------------|
| `id`         | String | ""      | Unique ID for the collection     |
| `name`       | String | ""      | Collection name                 |
| `version`    | String | ""      | Version number (for updates)    |
| `updated_utx`| Number | 0       | Unix timestamp of last update | 
| `info`       | String | ""      | Collection description           |
| `thumb_url`  | String | ""      | URL of an image representing the collection |

**Content Objects (`content`)**

The `content` field contains an object where each key represents an item to be displayed in the AR viewport. Each content item has the following properties:

| Field                     | Type    | Default  | Description                                                                                                            | Options                                           |
|---------------------------|---------|----------|------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------|
| `name`                    | String  | ""       | Object name                                                                                                            |                                                   |
| `info`                    | String  | ""       | Object information                                                                                                     |                                                   |
| `type`                    | String  | "marker" | Content type                                                                                                           | "image", "gif", "usdz", "text", "marker", "audio" |
| `url`                     | String  | ""       | Content URL                                                                                                            |                                                   |
| `scale`                   | Number  | 1.0      | Object scale                                                                                                           |                                                   |
| `world_scale`             | Boolean | `true`   | Distance scaling (if `true`, scale with distance) / Static (if `false`)                                                |                                                   |
| `world_position`          | Boolean | `true`   | Use latitude/longitude/altitude (`true`) or XYZ (`false`) for positioning                                              |                                                   |
| `lat`, `lng`, `alt`       | Number  | 0.0      | Latitude / Longitude / Altitude position                                                                               |                                                   |
| `x_pos`, `y_pos`, `z_pos` | Number  | 0.0      | X, Y, Z position (used if `world_position` is `false` or if world positioning is disabled in app settings)             |                                                   |
| `radius`                  | Number  | 0        | View radius (requires `lat` and `lng`, defines the distance from which content is visible)                             |                                                   |
| `billboard`               | Boolean | `true`   | Toggles billboard mode (always faces the camera)                                                                       |                                                   |
| `instance`                | Boolean | `false`  | Reuse local content if present (e.g., if a USDZ model with the same `url` is already loaded, reuse that instance instead of downloading it again)                          |
| `content_link`            | String  | ""       | Action menu option - URL to open in a web browser when the user interacts with the content                             |                                                   |
| `hex_color`               | String  | "7122e8" | Color for text and marker objects                                                                                      |                                                   |
| `text`                    | String  | ""       | Text content for text objects                                                                                          |                                                   |
| `font`                    | String  | ""       | Font for text objects                                                                                                  |                                                   |
| `chat_url`                | String  | ""       | The `chat_url` should point to a chat service that supports this integration.                                          |                                                   |


**Example:**

```json
{
  "id": "museum-tour",
  "name": "Museum Exhibit",
  "info": "AR experience for the museum's ancient Egypt exhibit",
  "version": "1.2",
  "updated_utx": 1678886400, 
  "thumb_url": "[invalid URL removed]",

  "content": {
    "Sarcophagus": {
      "name": "King Tut's Sarcophagus",
      "type": "usdz",
      "url": "[invalid URL removed]",
      "info": "Learn more about this ancient Egyptian sarcophagus.",
      "world_position": true,
      "lat": 37.7749, 
      "lng": -122.4194,
      "alt": 10, 
      "scale": 0.5,
      "content_link": "[invalid URL removed]" 
    },
    "Hieroglyphs": {
      "name": "Decipher the Hieroglyphs",
      "type": "image",
      "url": "[invalid URL removed]",
      "info": "Can you translate these ancient symbols?",
      "world_position": false,
      "x_pos": 0,
      "y_pos": 1,
      "z_pos": -2,
      "billboard": true 
    }
  }
}
