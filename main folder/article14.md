# Notifications API

> **Note:** This feature is available in [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API).

> **Secure context**
> This feature is available only in [secure contexts](https://developer.mozilla.org/en-US/docs/Web/Security/Secure_Contexts) (HTTPS), in some or all [supporting browsers](https://developer.mozilla.org/en-US/docs/Web/API/Notifications_API#Browser_compatibility).

The Notifications API allows web pages to control the display of system notifications to the end user. These are outside the  top-level browsing context viewport, so therefore can be displayed even  when the user has switched tabs or moved to a different app. The API is  designed to be compatible with existing notification systems, across  different platforms.

## Concepts and usage

On supported platforms, showing a system notification generally  involves two things. First, the user needs to grant the current origin  permission to display system notifications, which is generally done when the app or site initialises, using the [`Notification.requestPermission()`](https://developer.mozilla.org/en-US/docs/Web/API/Notification/requestPermission) method. This should be done in response to a user gesture, such as clicking a button, for example:

```js
btn.addEventListener('click', function() {
  let promise = Notification.requestPermission();
  // wait for permission
})
```

This is not only best practice — you should not be spamming users  with notifications they didn't agree to — but going forward browsers  will explicitly disallow notifications not triggered in response to a  user gesture. Firefox is already doing this from version 72, for  example.

This will spawn a request dialog, along the following lines:

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article14-folder/Screen_Shot_2019-12-11_at_9.59.14_AM.png)

From here the user can choose to allow notifications from this  origin, or block them. Once a choice has been made, the setting will  generally persist for the current session.

> **Note**: As of Firefox 44, the permissions for Notifications and [Push](https://developer.mozilla.org/en-US/docs/Web/API/Push_API) have been merged. If permission is granted for notifications, push will also be enabled.

Next, a new notification is created using the [`Notification()`](https://developer.mozilla.org/en-US/docs/Web/API/Notification/Notification) constructor. This must be passed a title argument, and can optionally  be passed an options object to specify options, such as text direction,  body text, icon to display, notification sound to play, and more.

In addition, the Notifications API spec specifies a number of additions to the [ServiceWorker API](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorker_API), to allow service workers to fire notifications.

> **Note**: To find out more about using notifications in your own app, read [Using the Notifications API](https://developer.mozilla.org/en-US/docs/Web/API/Notifications_API/Using_the_Notifications_API).

## Notifications interfaces

- [`Notification`](https://developer.mozilla.org/en-US/docs/Web/API/Notification)

  Defines a notification object.

### Service worker additions

- [`ServiceWorkerRegistration`](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerRegistration)

  Includes the [`ServiceWorkerRegistration.showNotification()`](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerRegistration/showNotification) and [`ServiceWorkerRegistration.getNotifications()`](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerRegistration/getNotifications) method, for controlling the display of notifications.

- [`ServiceWorkerGlobalScope`](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerGlobalScope)

  Includes the [`ServiceWorkerGlobalScope.onnotificationclick`](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerGlobalScope/onnotificationclick) handler, for firing custom functions when a notification is clicked.

- [`NotificationEvent`](https://developer.mozilla.org/en-US/docs/Web/API/NotificationEvent)

  A specific type of event object, based on [`ExtendableEvent`](https://developer.mozilla.org/en-US/docs/Web/API/ExtendableEvent), which represents a notification that has fired.

## Specifications

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article14-folder/t1.jpg)

## Browser compatibility

![](https://github.com/ChickenKyiv/awesome-mozilla-web-articles/blob/master/main%20folder/images/article14-folder/t2.jpg)