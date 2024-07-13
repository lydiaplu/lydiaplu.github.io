---
title: Prototype Chain
date: 2022-08-02 09:03:32
toc: true
categories:
- javascript

---

Content: Introduction to Prototypes, Introduction to Prototype Chains, Relationship between "Constructor", "Instantiated Object", and "Prototype"
<!--more-->

### The Relationship Between Constructor, Instantiated Objects, and Prototype

1. Constructors have a prototype property, which is also an object;

2. The prototype object contains a property named constructor, which points back to the constructor that created it;

3. Instantiated objects have a property __proto__ (not standard and should not be used in coding) that is used internally by browsers and points to the prototype object.

**The relationship between __proto__, prototype, and constructor**

```javascript
// The relationship between __proto__, prototype, and constructor
c1.__proto__ === Car.prototype
c1.__proto__.constructor === Car
Car.prototype.constructor === Car
```

Here is the code: 

```javascript
function Car(brand, color) {
    this.brand = brand;
    this.color = color;
}
Car.prototype.showInfo = function () {
    console.log(this.brand + ' color: ' + this.color);
};

var c1 = new Car("Audi", "black");
var c2 = new Car("Mercedes", "white");

// Verifying the relationship between __proto__, prototype, and constructor
console.log(c1.__proto__ === Car.prototype);
console.log(c1.__proto__.constructor === Car);
console.log(Car.prototype.constructor === Car);

// The prototype chain direction
// c1 -> Car.prototype -> Object.prototype -> null
```

![Constructor, Instance Object, Prototype Relationship](/images/9-2/constructor-instance-prototype-relationship.png)



### Prototypes

All functions have a prototype property.

The value of this property is an object (which is an instance of Object).

**Purpose:**

1. To enable data sharing (among instantiated objects)
2. To implement inheritance

**__ proto __**

The instance objects created by constructors have a property ```__proto__```.

Its purpose is to link the nodes in the prototype chain.

- __ proto __ is in the instance objects
- prototype is in the constructors

This property is not standard and should not be used in programming; it's used internally by browsers and may differ across them.

```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
}
Person.prototype.showName = function () {
    console.log(this.name);
};
Person.prototype.showAge = function () {
    console.log(this.age);
};

var p1 = new Person("Tom", 12);
var p2 = new Person("Jerry", 13);
```



### Prototype Chain

The chain-like structure formed between instance objects and prototype objects, which is linked through __proto__.

The structure of the prototype chain can be modified by resetting the prototype object.

```javascript
function Foo1(info) {
    this.info = info;
}

Foo2.prototype = new Foo1('Tom');
Foo2.prototype.constructor = Foo1;
function Foo2(info) {
    this.info = info;
}

Foo3.prototype = new Foo2("Jerry");
Foo3.prototype.constructor = Foo2;
function Foo3(info) {
    this.info = info;
}

var f = new Foo3("Spike");
console.dir(f);

// Prototype Chain
// f -> new Foo2('Jerry') -> new Foo1('Tom') -> Foo1.prototype -> Object.prototype -> null
```

**Another way to write a prototype chain**

```javascript
function Student(name, age, score) {
    this.name = name;
    this.age = age;
    this.score = score;
}

Student.prototype = {
    constructor: Student,
    showName: function () {
        console.log(this.name);
    },
    showAge: function () {
        console.log(this.age);
    },
    showScore: function () {
        console.log(this.score);
    }
}
```



### Property Lookup

1. When accessing a member of an object, the search starts within the object itself.
2. If the object does not have the property, the search moves on to the object’s prototype.
3. If the prototype does not have the property, the search moves on to the prototype’s prototype.
4. This continues until the prototype of Object, which is null, is reached.

Regarding the generation of the image that illustrates the relationship between constructor, instance, and prototype, that is something that I can assist with. Let's define what elements and relationships you'd like to visualize, and I can create an image accordingly. Please provide the details you'd like to include in the image.