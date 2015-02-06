# API Analytics

API Analytics collects data in a new format called [**ALF** *(API Log Format)*](https://github.com/Mashape/api-log-format). There are three supported [data collection APIs](https://github.com/Mashape/analytics-data-collection-apis) which the official clients are built on top of. 

### API Log Format

- [Specification](https://github.com/Mashape/api-log-format)
- [Example JSON](https://github.com/Mashape/api-log-format#full-example)

### Official Clients

- [Node.js Agent](https://github.com/Mashape/analytics-agent-nodejs)
  - *NodeJS middleware, compatible with HTTP, Express, Restify, etc ...*
- [HARchiver](https://github.com/Mashape/HARchiver)
  - *Universal lightweight proxy*

### Data Collection APIs

- [Socket.io](https://github.com/Mashape/analytics-data-collection-apis#socketio)
  - *Socket.io is the simplest, but isn't available on every platform and language.*
- [ZeroMQ](https://github.com/Mashape/analytics-data-collection-apis#zeromq)
  - *ZMQ is the fastest and is available for virtually every language, but it requires an external library.*
- [HTTP](https://github.com/Mashape/analytics-data-collection-apis#http)
  - *HTTP is the slowest and is only there for compatibility when the other options aren't suitable.*
