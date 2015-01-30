# Collection APIs

We support three different protocols for sending data into API analytics.

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
