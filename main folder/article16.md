# Web Workers API

**Web Workers** makes it possible to  run a script operation in a background thread separate from the main  execution thread of a web application. The advantage of this is that  laborious processing can be performed in a separate thread, allowing the main (usually the UI) thread to run without being blocked/slowed down.

## Web Workers concepts and usage

A worker is an object created using a constructor (e.g. [`Worker()`](https://developer.mozilla.org/en-US/docs/Web/API/Worker/Worker)) that runs a named JavaScript file — this file contains the code that  will run in the worker thread; workers run in another global context  that is different from the current [`window`](https://developer.mozilla.org/en-US/docs/Web/API/Window). This context is represented by either a [`DedicatedWorkerGlobalScope`](https://developer.mozilla.org/en-US/docs/Web/API/DedicatedWorkerGlobalScope) object (in the case of dedicated workers - workers that are utilized by a single script), or a [`SharedWorkerGlobalScope`](https://developer.mozilla.org/en-US/docs/Web/API/SharedWorkerGlobalScope) (in the case of shared workers - workers that are shared between multiple scripts).

You can run whatever code you like inside the worker thread, with  some exceptions. For example, you can't directly manipulate the DOM from inside a worker, or use some default methods and properties of the [`window`](https://developer.mozilla.org/en-US/docs/Web/API/Window) object. But you can use a large number of items available under `window`, including [WebSockets](https://developer.mozilla.org/en-US/docs/WebSockets), and data storage mechanisms like [IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API). See [Functions and classes available to workers](https://developer.mozilla.org/en-US/docs/Web/API/Worker/Functions_and_classes_available_to_workers) for more details.

Data is sent between workers and the main thread via a system of messages — both sides send their messages using the `postMessage()` method, and respond to messages via the `onmessage` event handler (the message is contained within the `Message` event's `data` property). The data is copied rather than shared.

Workers may in turn spawn new workers, as long as those workers are  hosted within the same origin as the parent page. In addition, workers  may use [`XMLHttpRequest`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) for network I/O, with the exception that the `responseXML` and `channel` attributes on `XMLHttpRequest` always return `null`.

In addition to dedicated workers, there are other types of worker:

- Shared workers are workers that can be utilized by multiple scripts running in different windows, IFrames, etc., as long as they are in the same domain as the worker. They are a little more complex than  dedicated workers — scripts must communicate via an active port. See [`SharedWorker`](https://developer.mozilla.org/en-US/docs/Web/API/SharedWorker) for more details.
- [ServiceWorkers](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorker_API) essentially act as proxy servers that sit between web applications, the browser, and the network (when available). They are intended, among  other things, to enable the creation of effective offline experiences,  intercept network requests and take appropriate action based on whether  the network is available, and update assets residing on the server. They will also allow access to push notifications and background sync APIs.
- Chrome Workers are a Firefox-only type of worker that you can use  if you are developing add-ons and want to use workers in extensions and  have access to [js-ctypes](https://developer.mozilla.org/en/js-ctypes) in your worker. See [`ChromeWorker`](https://developer.mozilla.org/en-US/docs/Web/API/ChromeWorker) for more details. 
- [Audio Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Audio_API#Audio_Workers) provide the ability for direct scripted audio processing to be done inside a web worker context.

> **Note**: As per the [Web workers Spec](https://html.spec.whatwg.org/multipage/workers.html#runtime-script-errors-2), worker error events should not bubble (see [bug 1188141](https://bugzilla.mozilla.org/show_bug.cgi?id=1188141). This has been implemented in Firefox 42.

## Web Worker interfaces

- [`AbstractWorker`](https://developer.mozilla.org/en-US/docs/Web/API/AbstractWorker)

  Abstracts properties and methods common to all kind of workers (i.e. [`Worker`](https://developer.mozilla.org/en-US/docs/Web/API/Worker) or [`SharedWorker`](https://developer.mozilla.org/en-US/docs/Web/API/SharedWorker)).

- [`Worker`](https://developer.mozilla.org/en-US/docs/Web/API/Worker)

  Represents a running worker thread, allowing you to pass messages to the running worker code.

- [`WorkerLocation`](https://developer.mozilla.org/en-US/docs/Web/API/WorkerLocation)

  Defines the absolute location of the script executed by the [`Worker`](https://developer.mozilla.org/en-US/docs/Web/API/Worker).

- [`SharedWorker`](https://developer.mozilla.org/en-US/docs/Web/API/SharedWorker)

  Represents a specific kind of worker that can be *accessed* from several [browsing contexts](https://developer.mozilla.org/en-US/docs/Glossary/browsing_context), being several windows, iframes or even workers.

- [`WorkerGlobalScope`](https://developer.mozilla.org/en-US/docs/Web/API/WorkerGlobalScope)

  Represents the generic scope of any worker (doing the same job as [`Window`](https://developer.mozilla.org/en-US/docs/Web/API/Window) does for normal web content). Different types of worker have scope  objects that inherit from this interface and add more specific features.

- [`DedicatedWorkerGlobalScope`](https://developer.mozilla.org/en-US/docs/Web/API/DedicatedWorkerGlobalScope)

  Represents the scope of a dedicated worker, inheriting from [`WorkerGlobalScope`](https://developer.mozilla.org/en-US/docs/Web/API/WorkerGlobalScope) and adding some dedicated features.

- [`SharedWorkerGlobalScope`](https://developer.mozilla.org/en-US/docs/Web/API/SharedWorkerGlobalScope)

  Represents the scope of a shared worker, inheriting from [`WorkerGlobalScope`](https://developer.mozilla.org/en-US/docs/Web/API/WorkerGlobalScope) and adding some dedicated features.

- [`WorkerNavigator`](https://developer.mozilla.org/en-US/docs/Web/API/WorkerNavigator)

  Represents the identity and state of the user agent (the client):

## Examples

We have created a couple of simple demos to show basic usage:

- [Basic dedicated worker example](https://github.com/mdn/simple-web-worker) ([run dedicated worker](http://mdn.github.io/simple-web-worker/)).
- [Basic shared worker example](https://github.com/mdn/simple-shared-worker) ([run shared worker](http://mdn.github.io/simple-shared-worker/)).

You can find out more information on how these demos work in [Using web workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Using_web_workers).

## Specifications

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article16-folder/t1.jpg)