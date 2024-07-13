---
title: Arrays and Array-like Objects
date: 2018-02-24 10:20:11
toc: false
categories:
- javascript

---

**Content: Introduction to Arrays and Array-like Objects**
<!--more-->

### Arrays and Array-like Objects

The "delete" keyword is used to delete properties from objects.

*Note: In the global scope, "delete" cannot delete variables declared with "var." However, variables declared without "var" in the global scope can be deleted.*

```javascript
// Array
var arr = [1,5,2,8,0,3];
delete arr[0];

// Object
var obj = {
  info: "abc",
  username: "John"
}
delete obj.info;

// Cannot delete variables declared with "var" in the global scope
var flag = 123;
delete flag;

// Variables declared without "var" in the global scope can be deleted
flag1 = 567;
delete flag1;
```

**Array-like Object Format**

```javascript
// Array-like object format
var obj = {
  0: "abc",
  1: "def",
  2: "ghi",
  length: 3
}
```

**Converting Array-like Objects to Arrays**

```javascript
// 1. Using "slice" and "call"
var arr1 = [].slice.call(obj, 0);

// 2. Using "push" and "apply"
var arr2 = [];
[].push.apply(arr2, obj);
```

```javascript
// Array-like object format
var obj = {
    0: "abc",
    1: "def",
    2: "ghi",
    length: 3
};

// Converting array-like object to an array
// 1. Using "slice" and "call"
var arr1 = [].slice.call(obj, 0);
console.log(arr1);

// 2. Using "push" and "apply"
var arr2 = [];
[].push.apply(arr2, obj);
// The following two methods are also equivalent to the one above
Array.prototype.push.apply(arr2, obj);
new Array().push.apply(arr2, obj);
console.log(arr2);
```