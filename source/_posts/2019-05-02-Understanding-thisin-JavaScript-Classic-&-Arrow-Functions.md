---
title: Understanding "this" in JavaScript: Classic & Arrow Functions
date: 2019-05-02 20:21:08
toc: true
categories:
- javascript
---

**Content: A Comprehensive Dive into "this" in JavaScript**
<!--more-->

### Exploring "this" in Various Contexts

JavaScript's "this" keyword is famously context-sensitive and can refer to different objects depending on how a function is called. This article will clarify the behavior of "this" in various scenarios, including the nuances introduced by arrow functions.

#### 1. "this" in Constructors

When used inside constructors, "this" refers to the new instance that's being created.

```javascript
function Car(make, model) {
  this.make = make;
  this.model = model;
}

const myCar = new Car('Toyota', 'Corolla');
console.log(myCar.make); // Toyota
```

#### 2. "this" in Prototypes

In prototype methods, "this" points to the instance from which the method is called.

```javascript
Car.prototype.getMake = function() {
  return this.make;
};

console.log(myCar.getMake()); // Toyota
```

#### 3. "this" in Event Handlers

In event handlers, "this" usually refers to the element that received the event.

```javascript
document.getElementById('myBtn').addEventListener('click', function() {
  console.log(this.id); // myBtn
});
```

#### 4. "this" in Regular Functions

The value of "this" in functions depends on strict mode and how the function is called.

```javascript
function logThis() {
  console.log(this);
}

logThis(); // window in non-strict mode, undefined in strict mode
```

#### 5. "this" with "call" and "apply"

"this" can be explicitly set using "call" or "apply".

```javascript
function greet() {
  console.log(`Hello, ${this.name}`);
}

const person = { name: 'Alice' };
greet.call(person); // Hello, Alice
```

#### 6. "this" in Timer Functions

Within "setTimeout" and "setInterval", "this" refers to the global object.

```javascript
function logThis() {
  console.log(this);
}

setTimeout(logThis, 1000); // logs global object (window in browsers)
```

#### 7. "this" in Object Methods

"This" inside a method refers to the object calling the method.

```javascript
const person = {
  name: 'Alice',
  greet: function() {
    console.log(`Hi, I'm ${this.name}`);
  }
};

person.greet(); // Hi, I'm Alice
```

#### 8. "this" in Arrow Functions

Arrow functions do not have their own "this" context; they inherit "this" from the parent scope at the time they are defined.

```javascript
const person = {
  name: 'Alice',
  greet: () => {
    console.log(`Hi, I'm ${this.name}`);
  }
};

person.greet(); // Hi, I'm , because `this` is not the person object but the global context
```

This behavior is particularly useful when dealing with callbacks.

```javascript
function Timer() {
  this.seconds = 0;
  setInterval(() => {
    this.seconds++;
    console.log(this.seconds);
  }, 1000);
}

new Timer();
```

Here, the arrow function inherits the "this" from the `Timer` instance, maintaining the context even inside the asynchronous callback.

**Additional Scenario: "this" in Array Functions**

If you access and invoke a function from an array using an index, "this" behaves differently with classic and arrow functions:

```javascript
var arr = [function() { console.log(this); }, () => { console.log(this); }];
arr[0](); // Array itself
arr[1](); // Global object or the scope in which the array is defined
```

### Conclusion

Understanding "this" in JavaScript can be challenging, especially for beginners. However, with the use of various examples as provided above, the concept becomes more approachable. Remember that "this" can behave differently in arrow functions, and always be mindful of the scope in which your functions are defined and called.