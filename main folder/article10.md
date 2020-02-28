# Web Animations API

> **This is an [experimental technology](https://developer.mozilla.org/en-US/docs/MDN/Contribute/Guidelines/Conventions_definitions#Experimental)**
> Check the [Browser compatibility table](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API#Browser_compatibility) carefully before using this in production.

The **Web Animations API** allows for synchronizing and  timing changes to the presentation of a Web page, i.e. animation of DOM  elements. It does so by combining two models: the Timing Model and the  Animation Model.

## Concepts and usage

The Web Animations API provides a common language for browsers and  developers to describe animations on DOM elements. To get more  information on the concepts behind the API and how to use it, read [Using the Web Animations API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API/Using_the_Web_Animations_API).

## Web Animations interfaces



- [`Animation`](https://developer.mozilla.org/en-US/docs/Web/API/Animation)

  Provides playback controls and a timeline for an animation node or source. Can take an object created with the [`KeyframeEffect()`](https://developer.mozilla.org/en-US/docs/Web/API/KeyframeEffect/KeyframeEffect) constructor.

- [`KeyframeEffect`](https://developer.mozilla.org/en-US/docs/Web/API/KeyframeEffect)

  Describes sets of animatable properties and values, called **keyframes** and their [timing options](https://developer.mozilla.org/en-US/docs/Web/API/Web_Animations_API/Animation_timing_options)**.** These can then be played using the [`Animation()`](https://developer.mozilla.org/en-US/docs/Web/API/Animation/Animation) constructor.

- [`AnimationTimeline`](https://developer.mozilla.org/en-US/docs/Web/API/AnimationTimeline)

  Represents the timeline of animation. This interface exists to define timeline features (inherited by [`DocumentTimeline`](https://developer.mozilla.org/en-US/docs/Web/API/DocumentTimeline) and future timeline objects) and is not itself accessed by developers.

- [`AnimationEvent`](https://developer.mozilla.org/en-US/docs/Web/API/AnimationEvent)

  Actually part of CSS Animations.

- [`DocumentTimeline`](https://developer.mozilla.org/en-US/docs/Web/API/DocumentTimeline)

  Represents animation timelines, including the default document timeline (accessed using the [`Document.timeline`](https://developer.mozilla.org/en-US/docs/Web/API/Document/timeline) property).

- [`EffectTiming`](https://developer.mozilla.org/en-US/docs/Web/API/EffectTiming)

  [`Element.animate()`](https://developer.mozilla.org/en-US/docs/Web/API/Element/animate), [`KeyframeEffectReadOnly.KeyframeEffectReadOnly()`](https://developer.mozilla.org/en-US/docs/Web/API/KeyframeEffectReadOnly/KeyframeEffectReadOnly), and [`KeyframeEffect.KeyframeEffect()`](https://developer.mozilla.org/en-US/docs/Web/API/KeyframeEffect/KeyframeEffect) all accept an optional dictionary object of timing properties.

## Extensions to other interfaces

The Web Animations API adds some new features to [`document`](https://developer.mozilla.org/en-US/docs/Web/API/Document) and [`element`](https://developer.mozilla.org/en-US/docs/Web/API/Element).

### Extensions to the `Document` interface

- [`document.timeline`](https://developer.mozilla.org/en-US/docs/Web/API/Document/timeline)

  The `DocumentTimeline` object representing the default document timeline.

- [`document.getAnimations()`](https://developer.mozilla.org/en-US/docs/Web/API/Document/getAnimations)

  Returns an Array of [`Animation`](https://developer.mozilla.org/en-US/docs/Web/API/Animation) objects currently in effect on elements in the `document`.

-  Extensions to the `Element` interface 

- [`Element.animate()`](https://developer.mozilla.org/en-US/docs/Web/API/Element/animate)

  A shortcut method for creating and playing an animation on an element. It returns the created [`Animation`](https://developer.mozilla.org/en-US/docs/Web/API/Animation) object instance.

- [`Element.getAnimations()`](https://developer.mozilla.org/en-US/docs/Web/API/Element/getAnimations)

  Returns an Array of [`Animation`](https://developer.mozilla.org/en-US/docs/Web/API/Animation) objects currently affecting an element or which are scheduled to do so in future.

## Specifications

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article1-folder/t1.jpg)