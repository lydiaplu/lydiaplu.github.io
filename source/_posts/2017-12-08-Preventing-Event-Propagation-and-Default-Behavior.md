---
title: Preventing Event Propagation and Default Behavior
date: 2017-12-08 21:30:50
toc: true
categories:
- javascript

---

Content: How to prevent event bubbling and default events, and precautions for using return false.
<!--more-->

### JS Event Binding Methods

1. Inline binding
2. Direct DOM element binding: `btn.onclick`
3. Using `addEventListener` / `attachEvent`

```javascript
// Inline binding
<div onclick="fn1();" id="div1">Click me</div>

// Direct DOM element binding
var div1 = document.getElementById('div1');
div1.onclick = function(){
    console.log(1);
};
 
// Using addEventListener / attachEvent
div1.addEventListener('click',function(){
    console.log(11);
},false);
```



### Preventing Bubbling: 

`event.stopPropagation();`

`event.cancelBubble = true;`

```javascript
// Prevent event bubbling
var div2 = document.getElementById("div2");
div2.onclick = function (event) {
    // Check event compatibility
    event = event || window.event;
    // Use stopPropagation if compatible, otherwise use cancelBubble
    if (event.stopPropagation) {
        event.stopPropagation();
    } else {
        event.cancelBubble = true;
    }
};
```



### Preventing Default Events:

`event.preventDefault();`

`event.returnValue = false;`

```javascript
// Prevent default behavior
var a = document.getElementById("jump");
a.onclick = function (event) {
    // Check event compatibility
    event = event || window.event;
    // Use preventDefault if compatible, otherwise use returnValue
    if (event.preventDefault) {
        event.preventDefault();
    } else {
        event.returnValue = false;
    }
};
```



### Notes on `return false`:

1. It can only prevent the default behavior when binding events directly to a DOM element;
2. It cannot prevent the default behavior when using `addEventListener` for event binding;
3. `return false` cannot stop event propagation in vanilla JS;
4. In jQuery, it can both stop propagation and prevent default behavior;

```javascript
// Issues with return false
// 1. Can only prevent default behavior in event bindings like onclick
var a = document.getElementById("jump");
a.onclick = function () {
    return false;
};

// 2. Cannot prevent default behavior in event bindings using addEventListener
var a = document.getElementById("jump");
a.addEventListener("click", function () {
    return false;
});
```

Additional Points:

- Inline event handlers like `onclick` attribute in HTML should be avoided where possible in favor of unobtrusive JavaScript techniques.
- When preventing default behavior, it's a good practice to do so only if necessary, as it can prevent other event listeners from executing properly if not handled carefully.
- When using `addEventListener`, if you want to prevent both default behavior and event bubbling, you need to call both `event.preventDefault()` and `event.stopPropagation()` within the event handler function.
- The use of `event.returnValue` and `event.cancelBubble` is considered old-fashioned and should be replaced with `event.preventDefault()` and `event.stopPropagation()` respectively, which are standardized across modern browsers.