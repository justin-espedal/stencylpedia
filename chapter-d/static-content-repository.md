# Static Content Repository

Store assets on a remote server. This server can be shared with others to allow them to access your content from within Stencyl.

### Content Types:

Each type of content has an id, lowercase letters delimited by dots:

| Content Type ID         | Description                    |
|-------------------------|--------------------------------|
| stencyl.ext.engine      | Engine Extension               |
| stencyl.ext.toolset     | Toolset Extension              |
| stencyl.lib.actortype   | Actor Type                     |
| stencyl.lib.background  | Background                     |
| stencyl.lib.font        | Font                           |
| stencyl.lib.scene       | Scene                          |
| stencyl.lib.sound       | Sound                          |
| stencyl.lib.tileset     | Tileset                        |
| stencyl.lib.code        | Behavior or Code               |
| stencyl.game            | Game                           |
| stencyl.kit             | Kit                            |
| file.png                | PNG Image                      |
| file.txt                | Text File                      |
| com.polydes.dialog.font | Custom Extension-Specific Type |

`{base url}`: the url provided to others to access the repository

### Static Repository Access
- Found at `{base url}/` index page

```json
{
  "repository_type": "static",
  "version": 1
}
```

### Type Listing
- Found at `{base url}/static/content_types.txt`
- Lists content types available on this repository.

Example:
```
stencyl.ext.engine
stencyl.ext.toolset
```

### Resource Listing
- Found at `{base url}/static/{content type id}/list.txt`
- Lists the unique id of each available resource of this type.

Example:
```
com.polydes.datastruct
com.polydes.dialog
```

### Resource
- A folder, found at `{base url}/static/{content type id}/{resource id}/`
- Has `info.txt`, example below
- Has `icon.png`
- Either has `{resource id}.zip` containing the resource, or
- `versions.json` containing information for multiple versions, and a `{version number}.zip` for each (e.g. `1.2.0.zip`).

info.txt:
```
Name=Data Structures Extension
Description=Create and Manage Data Structures
Author=Justin Espedal
Website=http://www.polydes.com/
```

`info.txt` can also specify optional fields and metadata per content type.

For toolset extensions: `Type=(java_library|game|normal)`

For code:
- `Code Mode=(Design|Code)`
- `Code Type=(Behavior|Arbitrary)`

versions.json
```json
{
  "versions": [
    {
      "date": "10/02/2015",
      "changes": "Initial Repository Version.",
      "version": "0.2.0",
      "dependencies": "toolset-com.polydes.common-1.0.0"
    },
    {
      "date": "05/02/2016",
      "changes": "Compatibility for Stencyl b8816.",
      "version": "0.2.1",
      "dependencies": "toolset-com.polydes.common-1.0.0"
    }
  ]
}
```
