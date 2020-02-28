# Streams API

> **This is an [experimental technology](https://developer.mozilla.org/en-US/docs/MDN/Contribute/Guidelines/Conventions_definitions#Experimental)**
> Check the [Browser compatibility table](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API#Browser_compatibility) carefully before using this in production.

The Streams API allows JavaScript to programmatically access streams  of data received over the network and process them as desired by the  developer.

## Concepts and usage

Streaming involves breaking a resource that you want to receive over a network down into small chunks, then processing it bit by bit. This is  something browsers do anyway when receiving assets to be shown on  webpages — videos buffer and more is gradually available to play, and  sometimes you'll see images display gradually as more is loaded.

But this has never been available to JavaScript before. Previously,  if we wanted to process a resource of some kind (be it a video, or a  text file, etc.), we'd have to download the entire file, wait for it to  be deserialized into a suitable format, then process the whole lot after it is fully received.

With Streams being available to JavaScript, this all changes — you  can now start processing raw data with JavaScript bit by bit as soon as  it is available on the client-side, without needing to generate a  buffer, string, or blob.

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article7-folder/Concept.png)

There are more advantages too — you can detect when streams start or  end, chain streams together, handle errors and cancel streams as  required, and react to the speed of the stream is being read at.

The basic usage of Streams hinges around making responses available as streams. For example, the response [`Body`](https://developer.mozilla.org/en-US/docs/Web/API/Body) returned by a successful [fetch request](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch) can be exposed as a [`ReadableStream`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream), and you can then read it using a reader created with [`ReadableStream.getReader()`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream/getReader), cancel it with [`ReadableStream.cancel()`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream/cancel), etc.

More complicated uses involve creating your own stream using the [`ReadableStream()`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream/ReadableStream) constructor, for example to process data inside a [service worker](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API).

You can also write data to streams using [`WritableStream`](https://developer.mozilla.org/en-US/docs/Web/API/WritableStream).

> **Note**: You can find a lot more details about the theory and practice of streams in our articles — [Streams API concepts](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API/Concepts), [Using readable streams](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API/Using_readable_streams), and [Using writable streams](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API/Using_writable_streams).

## Stream interfaces

### Readable streams

- [`ReadableStream`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream)

  Represents a readable stream of data. It can be used to handle response streams of the [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API), or developer-defined streams (e.g. a custom [`ReadableStream()`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream/ReadableStream) constructor).

- [`ReadableStreamDefaultReader`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStreamDefaultReader)

  Represents a default reader that can be used to read stream data supplied from a network (e.g. a fetch request).

- [`ReadableStreamDefaultController`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStreamDefaultController)

  Represents a controller allowing control of a [`ReadableStream`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream)'s state and internal queue. Default controllers are for streams that are not byte streams.

### Writable streams

- [`WritableStream`](https://developer.mozilla.org/en-US/docs/Web/API/WritableStream)

  Provides a standard abstraction for writing streaming data to a  destination, known as a sink. This object comes with built-in  backpressure and queuing.

- [`WritableStreamDefaultWriter`](https://developer.mozilla.org/en-US/docs/Web/API/WritableStreamDefaultWriter)

  Represents a default writable stream writer that can be used to write chunks of data to a writable stream.

- [`WritableStreamDefaultController`](https://developer.mozilla.org/en-US/docs/Web/API/WritableStreamDefaultController)

  Represents a controller allowing control of a [`WritableStream`](https://developer.mozilla.org/en-US/docs/Web/API/WritableStream)'s state. When constructing a `WritableStream`, the underlying sink is given a corresponding `WritableStreamDefaultController` instance to manipulate.

### Related stream APIs and operations

- [`ByteLengthQueuingStrategy`](https://developer.mozilla.org/en-US/docs/Web/API/ByteLengthQueuingStrategy)

  Provides a built-in byte length queuing strategy that can be used when constructing streams.

- [`CountQueuingStrategy`](https://developer.mozilla.org/en-US/docs/Web/API/CountQueuingStrategy)

  Provides a built-in chunk counting queuing strategy that can be used when constructing streams.

### Extensions to other APIs

- [`Request`](https://developer.mozilla.org/en-US/docs/Web/API/Request)

  When a new `Request` object is constructed, you can pass it a [`ReadableStream`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream) in the `body` property of its `RequestInit` dictionary. This `Request` could then be passed to a [`WindowOrWorkerGlobalScope.fetch()`](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch) to commence fetching the stream.

- [`Body`](https://developer.mozilla.org/en-US/docs/Web/API/Body)

  The response [`Body`](https://developer.mozilla.org/en-US/docs/Web/API/Body) returned by a successful [fetch request](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch) is exposed by default as a [`ReadableStream`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream), and can have a reader attached to it, etc.

### ByteStream-related interfaces

> **Important**: these are not implemented anywhere as  yet, and questions have been raised as to whether the spec details are  in a finished enough state for them to be implemented. This may change  over time.

- [`ReadableStreamBYOBReader`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStreamBYOBReader)

  Represents a BYOB ("bring your own buffer") reader that can be used to read stream data supplied by the developer (e.g. a custom [`ReadableStream()`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream/ReadableStream) constructor).

- [`ReadableByteStreamController`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableByteStreamController)

  Represents a controller allowing control of a [`ReadableStream`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream)'s state and internal queue. Byte stream controllers are for byte streams.

- [`ReadableStreamBYOBRequest`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStreamBYOBRequest)

  Represents a pull into request in a [`ReadableByteStreamController`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableByteStreamController).

## Examples

We have created a directory of examples to go along with the Streams API documentation — see [mdn/dom-examples/streams](https://github.com/mdn/dom-examples/tree/master/streams). The examples are as follows:

- [Simple stream pump](http://mdn.github.io/dom-examples/streams/simple-pump/): This example shows how to consume a ReadableStream and pass its data to another.
- [Grayscale a PNG](http://mdn.github.io/dom-examples/streams/grayscale-png/): This example shows how a ReadableStream of a PNG can be turned into grayscale.
- [Simple random stream](http://mdn.github.io/dom-examples/streams/simple-random-stream/): This example shows how to use a custom stream to generate random  strings, enqueue them as chunks, and then read them back out again.
- [Simple tee example](http://mdn.github.io/dom-examples/streams/simple-tee-example/): This example extends the Simple random stream example, showing how a  stream can be teed and both resulting streams can be read independently.
- [Simple writer](http://mdn.github.io/dom-examples/streams/simple-writer/): This example shows how to to write to a writable stream, then decode the stream and write the contents to the UI.
- [Unpack chunks of a PNG](http://mdn.github.io/dom-examples/streams/png-transform-stream/): This example shows how [`pipeThrough()`](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream/pipeThrough) can be used to transform a ReadableStream into a stream of other data  types by transforming a data of a PNG file into a stream of PNG chunks.

Examples from other developers:

- [Progress Indicators with Streams, Service Workers, & Fetch](https://fetch-progress.anthum.com/).

## Specifications

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article7-folder/t1.jpg)



## Browser compatibility

### ReadableStream

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article7-folder/t2.jpg)

### WritableStream

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article7-folder/t3.jpg)

