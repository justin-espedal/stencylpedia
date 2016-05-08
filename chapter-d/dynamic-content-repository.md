# Dynamic Content Repository

Similar to a Static Content Repository, but the implementation is meant to be handled by a server with
url dispatching and potentially user authentication, to allow for extended functionality, including:

- Content that is locked until paid for.
- Unique content per user.
- Server-side sorting and filtering of results, so that less information is downloaded by Stencyl.

`{base url}`: the url provided to others to access the repository

### Dynamic Repository Access
- Found at `{base url}/` index page
- `url` key defines `{api url}`.

Example:
```json
{
  "access": [
    {
      "version": "v1",
      "url": "v1"
    }
  ]
}
```

### Server Configuration
- A file that expresses how this content server interacts with Stencyl.
- Found at `{base url}/{api url}/config.json`
- One way of authorizing: send HTTP/POST request to `url` with credentials and start a session
- Another way of authorizing: send the saved access token in a query string with every request.
- Can also send other data over query string with each request.

Example:
```json
{
  "start_session": {
    "url": "login.php",
    "post": [
      {
        "key": "username",
        "remember": true,
        "encrypt": true
      },
      {
        "key": "password",
        "remember": true,
        "encrypt": true,
        "hide": true
      }
    ],
    "query": []
  },
  "query": [
    {
      "key": "account_token",
      "remember": false,
      "encrypt": true,
      "hide": false
    },
    {
      "key": "format",
      "value": "json",
      "verb": "get"
    }
  ],
  "content_types": [
    "stencyl.ext.engine",
    "stencyl.ext.toolset",
    "stencyl.lib.actortype"
  ]
}
```

Content types can specify that their resources require a cuid (content-type unique id)

Perhaps the cuid will be queried, or a (cuid => oid) map will be cached by the client.

Example additions to query string for pagination, sorting, and filtering.
- (&offset=10&limit=5)
- (&sort=+field1,-field2)
- (&author=Justin)
- (&cuid=com.polydes.dialog)

`{base url}/{api url}/resources?type={content.type.id}`

- List the resources of a given type

`{base url}/{api url}/resources/{content id}`

`{base url}/{api url}/resources/{content.type.id}/{cuid}`

- For content types that require a unique content id, these should be equivalent.

`{base url}/{api url}/resources/{content id}/versions`

- List versions for a resource

(POST {base url}/{api url}/resources/{content id}/versions/search to do an advanced search of some sort, maybe)

`{base url}/{api url}/resources/{content id}/info.txt`

`{base url}/{api url}/resources/{content id}/icon.png`

`{base url}/{api url}/resources/{content id}/versions/{version}.zip`

- Retrieve the given resources.
