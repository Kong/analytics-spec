# Node Agent

The node agent is compatible with standard HTTP servers and Express, Restify, etc...

## Installation

``` shell
npm install apianalytics --save
```

## Example Usage

``` js
var http = require('http');

var analytics = require('apianalytics');
var agent = analytics('SERVICE_TOKEN', {
  reqByteLimit: 1e10,
  entriesPerHar: 1
});

var server = http.createServer(function (req, res) {
  agent(req, res);
  res.writeHead(200, {"Content-Type": "text/plain"});
  res.end('Hello World!');
});

server.listen(3000);
console.log("Server running at http://127.0.0.1:3000/");
```

### Options

| Name            | Description                               | Default                                                   |
| --------------- | ----------------------------------------- | --------------------------------------------------------- |
| `logger`        | Customize the logging `function(message)` | Default uses [debug](https://www.npmjs.org/package/debug) |
| `reqByteLimit`  | limit the request body capture size       | `1e10`                                                    |
| `entriesPerHar` | num of entries per HAR object sent        | `1`                                                       |


#### Express Example

``` js
var express = require('express');
var analytics = require('apianalytics');
 
var app = express();
 
app.use(analytics('SERVICE_TOKEN'));
 
app.get('/api', function (req, res) {
  res.send('Hello World!');
});
 
var server = app.listen(3000, function () {
  var host = server.address().address
  var port = server.address().port
  console.log('Listening at http://%s:%s', host, port);
});
```

#### Restify Example

``` js
var restify = require('restify');
var analytics = require('apianalytics')

var server = restify.createServer();

server.use(analytics('SERVICE_TOKEN'));

server.get('/api', function (req, res, next) {
  res.send('Hello World!')
  next();
});

server.listen(3000, function() {
  console.log('%s listening at %s', server.name, server.url);
});
```
