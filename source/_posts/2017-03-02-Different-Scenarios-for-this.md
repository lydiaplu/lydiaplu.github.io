---
title: Different Scenarios for "this"
date: 2017-03-02 20:21:08
toc: true
categories:
- javascript

---

**Content: Introduction to Different Scenarios for "this"**
<!--more-->

### "this" in Different Scenarios

**1. "this" in Constructors**

In constructors, "this" refers to the instance object created by the constructor.

**2. "this" in Prototypes**

In prototype methods, "this" also points to the instance object created by the constructor.

**3. "this" in Event Handlers**

In event handlers, "this" refers to the object to which the event is bound.

**4. "this" in Regular Functions**

In non-strict mode, "this" refers to the global "window" object.

In strict mode, "this" is "undefined" inside regular functions.

**5. "this" in "call" and "apply"**

In functions called with "call" or "apply," "this" is the first argument passed to "call" or "apply," which should be an object.

**6. "this" in Timer Functions**

In timer functions, like "setTimeout" and "setInterval," "this" points to the "window" object.

**7. "this" in Object Methods**

In object methods, "this" refers to the object that calls the method (i.e., the object before the dot).

**Additional Note:**

If you have an array with functions and you access and invoke a function from the array using an index, like `arr[0]()`, the "this" inside the function will be the array itself:

```javascript
var arr = [function(){console.log(this);},function(){console.log(this,123);}];
arr[0]();
```