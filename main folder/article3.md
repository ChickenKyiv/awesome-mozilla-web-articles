# Server-sent events

Traditionally, a web page has to send a request to the server to  receive new data; that is, the page requests data from the server. With  server-sent events, it's possible for a server to send new data to a web page at any time, by pushing messages to the web page. These incoming  messages can be treated as *[Events](https://developer.mozilla.org/en-US/docs/DOM/event) + data* inside the web page.

## Concepts and usage

To learn how to use server-sent events, see our article [Using server-sent events](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events/Using_server-sent_events).

## Interfaces

- [`EventSource`](https://developer.mozilla.org/en-US/docs/Web/API/EventSource)

  Defines all the features that handle connecting to a server, receiving events/data, errors, closing a connection, etc.

## Examples

- [Simple SSE demo using PHP](https://github.com/mdn/dom-examples/tree/master/server-sent-events)

## Specification

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article3-folder/t2.jpg)