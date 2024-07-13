---
title: In-Depth Explanation of Recursion
date: 2022-05-26 18:10:23
toc: false
categories:
- javascript

---

**Content:** In-depth explanation of recursion
<!--more-->

### In-Depth Explanation of Recursion

```javascript
// Recursion: Factorial
function factorial(n) {
    if (n == 1) {
        console.log('Recursion ends at ' + n);
        return 1;
    }
    else {
        console.log('Before recursion ' + n);
        var result = n * factorial(n - 1);
        console.log('After recursion ' + n);
        return result;
    }
}
factorial(5);
```

The output will be:

```javascript
// Before recursion 5
// Before recursion 4
// Before recursion 3
// Before recursion 2
// Recursion ends at 1
// After recursion 2
// After recursion 3
// After recursion 4
// After recursion 5
```

Explanation:

![Analysis of Recursion](/images/9-4/Analysis-of-Recursion.png)

Practical Example of Recursion:

**Getting All Child Elements**

```javascript
// Application of Recursion
// Getting all child elements
function getAllChildNodes(node, arr) {
    for (var i = 0; i < node.childNodes.length; i++) {
        var subNode = node.childNodes[i];
        // If it's an element node, add it to the array
        if (subNode.nodeType == 1) {
            arr.push(subNode);
            getAllChildNodes(subNode, arr);
        }
    }
}
```