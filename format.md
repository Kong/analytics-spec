# HAR+

*HAR+* is a simple JSON-based format based on the **HAR** *(HTTP Archive Format)* [standard](http://www.softwareishard.com/blog/har-12-spec/).

### Encoding

A HAR+ Message is REQUIRED to be saved in `UTF-8` encoding. Other encodings are forbidden.

## List of objects

### message

This object represents the root of the JSON message. The object contains the following name/value pairs:

```js
{
  "serviceToken": "<service token>",
  "version": "1.2",
  "creator": {...},
  "entries": `...`
}
```

| Name                | Type     | Required   | Description                                                                                                   |
| ------------------- | -------- | ---------- | ------------------------------------------------------------------------------------------------------------- |
| **`serviceToken`**  | `String` | `required` | Version number of the format *(currently 1.2)*                                                                |
| **`version`**       | `String` | `required` | obtain yours by registering for a free trial at `APIAnalytics.com`(http://apianalytics.com)                   |
| **`creator`**       | `Object` | `required` | An object of type [`creator`](#creator) that contains the name and version information of the log creator agent |
| **`entries`**       | `Array`  | `required` | An array of objects of type `entry`(#entry), each representing one exported (tracked) HTTP request.           |

### creator

This object contains information about the log creator agent and contains the following name/value pairs:

```js
"creator": {
  "name": "My HAR client",
  "version": "1.0"
}
```

| Name          | Type     | Required   | Description                                           |
| ------------- | -------- | ---------- | ----------------------------------------------------- |
| **`name`**    | `String` | `required` | The name of the agent that created the log.           |
| **`version`** | `String` | `required` | The version number of the agent that created the log. |

### entries

This object represents an array with all exported HTTP requests.

```js
"entries": [
  {
    "serverIPAddress": "10.10.10.10",
    "clientIPAddress": "10.10.10.20",
    "startedDateTime": "2015-01-20T18:22:09.052",
    "time": 50,
    "request": {...},
    "response": {...},
    "timings": {...}
  }
]
```

| Name                  | Type      | Required   | Description                                                                                                                                                    |
| --------------------- | --------- | ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`serverIPAddress`** | `String`  | `optional` | IP address of the server                                                                                                                                       |
| **`clientIPAddress`** | `String`  | `optional` | IP address of the client                                                                                                                                       |
| **`startedDateTime`** | `String`  | `required` | Date and time stamp for the beginning of the request (ISO 8601 - YYYY-MM-DDThh:mm:ss.sTZD)                                                                     |
| **`time`**            | `Nnumber` | `required` | Total elapsed time of the request in milliseconds. This is the sum of all timings available in the `timings`(#timings) object (i.e. not including `-1` values) |
| **`request`**         | `Object`  | `required` | An object of type [`request`](#request) that contains info about the request                                                                                   |
| **`response`**        | `Object`  | `required` | An object of type [`response`](#response) that contains info about the response                                                                                |
| **`timings`**         | `Object`  | `required` | An object of type [`timings`](#timings) that contains timing info about request/response round trip                                                            |

### request

This object contains detailed info about performed request.

```js
"request": {
  "method": "GET",
  "url": "http://api.domain.com/path/",
  "httpVersion": "HTTP/1.1",
  "queryString" : `...`,
  "headers": `...`,
  "headersSize" : 50,
  "bodySize" : 20,
  "content": {...}
}
```

| Name              | Type      | Required   | Description                                                                                                                                                      |
| ----------------- | --------- | ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`method`**      | `String`  | `required` | Request method                                                                                                                                                   |
| **`url`**         | `String`  | `required` | Absolute URL of the request                                                                                                                                      |
| **`httpVersion`** | `String`  | `required` | Request HTTP Version                                                                                                                                             |
| **`queryString`** | `Array`   | `required` | List of query parameter objects                                                                                                                                  |
| **`headers`**     | `Array`   | `required` | List of header objects                                                                                                                                           |
| **`headersSize`** | `Number`  | `required` | Total number of bytes from the start of the HTTP request message until (and including) the double CRLF before the body. Set to `-1` if the info is not available |
| **`content`**     | `Object`  | `optional` | An object of type [`content`](#content) that contain info about the request body                                                                                   |
| **`bodySize`**    | `Number`  | `required` | Size of the request body (POST data payload) in bytes. Set to `-1` if the info is not available                                                                  |

### response

This object contains detailed info about the response.

```js
"response": {
    "status": 200,
    "statusText": "OK",
    "httpVersion": "HTTP/1.1",
    "headers": `...`,
    "headersSize" : 160,
    "content": {...},
    "bodySize" : 850,
 }
```

| Name              | Type      | Required   | Description                                                                                                                                                        |
| ----------------- | --------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **`status`**      | `Number`  | `required` | Response status                                                                                                                                                    |
| **`statusText`**  | `String`  | `required` | Response status description                                                                                                                                        |
| **`httpVersion`** | `String`  | `required` | Response HTTP Version                                                                                                                                              |
| **`headers`**     | `Array`   | `required` | List of header objects                                                                                                                                             |
| **`headersSize`** | `Number`  | `required` | Total number of bytes from the start of the HTTP response message until (and including) the double CRLF before the body. Set to `-1` if the info is not available  |
| **`content`**     | `Object`  | `optional` | An object of type [`content`](#content) that contain info about the response body                                                                                    |
| **`bodySize`**    | `Number`  | `required` | Size of the received response body in bytes. Set to zero in case of responses coming from the cache (304). Set to `-1` if the info is not available                |


### headers

This object contains list of all headers *(used in `request](#request) and [response`(#response) objects)*.

```js
"headers": [
  {
    "name": "Accept-Encoding",
    "value": "gzip,deflate",
  },
  {
    "name": "Accept-Language",
    "value": "en-us,en;q=0.5",
  }
]
```

### queryString

This object contains list of all parameters & values parsed from a query string, if any *(embedded in `request`(#request) object)*.

```js
"queryString": [
  {
    "name": "param1",
    "value": "value1",
  },
  {
    "name": "param1",
    "value": "value1",
  }
]
```

### content

This object describes details about response content *(used in `request](#request) and [response`(#response) objects)*.

```js
"content": {
  "size": 33,
  "compression": 0,
  "mimeType": "text/html; charset=utf-8",
  "encoding": "base64",
  "text": "",
}
```

| Name              | Type      | Required   | Description                                                                                                                                                                       |
| ----------------- | --------- | ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`size`**        | `Number`  | `required` | Length of the returned content in bytes. *Should be equal to `response.bodySize` / `request.bodySize` if there is no compression and bigger when the content has been compressed* |
| **`compression`** | `Number`  | `optional` | Number of bytes saved. Leave out if info is not available                                                                                                                         |
| **`mimeType`**    | `String`  | `required` | MIME type of the text field. The charset attribute of the MIME type is included (if available)                                                                                    |
| **`encoding`**    | `String`  | `optional` | Encoding used for the text field e.g `base64`. Leave out this field if the text field is HTTP decoded (decompressed & unchunked)                                                  |
| **`text`**        | `String`  | `optional` | Response body sent. populated with textual content only. Leave out if info is not available                                                                                       |

### timings

This object describes various phases within request-response round trip. All times are specified in milliseconds.

```js
"timings": {
  "blocked": 0,
  "dns": -1,
  "connect": 15,
  "send": 20,
  "wait": 38,
  "receive": 12,
  "ssl": -1,
  "comment": ""
}
```

| Name          | Type     | Required   | Description                                                                                                                     |
| ------------- | -------- | ---------- | ------------------------------------------------------------------------------------------------------------------------------- |
| **`blocked`** | `Number` | `optional` | Time spent in a queue waiting for a network connection. Use `-1` if the timing does not apply to the current request            |
| **`dns`**     | `Number` | `optional` | DNS resolution time. The time required to resolve a host name. Use `-1` if the timing does not apply to the current request     |
| **`connect`** | `Number` | `optional` | Time required to create TCP connection. Use `-1` if the timing does not apply to the current request                            |
| **`send`**    | `Number` | `required` | Time required to send HTTP request to the server                                                                                |
| **`wait`**    | `Number` | `required` | Waiting for a response from the server                                                                                          |
| **`receive`** | `Number` | `required` | Time required to read entire response from the server (or cache)                                                                |
| **`ssl`**     | `Number` | `optional` | Time required for SSL/TLS negotiation. Use `-1` if the timing does not apply to the current request                             |

*The `time` value for the [request object](#request) must be equal to the sum of the timings supplied in this section (excluding any -1 values).*

Following must be true in case there are no `-1` values:

```js
entry.time == entry.timings.blocked + entry.timings.dns +
  entry.timings.connect + entry.timings.send + entry.timings.wait +
  entry.timings.receive + entry.timings.ssl;
```

###### Full Example

```js
{
  "serviceToken": "<my service token>",
  "version": "1.2",
  "creator": {
    "name": "My HAR client",
    "version": "1.0"
  },
  "entries": [{
    "serverIPAddress": "10.10.10.10",
    "startedDateTime": "2015-01-20T18:22:09.052",
    "request": {
      "method": "POST",
      "url": "http://api.domain.com/path/",
      "httpVersion": "HTTP/1.1",
      "queryString": [
        {"name": "foo", "value": "bar"},
        {"name": "baz", "value": "abc"}
      ],
      "headers": [
        {"name":"Accept", "value":"text/plain"},
        {"name":"Cookie", "value":"ijafhIAGWF3Awf93f"}
      ],
      "headersSize": 44,
      "bodySize": 14,
      "content": {
        "size": 14,
        "mimeType": "application/json",
        "text": "{\"foo\": \"bar\"}"
      }
    },
    "response": {
      "status": 200,
      "statusText": "OK",
      "httpVersion": "HTTP/1.1",
      "headers": [
        {"name": "Content-Length", "value": 11},
        {"name": "Mime-Type", "value": "text/plain"}
      ],
      "content": {
        "size": 11,
        "mimeType": "text/plain",
        "text": "hello world"
      },
      "bodySize": 11,
      "headersSize": 41,
      "redirectUrl": ""
    },
    "timings": {
      "blocked": 0,
      "dns": -1,
      "connect": 15,
      "send": 20,
      "wait": 38,
      "receive": 12,
      "ssl": -1,
    }
  }]
}
```
