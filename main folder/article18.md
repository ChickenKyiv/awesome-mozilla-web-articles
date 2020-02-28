# WebRTC API

**WebRTC** (Web Real-Time  Communication) is a technology which enables Web applications and sites  to capture and optionally stream audio and/or video media, as well as to exchange arbitrary data between browsers without requiring an  intermediary. The set of standards that comprise WebRTC makes it  possible to share data and perform teleconferencing peer-to-peer,  without requiring that the user installs plug-ins or any other  third-party software.

WebRTC consists of several interrelated APIs and protocols which work together to achieve this. The documentation you'll find here will help  you understand the fundamentals of WebRTC, how to set up and use both  data and media connections, and more.

## Interoperability

Because implementations of WebRTC are still evolving, and because each browser has [different levels of support for codecs](https://developer.mozilla.org/en-US/docs/Web/Media/Formats/WebRTC_codecs) and WebRTC features, you should *strongly* consider making use of [the Adapter.js library](https://github.com/webrtcHacks/adapter) provided by Google before you begin to write your code.

Adapter.js uses shims and polyfills to smooth over the differences  among the WebRTC implementations across the environments supporting it.  Adapter.js also handles prefixes and other naming differences to make  the entire WebRTC development process easier, with more broadly  compatible results. The library is also [available as an NPM package](https://www.npmjs.com/package/webrtc-adapter).

To learn more about Adapter.js, see [Improving compatibility using WebRTC adapter.js](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API/adapter.js).

## WebRTC concepts and usage

WebRTC serves multiple purposes; together with the [Media Capture and Streams API](https://developer.mozilla.org/en-US/docs/Web/API/Media_Streams_API), they provide powerful multimedia capabilities to the Web, including  support for audio and video conferencing, file exchange, screen sharing, identity management, and interfacing with legacy telephone systems  including support for sending [DTMF](https://developer.mozilla.org/en-US/docs/Glossary/DTMF) (touch-tone dialing) signals. Connections between peers can be made  without requiring any special drivers or plug-ins, and can often be made without any intermediary servers.

Connections between two peers are represented by the [`RTCPeerConnection`](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection) interface. Once a connection has been established and opened using `RTCPeerConnection`, media streams ([`MediaStream`](https://developer.mozilla.org/en-US/docs/Web/API/MediaStream)s) and/or data channels ([`RTCDataChannel`](https://developer.mozilla.org/en-US/docs/Web/API/RTCDataChannel)s) can be added to the connection.

Media streams can consist of any number of tracks of media information; tracks, which are represented by objects based on the [`MediaStreamTrack`](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack) interface, may contain one of a number of types of media data,  including audio, video, and text (such as subtitles or even chapter  names). Most streams consist of at least one audio track and likely also a video track, and can be used to send and receive both live media or  stored media information (such as a streamed movie).

You can also use the connection between two peers to exchange arbitrary binary data using the [`RTCDataChannel`](https://developer.mozilla.org/en-US/docs/Web/API/RTCDataChannel) interface. This can be used for back-channel information, metadata  exchange, game status packets, file transfers, or even as a primary  channel for data transfer.

***more details and links to relevant guides and tutorials needed***

## WebRTC interfaces

Because WebRTC provides interfaces that work together to accomplish a variety of tasks, we have divided up the interfaces in the list below  by category. Please see the sidebar for an alphabetical list.

### Connection setup and management

These interfaces are used to set up, open, and manage WebRTC  connections. Included are interfaces representing peer media  connections, data channels, and interfaces used when exchanging  information on the capabilities of each peer in order to select the best possible configuration for a two-way media connection..

- [`RTCPeerConnection`](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection)

  Represents a WebRTC connection between the local computer and a  remote peer. It is used to handle efficient streaming of data between  the two peers.

- [`RTCDataChannel`](https://developer.mozilla.org/en-US/docs/Web/API/RTCDataChannel)

  Represents a bi-directional data channel between two peers of a connection.

- [`RTCDataChannelEvent`](https://developer.mozilla.org/en-US/docs/Web/API/RTCDataChannelEvent)

  Represents events that occur while attaching a [`RTCDataChannel`](https://developer.mozilla.org/en-US/docs/Web/API/RTCDataChannel) to a [`RTCPeerConnection`](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection). The only event sent with this interface is `datachannel`.

- [`RTCSessionDescription`](https://developer.mozilla.org/en-US/docs/Web/API/RTCSessionDescription)

  Represents the parameters of a session. Each `RTCSessionDescription` consists of a description [`type`](https://developer.mozilla.org/en-US/docs/Web/API/RTCSessionDescription/type) indicating which part of the offer/answer negotiation process it describes and of the [SDP](https://developer.mozilla.org/en-US/docs/Glossary/SDP) descriptor of the session.

- [`RTCSessionDescriptionCallback`](https://developer.mozilla.org/en-US/docs/Web/API/RTCSessionDescriptionCallback)

  The RTCSessionDescriptionCallback is passed into the [`RTCPeerConnection`](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection) object when requesting it to create offers or answers.

- [`RTCStatsReport`](https://developer.mozilla.org/en-US/docs/Web/API/RTCStatsReport)

  Provides information detailing statistics for a connection or for  an individual track on the connection; the report can be obtained by  calling [`RTCPeerConnection.getStats()`](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection/getStats). Details about using WebRTC statistics can be found in [WebRTC Statistics API](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_Statistics_API).

- [`RTCIceCandidate`](https://developer.mozilla.org/en-US/docs/Web/API/RTCIceCandidate)

  Represents a candidate Internet Connectivity Establishment ([ICE](https://developer.mozilla.org/en-US/docs/Glossary/ICE)) server for establishing an [`RTCPeerConnection`](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection).

- [`RTCIceTransport`](https://developer.mozilla.org/en-US/docs/Web/API/RTCIceTransport)

  Represents information about an ICE transport.

- [`RTCIceServer`](https://developer.mozilla.org/en-US/docs/Web/API/RTCIceServer)

  Defines how to connect to a single ICE server (such as a [STUN](https://developer.mozilla.org/en-US/docs/Glossary/STUN) or [TURN](https://developer.mozilla.org/en-US/docs/Glossary/TURN) server).

- [`RTCPeerConnectionIceEvent`](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnectionIceEvent)

  Represents events that occur in relation to ICE candidates with the target, usually an [`RTCPeerConnection`](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection). Only one event is of this type: `icecandidate`.

- [`RTCRtpSender`](https://developer.mozilla.org/en-US/docs/Web/API/RTCRtpSender)

  Manages the encoding and transmission of data for a [`MediaStreamTrack`](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack) on an [`RTCPeerConnection`](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection).

- [`RTCRtpReceiver`](https://developer.mozilla.org/en-US/docs/Web/API/RTCRtpReceiver)

  Manages the reception and decoding of data for a [`MediaStreamTrack`](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack) on an [`RTCPeerConnection`](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection).

- [`RTCRtpContributingSource`](https://developer.mozilla.org/en-US/docs/Web/API/RTCRtpContributingSource)

  Contains information about a given contributing source (CSRC)  including the most recent time a packet that the source contributed was  played out.

- [`RTCTrackEvent`](https://developer.mozilla.org/en-US/docs/Web/API/RTCTrackEvent)

  The interface used to represent a [`track`](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection/track_event) event, which indicates that an [`RTCRtpReceiver`](https://developer.mozilla.org/en-US/docs/Web/API/RTCRtpReceiver) object was added to the [`RTCPeerConnection`](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection) object, indicating that a new incoming [`MediaStreamTrack`](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack) was created and added to the `RTCPeerConnection`.

- [`RTCConfiguration`](https://developer.mozilla.org/en-US/docs/Web/API/RTCConfiguration)

  Used to provide configuration options for an [`RTCPeerConnection`](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection).

- [`RTCSctpTransport`](https://developer.mozilla.org/en-US/docs/Web/API/RTCSctpTransport)

  Provides information which describes a Stream Control Transmission Protocol (**[SCTP](https://developer.mozilla.org/en-US/docs/Glossary/SCTP)**) transport and also provides a way to access the underlying Datagram Transport Layer Security (**[DTLS](https://developer.mozilla.org/en-US/docs/Glossary/DTLS)**) transport over which SCTP packets for all of an [`RTCPeerConnection`](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection)'s data channels are sent and received.

- [`RTCSctpTransportState`](https://developer.mozilla.org/en-US/docs/Web/API/RTCSctpTransportState)

  Indicates the state of an [`RTCSctpTransport`](https://developer.mozilla.org/en-US/docs/Web/API/RTCSctpTransport) instance.

### Identity and security

The WebRTC API includes a number of interfaces which are used  to manage security and identity.

- `RTCIdentityProvider`

  Enables a user agent is able to request that an identity assertion be generated or validated.

- [`RTCIdentityAssertion`](https://developer.mozilla.org/en-US/docs/Web/API/RTCIdentityAssertion)

  Represents the identity of the remote peer of the current  connection. If no peer has yet been set and verified this interface  returns `null`. Once set it can't be changed.

- `RTCIdentityProviderRegistrar`

  Registers an identity provider (idP).

- [`RTCIdentityEvent`](https://developer.mozilla.org/en-US/docs/Web/API/RTCIdentityEvent)

  Represents an identity assertion generated by an identity provider (idP). This is usually for an [`RTCPeerConnection`](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection). The only event sent with this type is `identityresult`.

- [`RTCIdentityErrorEvent`](https://developer.mozilla.org/en-US/docs/Web/API/RTCIdentityErrorEvent)

  Represents an error associated with the identity provider (idP). This is usually for an [`RTCPeerConnection`](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection). Two events are sent with this type: `idpassertionerror` and `idpvalidationerror`.

- [`RTCCertificate`](https://developer.mozilla.org/en-US/docs/Web/API/RTCCertificate)

  Represents a certificate that an [`RTCPeerConnection`](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection) uses to authenticate.

### Telephony

These interfaces are related to interactivity with Public-Switched Telephone Networks (PTSNs).

- [`RTCDTMFSender`](https://developer.mozilla.org/en-US/docs/Web/API/RTCDTMFSender)

  Manages the encoding and transmission of Dual-Tone Multi-Frequency ([DTMF](https://developer.mozilla.org/en-US/docs/Glossary/DTMF)) signaling for an [`RTCPeerConnection`](https://developer.mozilla.org/en-US/docs/Web/API/RTCPeerConnection).

- [`RTCDTMFToneChangeEvent`](https://developer.mozilla.org/en-US/docs/Web/API/RTCDTMFToneChangeEvent)

  Used by the [`tonechange`](https://developer.mozilla.org/en-US/docs/Web/API/RTCDTMFSender/tonechange_event) event to indicate that a DTMF tone has either begun or ended. This  event does not bubble (except where otherwise stated) and is not  cancelable (except where otherwise stated).

## Guides

- [Introduction to WebRTC protocols](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API/Protocols)

  This article introduces the protocols on top of which the WebRTC API is built.

- [WebRTC connectivity](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API/Connectivity)

  A guide to how WebRTC connections work and how the various  protocols and interfaces can be used together to build powerful  communication apps.

- [Lifetime of a WebRTC session](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API/Session_lifetime)

  WebRTC lets you build peer-to-peer communication of arbitrary data, audio, or video—or any combination thereof—into a browser application.  In this article, we'll look at the lifetime of a WebRTC session, from  establishing the connection all the way through closing the connection  when it's no longer needed.

- [Signaling and two-way video calling](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API/Signaling_and_video_calling)

  A tutorial and example which turns a WebSocket-based chat system  created for a previous example and adds support for opening video calls  among participants. The chat server's WebSocket connection is used for  WebRTC signaling.

- [Codecs used by WebRTC](https://developer.mozilla.org/en-US/docs/Web/Media/Formats/WebRTC_codecs)

  A guide to the codecs which WebRTC requires browsers to support as  well as the optional ones supported by various popular browsers.  Included is a guide to help you choose the best codecs for your needs.

- [Using WebRTC data channels](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API/Using_data_channels)

  This guide covers how you can use a peer connection and an associated [`RTCDataChannel`](https://developer.mozilla.org/en-US/docs/Web/API/RTCDataChannel) to exchange arbitrary data between two peers.

- [Using DTMF with WebRTC](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API/Using_DTMF)

  WebRTC's support for interacting with gateways that link to  old-school telephone systems includes support for sending DTMF tones  using the [`RTCDTMFSender`](https://developer.mozilla.org/en-US/docs/Web/API/RTCDTMFSender) interface. This guide shows how to do so.

## Tutorials

- [Improving compatibility using WebRTC adapter.js](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API/adapter.js)

  The WebRTC organization [provides on GitHub the WebRTC adapter](https://github.com/webrtc/adapter/) to work around compatibility issues in different browsers' WebRTC  implementations. The adapter is a JavaScript shim which lets your code  to be written to the specification so that it will "just work" in all  browsers with WebRTC support.

- [Taking still photos with WebRTC](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API/Taking_still_photos)

  This article shows how to use WebRTC to access the camera on a  computer or mobile phone with WebRTC support and take a photo with it.

- [A simple RTCDataChannel sample](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API/Simple_RTCDataChannel_sample)

  The [`RTCDataChannel`](https://developer.mozilla.org/en-US/docs/Web/API/RTCDataChannel) interface is a feature which lets you open a channel between two peers  over which you may send and receive arbitrary data. The API is  intentionally similar to the [WebSocket API](https://developer.mozilla.org/en-US/docs/Web/API/WebSocket_API), so that the same programming model can be used for each.

## Resources

### Protocols

#### WebRTC-proper protocols

- [Application Layer Protocol Negotiation for Web Real-Time Communications](http://datatracker.ietf.org/doc/draft-ietf-rtcweb-alpn/)
- [WebRTC Audio Codec and Processing Requirements](http://datatracker.ietf.org/doc/draft-ietf-rtcweb-audio/)
- [RTCWeb Data Channels](http://datatracker.ietf.org/doc/draft-ietf-rtcweb-data-channel/)
- [RTCWeb Data Channel Protocol](http://datatracker.ietf.org/doc/draft-ietf-rtcweb-data-protocol/)
- [Web Real-Time Communication (WebRTC): Media Transport and Use of RTP](http://datatracker.ietf.org/doc/draft-ietf-rtcweb-rtp-usage/)
- [WebRTC Security Architecture](http://datatracker.ietf.org/doc/draft-ietf-rtcweb-security-arch/)
- [Transports for RTCWEB](http://datatracker.ietf.org/doc/draft-ietf-rtcweb-transports/)

#### Related supporting protocols

- [Interactive  Connectivity Establishment (ICE): A Protocol for Network Address  Translator (NAT) Traversal for Offer/Answer Protocol](https://tools.ietf.org/html/rfc5245)
- [Session Traversal Utilities for NAT (STUN)](https://tools.ietf.org/html/rfc5389)
- [URI Scheme for the Session Traversal Utilities for NAT (STUN) Protocol](https://tools.ietf.org/html/rfc7064)
- [Traversal Using Relays around NAT (TURN) Uniform Resource Identifiers](https://tools.ietf.org/html/rfc7065)
- [An Offer/Answer Model with Session Description Protocol (SDP)](https://tools.ietf.org/html/rfc3264)
- [Session Traversal Utilities for NAT (STUN) Extension for Third Party Authorization](https://datatracker.ietf.org/doc/draft-ietf-tram-turn-third-party-authz/)

#### WebRTC statistics

- [WebRTC Statistics API](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_Statistics_API)

## Specifications

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article18-folder/t1.jpg)

In additions to these specifications defining the API needed to use WebRTC, there are several protocols, listed under [resources](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API#Protocols).