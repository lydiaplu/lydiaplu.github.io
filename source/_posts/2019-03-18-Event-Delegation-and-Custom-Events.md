---
title: Event Delegation and Custom Events
date: 2019-03-18 20:30:52
toc: true
categories:
- javascript

---

Content: Event Delegation, Custom Events
<!--more-->

### Event Delegation

Instead of adding an event listener to each child element individually, which can be inefficient, event delegation allows us to bind the event to a parent element.

1. In vanilla JS, you can use the `event.target` method;
2. In jQuery, you can use `on` to bind events;

```javascript
// Previous way of binding events
var ul = document.getElementById("target");
var lis = ul.getElementsByTagName("li");
for (var i = 0; i < lis.length; i++) {
    lis[i].onclick = function () {
        console.log(this.innerHTML);
    }
}

// Delegating the child element's event to the parent element
var ul = document.getElementById("target");
ul.onclick = function (event) {
    event = event || window.event;
    var target = event.target || event.srcElement;
    console.log(target.innerHTML);
}

// jQuery way of binding events
$("#target").on("click", "li", function () {
    console.log($(this).html());
});
```

Event delegation is a powerful technique that takes advantage of the fact that events bubble up through the DOM tree. By binding a single event listener to a parent element, you can handle events from all of its descendants that match a selector.

### Custom Events

**1. Binding custom events with jQuery**

- Bind a custom event using the `on` method;
- Trigger a custom event using the `trigger("event name")` method;

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
    // Use the trigger method to trigger the abc event on the btn element
    $("#btn").trigger("abc");
});
```

**2. Implementing custom events in vanilla JS**

- Add a listener property to the target object element;
- In the listener property, add attributes named after the custom events;
- These attributes hold an array of event handler functions;

Here is the code:

```javascript
// Binding the event
function addEvent(obj, type, fn) {
    obj.listener = obj.listener || {};
    obj.listener[type] = obj.listener[type] || [];
    obj.listener[type].push(fn);
}

// Triggering the event
function triggerEvent(obj, type) {
    // Retrieve the array of event functions for obj
    var arr = obj.listener[type];
    for (var i = 0; i < arr.length; i++) {
        arr[i]();
    }
}
```

Testing and using the custom event:

```javascript
// Test the use of custom events
// Get a DOM element
var dv = document.getElementById("div1");
// Add a custom event named abc
addEvent(dv, "abc", function () {
    console.log(123);
});
// Add another custom event named abc
addEvent(dv, "abc", function () {
    console.log(567);
});
// Add a custom event named hi
addEvent(dv, "hi", function () {
    console.log("hi");
});

// Trigger the custom event
triggerEvent(dv,"abc");
```

After adding custom events, the format is as follows:

```javascript
// The format is as follows
obj.listener.abc = [function(){console.log(123);},function(){console.log(567);}];
obj.listener.hi = [function(){console.log("hi");}];
```

Custom events in JavaScript provide a way to communicate across different parts of an application without coupling the event sender to the receiver, allowing for more modular and reusable code.