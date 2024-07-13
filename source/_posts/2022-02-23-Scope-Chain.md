---
title: Scope Chain
date: 2022-02-23 20:20:23
toc: true
categories:
- javascript

---

Content: Scope and Scope Chain
<!--more-->

### Scope

1. Global Scope

2. Function Scope

*Note: There is no block-level scope in JavaScript*

```javascript
// The first type {}
{
  var abc = "123";
}
console.log(abc);

// The second type, if statement
if(true){
  var flag = "abc";
}
console.log(flag);

// The third type, for loop statement
for(var i = 0; i < arr.length; i++){
  
}
console.log(i);
```

The code examples demonstrate that in JavaScript, using `var` declares variables in the function scope or global scope, not in the block scope. This means that variables declared with `var` inside of blocks such as `{}`, `if`, or `for` are accessible outside of these blocks.

### Scope Chain

The inner function scope can access variables from its outer scope, but the outer scope cannot access variables defined in the inner scope.

```javascript
var a = 10;
function foo() {
    var b = 20;

    function fn() {
        var c = 30;
        console.log(a + b + c); // Accesses a and b from the outer scope and c from the inner scope.
    }

    function fn2() {
        var d = 50;
        console.log(a + b + d); // Accesses a and b from the outer scope and d from the inner scope.
    }

    fn();
    fn2();
}

foo();
```

The above example illustrates how the scope chain works in JavaScript. Functions `fn` and `fn2` are able to access the variables `a` and `b` from their parent function `foo`, as well as their own local variables `c` and `d`, respectively. This is because JavaScript scopes are lexically or statically defined by their position within the source code. When a variable is used, JavaScript looks up the scope chain until it finds the variable or reaches the global scope.

This is a fundamental concept in JavaScript known as lexical scoping, where the accessibility of variables is determined by the position of variables within the nested functions. The scope chain is created at the function's creation time, and it is the chain of function's scopes, which is used to resolve the values of variable names in JavaScript.