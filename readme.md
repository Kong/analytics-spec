# API Analytics

API Analytics collects data in a new format called [**ALF** *(API Log Format)*](https://github.com/APIAnalytics/spec/blob/master/format.md). We support multiple [data collection APIs](https://github.com/APIAnalytics/spec/blob/master/api.md) which our official clients are built on top of. No matter what stack you're running, as an API creator or consumer, it's possible to intregrate with API analytics to gain a deeper understanding of your API layer.

### API Log Format

- [Specification](https://github.com/APIAnalytics/spec/blob/master/format.md)
- [Example JSON](https://github.com/APIAnalytics/spec/blob/master/format.md#full-example)

### Official Clients

- [Node.js Agent](https://github.com/APIAnalytics/node-agent)
  - *NodeJS middleware, compatible with HTTP, Express, Restify, etc ...*
- [HARchiver](https://github.com/APIAnalytics/HARchiver)
  - *Universal lightweight proxy*

### Collection APIs

- [Socket.io](https://github.com/APIAnalytics/spec/blob/master/api.md#socketio)
  - *Socket.io is the simplest, but isn't available on every platform and language.*
- [ZeroMQ](https://github.com/APIAnalytics/spec/blob/master/api.md#zmq)
  - *ZMQ is the fastest and is available for virtually every language, but it requires an external library.*
- [HTTP](https://github.com/APIAnalytics/spec/blob/master/api.md#http)
  - *HTTP is the slowest and is only there for compatibility when the other options aren't suitable.*
