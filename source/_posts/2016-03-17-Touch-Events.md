---
title: Touch Events
date: 2016-03-17 19:10:25
toc: true
categories:
- Mobile Web

---

**Content**: Touch events, solutions for handling click events.
<!--more-->

## Touch Events

**Note: You should use `addEventListener` to bind touch events, not `on`.**

```js
var box = document.querySelector(".box");

// Occurs when a finger touches the screen
// Use addEventListener to bind the event, not "on"
box.addEventListener("touchstart", function (event) {
  console.log("touchstart");
});

// Occurs as the finger moves across the screen
box.addEventListener("touchmove", function (event) {
  console.log("touchmove");
});

// Occurs when a finger leaves the screen
box.addEventListener("touchend", function (event) {
  console.log("touchend");
});
```

| Event Name  | Description                                        |
| ----------- | -------------------------------------------------- |
| touchstart  | Occurs when a finger touches the screen            |
| touchmove   | Occurs as a finger moves across the screen         |
| touchend    | Occurs when a finger leaves the screen             |
| touchcancel | Occurs when the system stops tracking touch events |

**Order of Touch Event Response**

1. touchstart
2. touchmove
3. touchend
4. onclick (with a 300ms delay)

### Touch Event Parameters

1. changedTouches: A collection of all changed touch points.
2. targetTouches: A collection of touch points on the target element.
3. touches: A collection of all touch points on the page.

*Note: In the touchend event, the event only records changedTouches.*

**Coordinates in the changedTouches Collection**

- client: Coordinates relative to the viewport.
- page: Coordinates relative to the page.
- screen: Coordinates relative to the screen (including the browser's toolbar).

### touchmove Event

The touchmove event is continuously triggered as the finger moves on the screen.

When building swipe or scroll functionalities, you can use `event.preventDefault()` to prevent the default behavior, such as page scrolling.

## Resolving Click Event Delay

1. Use the `tap` event.
2. Use the FastClick plugin.

### tap Event

**Definition of the `tap` Event**

```js
// A namespace for the tap event
window.customTap = {};

/**
 * Method for the tap event
 * @param dom Element to bind the tap event to
 * @param callback Function to execute on tap event
 */
customTap.tap = function (dom, callback) {
    // 1. No scrolling occurred
    // 2. Faster response than click, within 150ms

    if (!dom || typeof dom != 'object') return false;

    // Record whether scrolling occurred, initially set to false
    var isMove = false;
    // Record the start touch time
    var startTime = 0;

    dom.addEventListener("touchstart", function (e) {
        // Timestamp
        startTime = Date.now();
    });

    dom.addEventListener("touchmove", function (e) {
        isMove = true;
    });

    dom.addEventListener("touchend", function (e) {
        // Calculate the response time
        var time = Date.now() - startTime;

        // Determine if it's a tap event
        if (!isMove && time < 150) {
            // Execute the tap event
            callback && callback(e);
        }

        // Reset parameters
        isMove = false;
        startTime = 0;
    });
};
```

**Usage of the `tap` Event**

```js
window.onload = function () {
  var box = document.querySelector(".box");
  customTap.tap(box, function (e) {
    console.log("tap event triggered");
  });
}
```