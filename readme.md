# API Analytics

API Analytics collects data in a custom format called [**ALF (API Log Format)**](https://github.com/APIAnalytics/spec/blob/master/format.md). We support multiple input protocols for collecting ALF data which we used to build the official clients so no matter what tech stack you're running it is possible to intregrate API analytics and gain a deeper understanding of your API layer. 

## API Log Format

- [Specification](https://github.com/APIAnalytics/spec/blob/master/format.md)
- [Example JSON](https://github.com/APIAnalytics/spec/blob/master/format.md#full-example)

## Official Clients

- [Node.js Agent](https://github.com/APIAnalytics/node-agent)
  - *NodeJS middleware, compatible with HTTP, Express, Restify, etc ...*
- [HARchiver](https://github.com/APIAnalytics/HARchiver)
  - *Universal lightweight proxy*

## Collection APIs

- [Socket.io](https://github.com/APIAnalytics/spec/blob/master/api.md#socketio)
  - *Socket.io is the simplest, but isn't available on every platform and language.*
- [ZeroMQ](https://github.com/APIAnalytics/spec/blob/master/api.md#zmq)
  - *ZMQ is the fastest and is available for virtually every language, but it requires an external library.*
- [HTTP](https://github.com/APIAnalytics/spec/blob/master/api.md#http)
  - *HTTP is the slowest and is only there for compatibility when the other options aren't suitable.*
