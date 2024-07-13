---
title: Event Delegation and Custom Events
date: 2022-02-18 20:30:52
toc: true
categories:
- javascript

---

**Content:** Event delegation, custom events
<!--more-->

### Event Delegation

When you need to add an event to all child elements, it's more efficient to use event delegation.

1. In JavaScript, you can use `event.target`.
2. In jQuery, you can use the `on` method to bind events.

```javascript
// Traditional way of binding events
var ul = document.getElementById("target");
var lis = ul.getElementsByTagName("li");
for (var i = 0; i < lis.length; i++) {
    lis[i].onclick = function () {
        console.log(this.innerHTML);
    }
}

// Delegating the events to the parent element
var ul = document.getElementById("target");
ul.onclick = function (event) {
    event = event || window.event;
    var target = event.target || event.srcElement;
    console.log(target.innerHTML);
}

// Binding events using jQuery
$("#target").on("click", "li", function () {
    console.log($(this).html());
});
```

### Custom Events

**1. Binding Custom Events in jQuery**

- Use the `on` method to bind custom events.
- Use the `trigger("event name")` method to trigger custom events.

```javascript
// Binding a custom event
$("#btn").on("abc", function () {
    console.log(123);
});

// Binding another custom event with the same name
$("#btn").on("abc", function () {
    console.log(456);
});

// Triggering the custom event
$("#btnTrigger").on("click", function () {
    // Use the trigger method to trigger the "abc" event of the "btn" button
    $("#btn").trigger("abc");
});
```

**2. Implementing Custom Events in JavaScript**

- Add a `listener` property to the object element.
- Within the `listener` property, add an attribute with the custom event name.
- Store an array of event handling functions as the attribute value.

Here's the code:

```javascript
// Binding an event
function addEvent(obj, type, fn) {
    obj.listener = obj.listener || {};
    obj.listener[type] = obj.listener[type] || [];
    obj.listener[type].push(fn);
}

// Triggering an event
function triggerEvent(obj, type) {
    // Get the array of event functions corresponding to the "type"
    var arr = obj.listener[type];
    for (var i = 0; i < arr.length; i++) {
        arr[i]();
    }
}
```

Testing and using custom events:

```javascript
// Testing the use of custom events
// Get a DOM element
var dv = document.getElementById("div1");
// Add a custom event "abc"
addEvent(dv, "abc", function () {
    console.log(123);
});
// Add another custom event "abc"
addEvent(dv, "abc", function () {
    console.log(567);
});
// Add a custom event "hi"
addEvent(dv, "hi", function () {
    console.log("hi");
});

// Trigger a custom event
triggerEvent(dv,"abc");
```

After adding custom events, the format looks like this:

```javascript
// Format:
obj.listener.abc = [function(){console.log(123);},function(){console.log(567);}];
obj.listener.hi = [function(){console.log("hi");}];
```