# Resource Timing API

The **`Resource Timing`** interfaces enable retrieving and analyzing detailed network timing data regarding the loading of an application's *resource(s)*. An application can use the timing metrics to determine, for example,  the length of time it takes to load a specific resource, such as an [`XMLHttpRequest`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest), [`SVG`](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/SVG), image, or script.

The interface's properties create a *resource loading timeline* with [high-resolution timestamps](https://developer.mozilla.org/en-US/docs/Web/API/DOMHighResTimeStamp) for network events such as redirect start and end times, DNS lookup  start and end times, request start, response start and end times, etc.  The interface also includes other properties that provide data about the size of the fetched resource as well as the *type* of resource that initiated the fetch.

This document provides an overview of the `Resource Timing` interfaces. For more details about the interfaces including examples see each interface's reference page, [Using the Resource Timing API](https://developer.mozilla.org/en-US/docs/Web/API/Resource_Timing_API/Using_the_Resource_Timing_API), and the references in the [See also](https://developer.mozilla.org/en-US/docs/Web/API/Resource_Timing_API#See_also) section. For a graphical representation of the resource timing processing model see the [resource timing phases](https://w3c.github.io/resource-timing/#process) figure.

> The `PerformanceResourceTiming` interface extends the [`PerformanceEntry`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceEntry) for [performance entries](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceEntry) which have an [`entryType`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceEntry/entryType) of "`resource`".

## High-resolution timestamps

Several of the `Resource Timing` properties return *high-resolution timestamps*. These timestamps have a `DOMHighResTimeStamp` type and as its name implies, they represent a high-resolution point in time. This type is a `double` and its value is a discrete point in time or the difference in time between two discrete points in time.

The unit of `DOMHighResTimeStamp` is milliseconds and  should be accurate to 5 µs (microseconds). However, If the browser is  unable to provide a time value accurate to 5 µs (because, for example,  due to hardware or software constraints), the browser can represent a  the value as a time in milliseconds accurate to a millisecond.

## Resource loading timestamps

An application can get timestamps for the various stages used to load a resource. The first property in the processing model is [`startTime`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceEntry/startTime) which returns the timestamp immediately before the resource loading process begins. The [`fetchStart`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming/fetchStart) timestamps follows and redirect processing (if applicable) and preceeds DNS lookup. The next stages are [`connectStart`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming/connectStart) and [`connectEnd`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming/connectEnd) which are the timestamps immediately before and after connecting to the server, respectively. The last three timestamps are, in order: [`requestStart`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming/requestStart) - the timestamp before the browser starts requesting the resource from the server; [`responseStart`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming/responseStart) - the timestamp after the browser receives the first byte of the response from the server; and [`responseEnd`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming/responseEnd) - the timestamp after the browser receives the last byte of the resource. If the resource is loaded via a secure connection a [`secureConnectionStart`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming/secureConnectionStart) timestamp will be available between the connection start and end events.

> When [CORS](https://developer.mozilla.org/en-US/docs/Glossary/CORS) is in effect, many of these values are returned as zero unless the  server's access policy permits these values to be shared. This requires  the server providing the resource to send the `Timing-Allow-Origin` HTTP response header with a value specifying the origin or origins which are allowed to get the restricted timestamp values.

> The properties which are returned as 0 by default when loading a  resource from a domain other than the one of the web page itself: `redirectStart`, `redirectEnd`, `domainLookupStart`, `domainLookupEnd`, `connectStart`, `connectEnd`, `secureConnectionStart`, `requestStart`, and `responseStart`.

The `PerformanceResourceTiming` interface also includes several network timing properties. The [`redirectStart`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming/redirectStart) and [`redirectEnd`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming/redirectEnd) properties return [`timestamps`](https://developer.mozilla.org/en-US/docs/Web/API/DOMHighResTimeStamp) for redirect start and end times, respectively. Likewise, the The [`domainLookupStart`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming/domainLookupStart) and [`domainLookupEnd`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming/domainLookupEnd) properties return [`timestamps`](https://developer.mozilla.org/en-US/docs/Web/API/DOMHighResTimeStamp) for DNS lookup start and end times, respectively.

*This would be a nice place to have a diagram showing the relationships between these segments of the resource loading time.*

## Resource size

The [`PerformanceResourceTiming`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming) interface has three properties that can be used to obtain size data about a resource. The [`transferSize`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming/transferSize) property returns the size (in octets) of the fetched resource including the response header fields plus the response payload body.

The [`encodedBodySize`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming/encodedBodySize) property returns the size (in octets) received from the fetch (HTTP or cache), of the *payload body*, **before** removing any applied content-codings. [`decodedBodySize`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming/decodedBodySize) returns the size (in octets) received from the fetch (HTTP or cache) of the *message body*, **after** removing any applied content-codings.

## Other properties

The [`nextHopProtocol`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming/nextHopProtocol) property returns the *network protocol* used to fetch the resource.

The [`initiatorType`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming/initiatorType) property returns the *type* of resource that initiated the performance entry such as "`css`" for a CSS resource, "`xmlhttprequest`" for an XMLHttpRequest and "`img`" for an image (such as a JPEG).

If the current context is a [`worker`](https://developer.mozilla.org/en-US/docs/Web/API/Worker), the [`workerStart`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming/workerStart) property can be used to obtain a [`DOMHighResTimeStamp`](https://developer.mozilla.org/en-US/docs/Web/API/DOMHighResTimeStamp) when the worker was started.

## Methods

The Resource Timing API includes two methods that extend the [`Performance`](https://developer.mozilla.org/en-US/docs/Web/API/Performance) interface. The [`clearResourceTimings()`](https://developer.mozilla.org/en-US/docs/Web/API/Performance/clearResourceTimings) method removes all "`resource`" type performance entries from the browser's *resource* performance entry buffer. The [`setResourceTimingBufferSize()`](https://developer.mozilla.org/en-US/docs/Web/API/Performance/setResourceTimingBufferSize) method sets the resource performance entry buffer size to the specified number of resource [`performance entries`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceEntry).

The [`PerformanceResourceTiming`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming) interface's [`toJSON()`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming/toJSON) method returns a JSON serialization of a "`resource`" type [`performance entry`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceEntry).

## Implementation status

As shown in the [`PerformanceResourceTiming`](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming) interface's [Browser Compatibility](https://developer.mozilla.org/Web/API/PerformanceResourceTiming#Browser_compatibility) table, most of these interfaces are broadly implemented by desktop  browsers. However, note that some properties have little to no  implementation so see each property's "Browser compatibility" section  for more specific interoperability data.

To test your browser's support for these interfaces, run the `perf-api-support` application.