---
title: Determining if a Property Exists
date: 2019-05-27 22:30:52
toc: true
categories:
- javascript

---

Content: Utilizing `in` and `hasOwnProperty()` for Property Checks
<!--more-->

### Property Existence Check in Objects

**`in`** and **`hasOwnProperty()`** are two ways to determine if a property exists within an object.

Usage:

```javascript
// Using 'in'
"propertyName" in obj

// Using hasOwnProperty()
obj.hasOwnProperty("propertyName")
```

**Differences between the two:**

`in` operator checks for property in both the instance object and the prototype object.

`hasOwnProperty()` only checks for properties on the instance object, meaning it can detect properties that have been added manually but not the built-in properties.

Example:

```javascript
// Define a constructor function
function Person(name, age) {
    this.name = name;
    this.age = age;
}
Person.prototype.greet = function () {
    console.log("Hello, my name is " + this.name);
};

// Instantiate an object
var person1 = new Person("John Doe", 30);

// Check using 'in'
console.log("name" in person1); // Prints true
console.log("greet" in person1); // Prints true

// Check using hasOwnProperty()
console.log(person1.hasOwnProperty("name")); // Prints true
console.log(person1.hasOwnProperty("greet")); // Prints false
```

To further understand the difference, let's look at an inherited property example:

```javascript
// Define another prototype method
Person.prototype.ageGroup = "Adult";

// Check inherited property
console.log("ageGroup" in person1); // Prints true
console.log(person1.hasOwnProperty("ageGroup")); // Prints false

// This shows 'in' finds inherited properties, whereas 'hasOwnProperty()' does not.
```

In practical use, `in` is helpful when you want to check if a property is available for use (either on the object itself or somewhere in its prototype chain), which is common when you want to avoid errors from calling undefined methods. On the other hand, `hasOwnProperty()` is useful when you need to ensure a property is explicitly defined on the object itself, often used when iterating over properties for the purpose of serialization or comparison without including inherited properties.

### Conclusion

Using `in` and `hasOwnProperty()` effectively can ensure that your JavaScript code respects the object's property structure and inheritance. While `in` can tell you if a method or property is accessible, `hasOwnProperty()` confirms that the property is a direct property of the object, which is critical for certain operations, particularly those involving object property enumeration or cloning.