# API Analytics

This specification documents the public interface to log data points into [apianalytics.com](http://apianalytics.com)

**This document is authoritative**: other copies of this information must follow the standard to ensure compatibility.

API Analytics uses a custom logging format that incorporates [**HAR**](http://www.softwareishard.com/blog/har-12-spec/) *(HTTP Archive Format)* for HTTP logging.
It supports the Socket.io, ZMQ and HTTP protocols, see [API Log Format](format.md) for more details on the modified standard.

## Official Clients

- [Node.js Agent](https://github.com/APIAnalytics/node-agent)
  - *NodeJS middleware, compatible with HTTP, Express, Restify, etc ...*
- [HARchiver](https://github.com/APIAnalytics/HARchiver)
  - *Universal lightweight proxy*

## Communicating with the server

The ApiAnalytics.com platform supports 3 different protocols: Socket.io, ZMQ and HTTP.

- Socket.io is the simplest, but isn't available on every platform and language.

- ZMQ is the fastest and is available for virtually every language, but it requires an external library.

- HTTP is the slowest and is only there for compatibility when the other options aren't suitable.

### Socket.io

Open a connection to `ws://socket.apianalytics.com`. Emit [API Log Format](format.md) object on the channel `message`.

```js
var io = require('socket.io-client');
var socket = io('ws://socket.apianalytics.com');
socket.send(harObject);
```

### ZMQ

Open a connection to `socket.apianalytics.com`, port `5000`, in `push` mode. Send a string representation of the [API Log Format](format.md) object.

```js
var zmq = require('zmq');
var socket = zmq.socket('push');
socket.connect('tcp://socket.apianalytics.com:5000');
socket.send(JSON.stringify(harObject));
```

### HTTP

Send HTTP `POST` requests to `http://socket.apianalytics.com/`. The body must be a valid [API Log Format](format.md) object.

Alternatively, it's possible to send an array of API Log Format objects.

**Note:** The payload (body) per HTTP request must not exceed 1MB.
