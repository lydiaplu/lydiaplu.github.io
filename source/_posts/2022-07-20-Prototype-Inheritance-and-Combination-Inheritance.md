---
title: Prototype Inheritance and Combination Inheritance
date: 2022-07-20 13:32:10
toc: true
categories:
- javascript

---

**Content:** Prototype inheritance, constructor borrowing inheritance, introduction to strict mode, using call and apply, combination inheritance.

### Prototype Inheritance

Inheritance, in essence, is about code reuse.

Disadvantages:

1. There's no way to assign values to inherited properties.
2. Inherited reference type data is shared among all instances.

```javascript
// Define the Animal constructor
function Animal(name, voice) {
    this.name = name;
    this.voice = voice;
}

Animal.prototype.cry = function () {
    console.log(this.name + this.voice);
}

// Define the Cat constructor
function Cat(color) {
    this.color = color;
}

Cat.prototype = new Animal("tom","miaomiao");
Cat.prototype.tree = function () {
    console.log(this.name + "爬树");
}

var cat1 = new Cat("blue");
var cat2 = new Cat("orange");

console.log(cat1.name);
cat1.cry();
cat1.tree();
```

Demonstrating the disadvantages of prototype inheritance:

```javascript
function Person(name, favour) {
    this.name = name;
    this.favour = favour;
}

function Student(score) {
    this.score = score;
}

Student.prototype = new Person("xiaoming", ["coding", "dancing"]);

var stu1 = new Student(90);
stu1.favour.push("swimming");
var stu2 = new Student(98);
console.log(stu2.favour);

// 1. There's no way to assign values to inherited properties; they are added directly to the object.
stu1.name = "xiaohong";
console.dir(stu1);
// Student
//  name: "xiaohong"
//  score: 90
//  __proto__: Person
//      favour: Array[3]
//      name: "xiaoming"
//      __proto__: Object

// 2. Inherited reference type data is shared among all instances.
```

To address these issues, we can use constructor borrowing inheritance.

### Constructor Borrowing Inheritance

Disadvantage: Constructor borrowing inheritance cannot inherit members from the parent constructor's prototype.

```javascript
function Person(name, favour) {
    this.name = name;
    this.favour = favour;
}

Person.prototype.showName = function () {
    console.log(this.name);
}

function Student(name, favour, score) {
    Person.apply(this, [name, favour]);
    this.score = score;
}

var stu1 = new Student("小明", ["coding"], 96);
stu1.favour.push('swimming');
var stu2 = new Student("小红", ["dancing"], 98);

stu1.showName(); // Throws an error
```

### Strict Mode

In non-strict mode, the `this` keyword in regular functions refers to the `window` object. In strict mode, the `this` keyword in regular functions is `undefined`.

*Strict mode is enabled by writing `"use strict"` within a function.*

```javascript
// Non-strict mode
function foo() {
    console.log(this); // Outputs the window object
}

// Strict mode
function foo() {
    "use strict";
    console.log(this); // Outputs undefined
}
```

### Call and Apply

- Can be used to invoke functions.
- Can change the `this` context within the function.
- Can convert array-like objects.
- Can borrow methods from other objects.
- If there's a first argument, it must be of reference type.

```javascript
function foo(a, b) {
    console.log(a + b);
}
foo(1, 2);
foo.call(null, 12, 13);
foo.apply(null, [14, 15]);
```

Changing `this` context using `call` and `apply`:

```javascript
// Changing the 'this' context within a regular function
var a = 1;
var b = 2;

function sum(c) {
    console.log(this.a + this.b + c);
}

var obj = {
    a: 11,
    b: 12
}

// Outputs 24 because 'a' and 'b' are taken from 'obj'
sum.apply(obj, [1]);
```

Converting array-like objects:

```javascript
// 1. Using 'slice' and 'call'
var arr1 = [].slice.call(obj, 0);

// 2. Using 'push' and 'apply'
var arr2 = [];
[].push.apply(arr2, obj);
```

Borrowing methods from other objects:

```javascript
var arr = [12321, 234, 99999999, 4454, 12, 454545, 343, 34, 342];
var max = Math.max.apply(null, arr);
console.log(max);
```

### Bind (ES5 Feature, Function Currying)

The first argument must be of reference type.

`bind` changes the `this` context within a function but doesn't invoke it. It returns a new function with the specified `this` context.

```javascript
function foo(a, b) {
  console.log(a + b);
}

var fn = foo.bind({info: "hello"}, 12, 13);
```

Changing the `this` context within a timer function:

```javascript
var inner = function () {
  console.log(this);
}

var newInner = inner.bind({info: "hello"});
setTimeout(newInner, 1000);
```

### Combination Inheritance

Combination inheritance combines prototype inheritance and constructor borrowing inheritance.

```javascript
// Define a Person
function Person(name, favour) {
    this.name = name;
    this.favour = favour;
}
Person.prototype.showFavour = function () {
    console.log(this.favour);
}
Person.prototype.flag = 1;

// Define a Teacher
function Teacher(name, favour, level) {
    Person.call(this, name, favour);
    this.level = level;
}
Teacher.prototype = new Person();

var tea1 = new Teacher("小明", ["coding"], "T5");
var tea2 = new Teacher("小红", ["swimming"], "T3");
tea1.favour.push("singing");
tea1.showFavour();
tea2.showFavour();

tea1.flag = 2;
console.log(tea1.flag); // Outputs 2
console.log(tea2.flag); // Outputs 1
```