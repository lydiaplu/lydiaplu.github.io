---
title: Function Properties
date: 2022-02-21 12:15:32
toc: false
categories:
- javascript

---

Content: Properties of a function
<!--more-->

### Function Properties

| Function Property | Purpose                        |
| ----------------- | ------------------------------ |
| arguments         | Collection of actual arguments |
| length            | Number of formal parameters    |
| caller            | The caller of the function     |
| name              | The name of the function       |

Detailed Explanation:

1. The `arguments` object is an array-like object that can capture passed arguments even if no formal parameters are defined;
2. The use of `arguments` is discouraged as it can be resource-intensive;
3. `arguments.callee` refers to the function itself, but its use is also discouraged;

```javascript
function foo(a, b) {
    // Collection of actual arguments
    console.dir(arguments);
    // Convert arguments to an array
    var arr = Array.prototype.slice.call(arguments, 0);
    console.log(arr);

    // The caller of the function
    console.log(foo.caller);

    // arguments.callee refers to the function itself
    console.log(arguments.callee);

    // Number of formal parameters
    console.log(foo.length);

    // The name of the function
    console.log(foo.name);
}

function fn() {
    foo(1, 2, 3);
}
fn();
```

Additional Context:

- The `arguments` object provides a way to use the actual parameters passed to a function, which is especially useful in functions that are meant to handle a variable number of arguments.
- The `length` property of a function is often used in the definition of currying and partial application functions, as it provides a reliable way to get the arity of the function - that is, how many arguments the function is designed to accept.
- The `caller` property, although not standard and not recommended for use in new code, can be useful for debugging purposes as it tells you which function called the current function.
- The `name` property is a string that contains the name of the function. Anonymous functions will have an empty string for the `name` property. This can be useful for debugging and function identification purposes.