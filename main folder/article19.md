# WebVR API

> **Deprecated**
> This feature is no longer  recommended. Though some browsers might still support it, it may have  already been removed from the relevant web standards, may be in the  process of being dropped, or may only be kept for compatibility  purposes. Avoid using it, and update existing code if possible; see the [compatibility table](https://developer.mozilla.org/en-US/docs/Web/API/WebVR_API#Browser_compatibility) at the bottom of this page to guide your decision. Be aware that this feature may cease to work at any time.

> **Note:** WebVR API is replaced by [WebXR API](https://developer.mozilla.org/en-US/docs/Web/API/WebXR_API). WebVR was never ratified as a standard, was implemented and enabled by  default in very few browsers and supported a small number of devices.

WebVR provides support for exposing virtual reality  devices — for example, head-mounted displays like the Oculus Rift or HTC Vive — to web apps, enabling developers to translate position and  movement information from the display into movement around a 3D scene.  This has numerous, interesting applications, from virtual product tours  and interactive training apps to immersive first-person games.

## Concepts and usage

Any VR devices attached to your computer will be returned by the [`Navigator.getVRDisplays()`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/getVRDisplays) method; each one will be represented by a [`VRDisplay`](https://developer.mozilla.org/en-US/docs/Web/API/VRDisplay) object.

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article1-folder/hw-setup.png)

[`VRDisplay`](https://developer.mozilla.org/en-US/docs/Web/API/VRDisplay) is the central interface in the WebVR API — via its properties and methods you can access functionality to:

- Retrieve useful information to allow us to identify the display,  what capabilities it has, controllers associated with it, and more.
- Retrieve [`frame data`](https://developer.mozilla.org/en-US/docs/Web/API/VRFrameData) for each frame of content you you want to present in a display, and submit those frames for display at a consistent rate.
- Start and stop presenting to the display.

A typical (simple) WebVR app would work like so:

1. [`Navigator.getVRDisplays()`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/getVRDisplays) is used to get a reference to your VR display.
2. [`VRDisplay.requestPresent()`](https://developer.mozilla.org/en-US/docs/Web/API/VRDisplay/requestPresent) is used to start presenting to the VR display.
3. WebVR's dedicated [`VRDisplay.requestAnimationFrame()`](https://developer.mozilla.org/en-US/docs/Web/API/VRDisplay/requestAnimationFrame) method is used to run the app's rendering loop at the correct refresh rate for the display.
4. Inside the rendering loop, you grab the data required to display the current frame ([`VRDisplay.getFrameData()`](https://developer.mozilla.org/en-US/docs/Web/API/VRDisplay/getFrameData)), draw the displayed scene twice — once for the view in each eye, then  submit the rendered view to the display to show to the user ([`VRDisplay.submitFrame()`](https://developer.mozilla.org/en-US/docs/Web/API/VRDisplay/submitFrame)).

In addition, WebVR 1.1 adds a number of events on the [`Window`](https://developer.mozilla.org/en-US/docs/Web/API/Window) object to allow JavaScript to respond to changes to the status of the display.

> **Note**: You can find a lot more out about how the API works in our [Using the WebVR API](https://developer.mozilla.org/en-US/docs/Web/API/WebVR_API/Using_the_WebVR_API) and [WebVR Concepts](https://developer.mozilla.org/en-US/docs/Web/API/WebVR_API/Concepts) articles.

### Using controllers: Combining WebVR with the Gamepad API

Many WebVR hardware setups feature controllers that go along with the headset. These can be used in WebVR apps via the [Gamepad API](https://developer.mozilla.org/en-US/docs/Web/API/Gamepad_API), and specifically the [Gamepad Extensions API](https://developer.mozilla.org/en-US/docs/Web/API/Gamepad_API#Experimental_Gamepad_extensions) that adds API features for accessing [controller pose](https://developer.mozilla.org/en-US/docs/Web/API/GamepadPose), [haptic actuators](https://developer.mozilla.org/en-US/docs/Web/API/GamepadHapticActuator), and more.

> **Note**: Our [Using VR controllers with WebVR](https://developer.mozilla.org/en-US/docs/Web/API/WebVR_API/Using_VR_controllers_with_WebVR) article explains the basics of how to use VR controllers with WebVR apps.

## WebVR Interfaces

- [`VRDisplay`](https://developer.mozilla.org/en-US/docs/Web/API/VRDisplay)

  Represents any VR device supported by this API. It includes generic information such as device IDs and descriptions, as well as methods for starting to present a VR scene, retrieving eye parameters and display  capabilities, and other important functionality.

- [`VRDisplayCapabilities`](https://developer.mozilla.org/en-US/docs/Web/API/VRDisplayCapabilities)

  Describes the capabilities of a [`VRDisplay`](https://developer.mozilla.org/en-US/docs/Web/API/VRDisplay) — it's features can be used to perform VR device capability tests, for example can it return position information.

- [`VRDisplayEvent`](https://developer.mozilla.org/en-US/docs/Web/API/VRDisplayEvent)

  Represents the event object of WebVR-related events (see the [window object extensions](https://developer.mozilla.org/en-US/docs/Web/API/WebVR_API#Window) listed below).

- [`VRFrameData`](https://developer.mozilla.org/en-US/docs/Web/API/VRFrameData)

  Represents all the information needed to render a single frame of a VR scene; constructed by [`VRDisplay.getFrameData()`](https://developer.mozilla.org/en-US/docs/Web/API/VRDisplay/getFrameData).

- [`VRPose`](https://developer.mozilla.org/en-US/docs/Web/API/VRPose)

  Represents the position state at a given timestamp (which includes orientation, position, velocity, and acceleration.)

- [`VREyeParameters`](https://developer.mozilla.org/en-US/docs/Web/API/VREyeParameters)

  Provides access to all the information required to correctly render a scene for each given eye, including field of view information.

- [`VRFieldOfView`](https://developer.mozilla.org/en-US/docs/Web/API/VRFieldOfView)

  Represents a field of view defined by 4 different degree values describing the view from a center point.

- [`VRLayerInit`](https://developer.mozilla.org/en-US/docs/Web/API/VRLayerInit)

  Represents a layer to be presented in a [`VRDisplay`](https://developer.mozilla.org/en-US/docs/Web/API/VRDisplay).

- [`VRStageParameters`](https://developer.mozilla.org/en-US/docs/Web/API/VRStageParameters)

  Represents the values describing the the stage area for devices that support room-scale experiences.

### Extensions to other interfaces

The WebVR API extends the following APIs, adding the listed features.

#### Gamepad

- [`Gamepad.displayId`](https://developer.mozilla.org/en-US/docs/Web/API/Gamepad/displayId) Read only 

  Returns the [`VRDisplay.displayId`](https://developer.mozilla.org/en-US/docs/Web/API/VRDisplay/displayId) of the associated [`VRDisplay`](https://developer.mozilla.org/en-US/docs/Web/API/VRDisplay) — the `VRDisplay` that the gamepad is controlling the displayed scene of.

#### Navigator

- [`Navigator.activeVRDisplays`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/activeVRDisplays) Read only 

  Returns an array containing every [`VRDisplay`](https://developer.mozilla.org/en-US/docs/Web/API/VRDisplay) object that is currently presenting ([`VRDisplay.ispresenting`](https://developer.mozilla.org/en-US/docs/Web/API/VRDisplay/ispresenting) is `true`).

- [`Navigator.getVRDisplays()`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/getVRDisplays)

  Returns a promise that resolves to an array of [`VRDisplay`](https://developer.mozilla.org/en-US/docs/Web/API/VRDisplay) objects representing any available VR displays connected to the computer.

#### Window events

- [`Window.onvrdisplaypresentchange`](https://developer.mozilla.org/en-US/docs/Web/API/Window/onvrdisplaypresentchange)

  Represents an event handler that will run when the presenting state of a VR display changes — i.e. goes from presenting to not presenting  or vice versa (when the `vrdisplaypresentchange` event fires).

- [`Window.onvrdisplayconnect`](https://developer.mozilla.org/en-US/docs/Web/API/Window/onvrdisplayconnect)

  Represents an event handler that will run when a compatible VR display has been connected to the computer (when the `vrdisplayconnect` event fires).

- [`Window.onvrdisplaydisconnect`](https://developer.mozilla.org/en-US/docs/Web/API/Window/onvrdisplaydisconnect)

  Represents an event handler that will run when a compatible VR display has been disconnected from the computer (when the `vrdisplaydisconnect` event fires).

- [`Window.onvrdisplayactivate`](https://developer.mozilla.org/en-US/docs/Web/API/Window/onvrdisplayactivate)

  Represents an event handler that will run when a display is able to be presented to (when the `vrdisplayactivate` event fires), for example if an HMD has been moved to bring it out of standby, or woken up by being put on.

- [`Window.onvrdisplaydeactivate`](https://developer.mozilla.org/en-US/docs/Web/API/Window/onvrdisplaydeactivate)

  Represents an event handler that will run when a display can no longer be presented to (when the `vrdisplaydeactivate` event fires), for example if an HMD has gone into standby or sleep mode due to a period of inactivity.

- [`Window.onvrdisplayblur`](https://developer.mozilla.org/en-US/docs/Web/API/Window/onvrdisplayblur)

  Represents an event handler that will run when presentation to a  display has been paused for some reason by the browser, OS, or VR  hardware (when the `vrdisplayblur` event fires) — for example, while the user is interacting with a system menu or browser, to prevent tracking or loss of experience.

- [`Window.onvrdisplayfocus`](https://developer.mozilla.org/en-US/docs/Web/API/Window/onvrdisplayfocus)

  Represents an event handler that will run when presentation to a display has resumed after being blurred (when the `vrdisplayfocus` event fires).

## Examples

You can find a number of examples at these locations:

- [webvr-tests](https://github.com/mdn/webvr-tests) — very simple examples to accompany the MDN WebVR documentation.
- [Carmel starter kit](https://github.com/facebook/Carmel-Starter-Kit) — nice simple, well-commented examples that go along with Carmel, Facebook's WebVR browser.
- [WebVR.info samples](https://webvr.info/samples/) — slightly more in-depth examples plus source code
- [WebVR.rocks Firefox demos](https://webvr.rocks/firefox#demos) — showcase examples
- [A-Frame homepage](https://aframe.io/) — examples showing A-Frame usage

## Specifications

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article19-folder/t1.jpg)



## Browser compatibility

### `Navigator.getVRDisplays`

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article19-folder/t2.jpg)