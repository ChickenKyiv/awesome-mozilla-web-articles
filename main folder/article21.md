# WebXR Device API

> **Draft**
>     This page is not complete.

**WebXR** is a group of  standards which are used together to support rendering 3D scenes to  hardware designed for presenting virtual worlds (**virtual reality**, or **VR**), or for adding graphical imagery to the real world, (**augmented reality**, or **AR**). The **WebXR Device API** implements the core of the WebXR feature set, managing the selection of output  devices, render the 3D scene to the chosen device at the appropriate  frame rate, and manage motion vectors created using input controllers.

WebXR-compatible devices include fully-immersive 3D headsets with  motion and orientation tracking, eyeglasses which overlay graphics atop  the real world scene passing through the frames, and handheld mobile  phones which augment reality by capturing the world with a camera and  augment that scene with computer-generated imagery.

To accomplish these things, the WebXR Device API provides the following key capabilities:

- Find compatible VR or AR output devices
- Render a 3D scene to the device at an appropriate frame rate
- (Optionally) mirror the output to a 2D display
- Create vectors representing the movements of input controls

At the most basic level, a scene is presented in 3D by computing the  perspective to apply to the scene in order to render it from the  viewpoint of each of the user's eyes, taking into account the typical  distance between the eyes, then rendering the scene twice, once for each eye. The resulting images (or image, if the scene is rendered twice  onto a single frame, half per eye) are then displayed to the user.

Since [WebGL](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API) is used for rendering the 3D world into the WebXR session, you should  first be familiar with WebGL's general usage, and with the basics of 3D  graphics in general. You most likely will not directly use the WebGL  API, instead making use of one of the frameworks or libraries that are  built atop WebGL to make it more convenient to use. Among the most  popular of these is [three.js](https://threejs.org/).

A particular benefit to using a library rather than directly using  the WebGL API is that libraries tend to implement virtual camera  functionality. OpenGL (and thus WebGL by extension) does not directly  offer a camera view, using a library that simulates one on your behalf  can make your job much, much easier, especially when building code that  allows free movement through your virtual world.

## Important health and safety reminders

Because the entire act of creating a virtual 3D world is, in essence, a trick which takes advantage of our understanding of how eyes collect  light and how the brain interprets the collected data, it is important  to keep in mind that as such, software designers and developers have a  responsibility to be even more careful than usual to ensure that the  results are correct.

Defects, misalignments, or distortion can confuse the eyes and the  brain, resulting in anything from aching eyes or headache to in some  cases vertigo, dizziness, or potentially severe nausea. It's also  important to be alert for anything you may display that may have the  potential to trigger seizures, given the all-encompassing nature of VR  goggles; the user may not be able to quickly look away from the imagery  you're presenting if it's causing distress.

If you have any content that may be of risk to any users, you should provide a warning message. Better to be safe than sorry!

## WebXR Device API concepts and usage

### WebXR: AR and VR

Example WebXR hardware setup

 ![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article1-folder/hw-setup.png)

While the older [WebVR API](https://developer.mozilla.org/en-US/docs/Web/API/WebVR_API) was designed solely to support Virtual Reality (VR), WebXR provides support for both VR and Augmented Reality (AR) on the web. Support for AR  functionality is added by the WebXR Augmented Reality Module.

A typical XR device can have either 3 or 6 degrees of freedom and might or might not have an external positional sensor.

The equipment may also include an accelerometer, barometer, or other  sensors which are used to sense when the user moves through space,  rotates their head, or the like.

### WebXR application lifecycle

Most applications using WebXR will follow a similar overall design pattern:

1. Check to see if the user's device and browser are both capable of presenting the XR experience you want to provide. 

   1. Make sure the WebXR API is available; if [`navigator.xr`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/xr) is undefined, you can assume the user's browser and/or device doesn't  support WebXR. If it's not supported, disable any user interface used to activate XR features and abort any attempts to enter XR mode.
   2. Call [`navigator.xr.isSessionSupported()`](https://developer.mozilla.org/en-US/docs/Web/API/XR/isSessionSupported), specifying the WebXR experience mode you want to provide: `inline`, `immersive-vr`, or `immersive-ar`, in order to determine whether or not the type of session you wish to provide is available.
   3. If the session type you want to use is available, provide the appropriate interface to the user to allow them to activate it.

2. When the user requests the activation of WebXR functionality by engaging with the user interface enabled above, request an [`XRSession`](https://developer.mozilla.org/en-US/docs/Web/API/XRSession) using the desired mode. This is done by calling [`navigator.xr.requestSession()`](https://developer.mozilla.org/en-US/docs/Web/API/XR/requestSession), again specifying the string indicating the mode you want to enable: `inline`, `immersive-vr`, or `immersive-ar`.

3. If the promise returned by `requestSession()` resolves, use the new`XRSession`

    to run the frame loop for the entire duration of the WebXR experience. 

   1. Call the [`XRSession`](https://developer.mozilla.org/en-US/docs/Web/API/XRSession) method [`requestAnimationFrame()`](https://developer.mozilla.org/en-US/docs/Web/API/XRSession/requestAnimationFrame) to schedule the first frame render for the XR device.
   2. Each `requestAnimationFrame()` callback should use the information provided about the objects located in the 3D world to render the frame using WebGL.
   3. Keep calling [`requestAnimationFrame()`](https://developer.mozilla.org/en-US/docs/Web/API/XRSession/requestAnimationFrame) from within the callback to schedule each successive frame to be rendered.

4. When the time comes, end the XR session; otherwise, continue the loop until the user chooses to exit XR mode. 

   1. To end the XR session yourself, call [`XRSession.end()`](https://developer.mozilla.org/en-US/docs/Web/API/XRSession/end).
   2. Include a handler for the [`XRSession`](https://developer.mozilla.org/en-US/docs/Web/API/XRSession) event [`end`](https://developer.mozilla.org/en-US/docs/Web/API/XRSession/end_event) event to be informed when the session is ending, regardless of whether  your code, the user, or the browser initiated the termination of the  session.

### Permissions and security

The WebXR Device API is subject to a number of permission and  security controls. While not onerous, they are worth being aware of.  These mostly revolve around the fully-immersive `immersive-vr` session mode, but there are things to be aware of when setting up an AR session, as well.

#### Immersive presentation of VR

First, any requests to activate the `immersive-vr` mode  are rejected if the domain issuing the request does not have permission  to enable an immersive session. This permission comes from the `xr-spatial-tracking` [feature policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Feature_Policy).

Once that check is passed, the request to enter `immersive-vr` mode is allowed if all of the following are true:

- The `requestSession()` call was issued by code executing within the handler for a user event, or the from the startup code for a user-launched [web application](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps).
- The document is considered trustworthy, in that it is responsible and is both currently active and has focus.
- The user's intent to enter immersive VR mode is well understood; see [User intent](https://developer.mozilla.org/en-US/docs/Web/API/WebXR_Device_API#User_intent) below for details.

If all of that is true, the promise returned by `requestSession()` is resolved, and the new [`XRSession`](https://developer.mozilla.org/en-US/docs/Web/API/XRSession) object is passed into the fulfillment handler. Otherwise, an appropriate exception is thrown, such as `SecurityError` if the document doesn't have permission to enter immersive mode.

#### Inline presentation

When you request an [`XRSession`](https://developer.mozilla.org/en-US/docs/Web/API/XRSession) with the mode set to `inline`, and any features are required or requested, the browser will only allow the session to be created if the call to [`requestSession()`](https://developer.mozilla.org/en-US/docs/Web/API/XR/requestSession) was made by code which is executing expressly due to **user intent**.

Specifically:

- If the `requestSession()` call isn't coming from within  the handler executed in response to a user event, and is not being  issued while launching a web application, the request is denied and `false` is delivered to the promise's fulfillment handler.
- If the document making the request isn't the one which is responsible for the script, the request is denied.
- If the document making the request isn't trustworthy, the request is denied and `false` is returned through the promise's fulfillment routine. A trustworthy  document is one which is both responsible and active, and which  currently has focus.
- If the user's intent to open an inline XR presentation is not well understood, the request is denied. Understanding of the [user's intent](https://developer.mozilla.org/en-US/docs/Web/API/WebXR_Device_API#User_intent) may be either implicit or explicit.

> **Note:** Additional requirements may be put into effect due to the specific features requested by the options object when calling `requestSession()`.

#### User intent

**User intent** is the concept of whether or not an  action being performed by code is being performed because of something  the user intends to do or not. There are two kinds of user intent: **implicit** and **explicit**.

**Explicit user intent** (explicit user consent) is granted when the user has specifically and expressly been asked for permission to perform an action.

**Implicit user intent** (implicit user consent) is assumed if either of the following scenarios is the case:

- The user has interacted with the document in some way which has in  turn caused your request to occur. For example, if you have an "Enter XR mode" button, and the user clicks it, calling `requestSession()` from the button's [`click`](https://developer.mozilla.org/en-US/docs/Web/API/Element/click_event) event handler will permitted.
- If your code is executing during the launch of a web application,  the runtime may consider the act of launching your web application to  qualify as user intent.

### WebXR availability

As a new and still in development API, WebXR support is limited to  specific devices and browsers; and even on those, it may not be enabled  by default. There may be options available to allow you to experiment  with WebXR even if you don't have a compatible system, however.

#### WebXR polyfill

The team designing the WebXR specification has published a [WebXR polyfill](https://github.com/immersive-web/webxr-polyfill) which you can use to simulate WebXR on browsers which don't have support for the WebXR APIs. If the browser supports the older [WebVR API](https://developer.mozilla.org/en-US/docs/Web/API/WebVR_API), that is used. Otherwise, the polyfill falls back to an implementation which uses Google's Cardboard VR API.

The polyfill is maintained alongside the specification, and is kept  up to date with the specification. Additionally, it is updated to  maintain compatibility with browsers as their support for WebXR and  other technologies related to it and to the implementation of the  polyfill change over time.

Be sure to read the readme carefully; the polyfill comes in several  versions depending on what degree of compatibility with newer JavaScript features your target browsers include.

#### WebXR API Emulator extension

The [Mozilla WebXR team](https://mixedreality.mozilla.org/) has created a [WebXR API Emulator](https://blog.mozvr.com/webxr-emulator-extension/) browser extension, compatible with both Firefox and Chrome, which emulates the  WebXR API, simulating a variety of compatible devices such as the HTC  Vive, the Oculus Go and Oculus Quest, Samsung Gear, and Google  Cardboard. With the extension in place, you can open up a developer  tools panel that lets you control the position and orientation of the  headset and any hand controllers, as well as button presses on the  controllers.

While somewhat awkward compared to using an actual headset, this  makes it possible to experiment with and developer WebXR code on a  desktop computer, where WebXR isn't normally available. It also lets you perform some basic testing before taking your code to a real device. Be aware, however, that the emulator does not yet completely emulate all  of the WebXR API, so you may run into problems you're not expecting.  Again, carefully read the readme file and make sure you're aware of the  limitations before you begin.

> **Important:** You should *always* test your code on actual AR and/or VR hardware before releasing or shipping a product! Emulated, simulated, or polyfilled environments are *not* an adequate substitute for actual testing on physical devices.

Download the WebXR API Emulator for your supported browser below:

- [Google Chrome](https://chrome.google.com/webstore/detail/webxr-api-emulator/mjddjgeghkdijejnciaefnkjmkafnnje)
- [Mozilla Firefox](https://addons.mozilla.org/en-US/firefox/addon/webxr-api-emulator/)

The [source code for the extension](https://github.com/MozillaReality/WebXR-emulator-extension) is also available on GitHub.

## Accessing the WebXR API

To gain access to the WebXR API within the context of a given window, use the [`navigator.xr`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/xr) property.

- [`navigator.xr`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/xr) Read only 

  This property, added to the [`Navigator`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator) interface, returns the [`XR`](https://developer.mozilla.org/en-US/docs/Web/API/XR) object through which the WebXR API is exposed. If this property is missing or `null`, WebXR is not available.

## WebXR interfaces

- [`XR`](https://developer.mozilla.org/en-US/docs/Web/API/XR)

  The [`navigator.xr`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/xr) property returns the window's instance of [`XR`](https://developer.mozilla.org/en-US/docs/Web/API/XR), which is the mechanism by which your code accesses the WebXR API. Using the `XR` interface, you can create [`XRSession`](https://developer.mozilla.org/en-US/docs/Web/API/XRSession)s to represent actual AR and/or VR sessions.

- [`XRFrame`](https://developer.mozilla.org/en-US/docs/Web/API/XRFrame)

  While presenting an XR session, the state of all tracked objects which make up the session are represented by an `XRFrame`. To get an `XRFrame`, call the session's [`requestAnimationFrame()`](https://developer.mozilla.org/en-US/docs/Web/API/XRSession/requestAnimationFrame) method, providing a callback which will be called with the `XRFrame` once available. Events which communicate tracking states will also use `XRFrame` to contain that information.

- [`XRRenderState`](https://developer.mozilla.org/en-US/docs/Web/API/XRRenderState)

  Provides a set of configurable properties which change how the imagery output by an `XRSession` is composited.

- [`XRSession`](https://developer.mozilla.org/en-US/docs/Web/API/XRSession)

  Provides the interface for interacting with XR hardware. Once an `XRSession` is obtained from [`XR.requestSession()`](https://developer.mozilla.org/en-US/docs/Web/API/XR/requestSession), the session can be used to check the position and orientation of the  viewer, query the device for environment information, and present the  virtual or augmented world to the user.

- [`XRSpace`](https://developer.mozilla.org/en-US/docs/Web/API/XRSpace)

  `XRSpace` is an opaque base class on which all virtual  coordinate system interfaces are based. Positions in WebXR are always  expressed in relation to a particular `XRSpace` at the time at which a particular `XFrame` takes place. The space's coordinate system has its origin at the a given physical position.

- [`XRReferenceSpace`](https://developer.mozilla.org/en-US/docs/Web/API/XRReferenceSpace)

  A subclass of [`XRSpace`](https://developer.mozilla.org/en-US/docs/Web/API/XRSpace) which is used to identify a spatial relationship in relation to the user's physical environment. The `XRReferenceSpace` coordinate system is expected to remain unchanged through the lifespan of the [`XRSession`](https://developer.mozilla.org/en-US/docs/Web/API/XRSession).The world has no boundaries and extends infinitely in every direction.

- [`XRBoundedReferenceSpace`](https://developer.mozilla.org/en-US/docs/Web/API/XRBoundedReferenceSpace)

  `XRBoundedReferenceSpace` extends the [`XRReferenceSpace`](https://developer.mozilla.org/en-US/docs/Web/API/XRReferenceSpace) coordinate system to further include support for a finite world with set boundaries. Unlike `XRReferenceSpace`, the origin must be located on the floor (that is, *y* = 0 at the floor). The x and z components of the origin are typically  presumed to be located at or near the center of the room or surface.

- [`XRView`](https://developer.mozilla.org/en-US/docs/Web/API/XRView)

  Represents a single view into the XR scene for a particular frame. Each `XRView` corresponds to the video display surface used to present the scene to the user. For example, a given XR device might have two views: one for the left eye  and one for the right. Each view has an offset used to shift the  position of the view relative to the camera, in order to allow for  creating stereographic effects.

- [`XRViewport`](https://developer.mozilla.org/en-US/docs/Web/API/XRViewport)

  Describes a viewport. A viewport is a rectangular portion of a graphic surface.

- [`XRRigidTransform`](https://developer.mozilla.org/en-US/docs/Web/API/XRRigidTransform)

  A transform defined using a position and orientation in the virtual space's coordinate system as described by the [`XRSpace`](https://developer.mozilla.org/en-US/docs/Web/API/XRSpace).

- [`XRPose`](https://developer.mozilla.org/en-US/docs/Web/API/XRPose)

  Describes a position and orientation in space relative to an [`XRSpace`](https://developer.mozilla.org/en-US/docs/Web/API/XRSpace).

- [`XRViewerPose`](https://developer.mozilla.org/en-US/docs/Web/API/XRViewerPose)

  Based on [`XRPose`](https://developer.mozilla.org/en-US/docs/Web/API/XRPose), `XRViewerPose` specifies the state of a viewer of the WebXR scene as indicated by the XR device. Included is an array of [`XRView`](https://developer.mozilla.org/en-US/docs/Web/API/XRView) objects, each representing one perspective on the scene. For example,  it takes two views to create the stereoscopic view as perceived by human vision—one for the left eye and a second for the right eye. One view is offset to the left slightly from the viewer's position, and the other  view is offset to the right by the same distance. The view list can also be used to represent the perspectives of each of the spectators of a  scene, in a multi-user environment.

- [`XRInputSource`](https://developer.mozilla.org/en-US/docs/Web/API/XRInputSource)

  Represents any input device the user can use to perform targeted  actions within the same virtual space as the viewer. Input sources may  include devices such as hand controllers, optical tracking systems, and  other devices which are explicitly associated with the XR device. Other  input devices such as keyboards, mice, and gamepads are not presented  as `XRInputSource` instances.

- [`XRWebGLLayer`](https://developer.mozilla.org/en-US/docs/Web/API/XRWebGLLayer)

  A layer which serves as a [WebGL](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API) frame buffer into which a scene's view is rendered. Using WebGL to render the scene gains substantial performance benefits due to graphics  acceleration.

### Event interfaces

The following interfaces are used to represent the events used by the WebXR API.

- `XRInputSourceEvent`

  Sent when the state of an [`XRInputSource`](https://developer.mozilla.org/en-US/docs/Web/API/XRInputSource) changes. This can happen, for example, when the position and/or  orientation of the device changes, or when buttons are pressed or  released.

- `XRInputSourcesChangeEvent`

  Sent to indicate that the set of available input sources has changed for the [`XRSession`](https://developer.mozilla.org/en-US/docs/Web/API/XRSession).

- `XRReferenceSpaceEvent`

  Sent when the state of an [`XRReferenceSpace`](https://developer.mozilla.org/en-US/docs/Web/API/XRReferenceSpace) changes.

- `XRSessionEvent`

  Sent to indicate that the state of an [`XRSession`](https://developer.mozilla.org/en-US/docs/Web/API/XRSession) has changed. For example, if the position and/or orient

## Extensions to the WebGL API

The WebGL API is extended by the WebXR specification to augment the  WebGL context to allow it to be used to render views for display by a  WebXR device.

- `WebGLRenderingContextBase.makeXRCompatibile()`

  Configures the WebGL context to be compatible with WebXR. If the context was not initially created with the `xrCompatible` property set to `true`, you must call `makeXRCompatible()` prior to attempting to use the WebGL context for WebXR rendering. Returns a [`promise`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/promise) which resolves once the context has been prepared, or is rejected if the context cannot be configured for use by WebXR.

## Guides and tutorials

The following guides and tutorials are a great resource to learn how  to comprehend WebXR and the underlying 3D and VR/AR graphics concepts.

- [Fundamentals of WebXR](https://developer.mozilla.org/en-US/docs/Web/API/WebXR_Device_API/Fundamentals)

  Before diving into the details of how to create content using  WebXR, it may be helpful to read this overview of the technology, which  includes introductions to terminology that may be unfamiliar to you, or  which may be used in a new way.

- [Matrix math for the web](https://developer.mozilla.org/en-US/docs/Web/API/WebGL_API/Matrix_math_for_the_web)

  A guide covering how matrices can be used on the web, including  both for CSS transforms and for WebGL purposes, as well as to handle the positioning and orientation of objects in WebXR contexts.

- Setting up and shutting down a WebXR session

  Before actually presenting a scene using an XR device such as a  headset or goggles, you need to create a WebXR session bound to a  rendering layer that draws the scene for presentation in each of the XR  device's displays so that the 3D effect can be presented to the user.  This guide covers how to create and stop WebXR sessions.

- [Geometry and reference spaces in WebXR](https://developer.mozilla.org/en-US/docs/Web/API/WebXR_Device_API/Geometry)

  In this guide, the required concepts of 3D geometry are briefly  reviewed, and the fundamentals of how that geometry is represented in  WebXR are detailed. Learn how reference spaces are used to position  objects—and the viewer—and the differences among the available types of  reference space, as well as their use cases.

- [Spatial tracking in WebXR](https://developer.mozilla.org/en-US/docs/Web/API/WebXR_Device_API/Spatial_tracking)

  This guide describes how objects—including the user's body and its  parts—are located in space, and how their movement and orientation  relative to one another is monitored and managed over time. This article explains the relationship between spaces, poses, viewers, and views.

- [Rendering and the WebXR frame loop](https://developer.mozilla.org/en-US/docs/Web/API/WebXR_Device_API/Rendering)

  Starting with how you schedule frames to be rendered, this guide  then continues to cover how to determine the placement of objects in the view and how to then render them into the WebGL buffer used for each of the two eyes' views of the scene.

- [Viewpoints and viewers: Simulating cameras in WebXR ](https://developer.mozilla.org/en-US/docs/Web/API/WebXR_Device_API/Cameras)

  WebGL (and therefore WebXR) doesn't really have a concept of a  camera, which is the traditional concept used to represent a viewpoint  in 3D graphics. In this article, we see how to simulate a camera and how to create the illusion of moving a viewer through a world in which the  viewer doesn't really move.

- [Movement, orientation, and motion: A WebXR example](https://developer.mozilla.org/en-US/docs/Web/API/WebXR_Device_API/Movement_and_motion)

  In this example and tutorial, we use information learned throughout the WebXR documentation to create a scene containing a rotating cube  which the user can move around using both VR headset and keyboard and  mouse.

- [Using bounded reference spaces](https://developer.mozilla.org/en-US/docs/Web/API/WebXR_Device_API/Bounded_reference_spaces)

  In this article, we examine how to use a `bounded-floor` reference space to define the boundaries of where the viewer can safely move  about without leaving the area tracked by their XR hardware or colliding with a physical obstacle. On devices which support it, `bounded-floor` can be a useful tool in your repertoire.

- [WebXR performance guide](https://developer.mozilla.org/en-US/docs/Web/API/WebXR_Device_API/Performance)

  Recommendations and tips to help you optimize the performance of your WebXR application.

- [Inputs and input sources](https://developer.mozilla.org/en-US/docs/Web/API/WebXR_Device_API/Inputs)

  A guide to input sources and how to efficiently manage the input  devices being used to control the WebXR session, and how to receive and  process user inputs from those devices.

- Supporting gamepads in WebXR applications

  WebXR implements the Gamepad API to allow gamepads connected to the XR device to be used as input controls. This guide describes how this  works.

## Specifications

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article21-folder/t1.jpg)

## Browser compatibility

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article21-folder/t2.jpg)