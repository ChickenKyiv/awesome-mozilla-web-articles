# The WebSocket API (WebSockets)

The **WebSocket API** is an advanced technology that  makes it possible to open a two-way interactive communication session  between the user's browser and a server. With this API, you can send  messages to a server and receive event-driven responses without having  to poll the server for a reply.

> **Note:** While a WebSocket connection is functionally somewhat similar to standard Unix-style sockets, they are not related.

## Interfaces

- [`WebSocket`](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket)

  The primary interface for connecting to a WebSocket server and then sending and receiving data on the connection.

- `CloseEvent`

  The event sent by the WebSocket object when the connection closes.

- [`MessageEvent`](https://developer.mozilla.org/en-US/docs/Web/API/MessageEvent)

  The event sent by the WebSocket object when a message is received from the server.

## Guides

- [Writing WebSocket client applications](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API/Writing_WebSocket_client_applications)
- [Writing WebSocket servers](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API/Writing_WebSocket_servers)
- [Writing a WebSocket server in C#](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API/Writing_WebSocket_server)
- [Writing a WebSocket server in Java](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API/Writing_a_WebSocket_server_in_Java)

## Tools

- [HumbleNet](https://hacks.mozilla.org/2017/06/introducing-humblenet-a-cross-platform-networking-library-that-works-in-the-browser/): A cross-platform networking library that works in the browser. It  consists of a C wrapper around WebSockets and WebRTC that abstracts away cross-browser differences, facilitating the creation of multi-user  networking functionality for games and other apps.
- [µWebSockets](https://github.com/uWebSockets/uWebSockets): Highly scalable WebSocket server and client implementation for [C++11](https://isocpp.org/) and [Node.js](https://nodejs.org).
- [ClusterWS](https://github.com/ClusterWS/ClusterWS): Lightweight, fast and powerful framework for building scalable WebSocket applications in [Node.js](https://nodejs.org).
- [CWS](https://github.com/ClusterWS/cWS): Fast C++ WebSocket implementation for Node.js (uWebSockets v0.14 fork)
- [Socket.IO](https://socket.io): A long polling/WebSocket based third party transfer protocol for [Node.js](https://nodejs.org).
- [SocketCluster](http://socketcluster.io/): A pub/sub WebSocket framework for [Node.js](https://nodejs.org) with a focus on scalability.
- [WebSocket-Node](https://github.com/Worlize/WebSocket-Node): A WebSocket server API implementation for [Node.js](https://nodejs.org).
- [Total.js](http://www.totaljs.com): Web application framework for [Node.js](https://www.nodejs.org) (Example: [WebSocket chat](https://github.com/totaljs/examples/tree/master/websocket))
- [Faye](https://www.npmjs.com/package/faye-websocket): A [WebSocket](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) (two-ways connections) and [EventSource](https://developer.mozilla.org/en-US/docs/Web/API/EventSource/) (one-way connections) for [Node.js](https://nodejs.org) Server and Client.
- [SignalR](http://signalr.net/): SignalR will use WebSockets under the covers when it's available, and  gracefully fallback to other techniques and technologies when it isn't,  while your application code stays the same.
- [Caddy](https://caddyserver.com/docs/websocket): A web server capable of proxying arbitrary commands (stdin/stdout) as a websocket.
- [ws](https://github.com/websockets/ws): a popular WebSocket client & server library for [Node.js](https://nodejs.org/).
- [jsonrpc-bidirectional](https://github.com/bigstepinc/jsonrpc-bidirectional): Asynchronous RPC which, on a single connection, may have functions  exported on the server and, and the same time, on the client (client may call server, server may also call client).
- [cowboy](https://github.com/ninenines/cowboy): Cowboy is a small, fast and modern HTTP server for Erlang/OTP with WebSocket support.

## Related Topics

- [AJAX](https://developer.mozilla.org/en-US/docs/Web/Guide/AJAX)
- [JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

## Specifications

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article22-folder/t1.jpg)

## Browser compatibility

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article22-folder/t2.jpg)