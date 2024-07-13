---
title: Event Loop
date: 2019-02-19 09:23:50
toc: true
categories:
- javascript

---

Content: Event Loop, What is JSON?
<!--more-->

### Event Loop

JavaScript runs in a single-threaded environment.

Executing tasks one after another can lead to issues, such as blocking subsequent execution when encountering a time-consuming task, resulting in lag. To address this, JavaScript implements an **event loop**.

**Event Queue:**

The queue holds tasks (essentially functions) such as:

1. Timer functions (like `setTimeout`, `setInterval`)
2. Event handlers (functions that respond to user interactions like clicks)
3. AJAX callback functions

**Conditions for tasks in the event queue to execute:**

1. The main thread is idle
2. The triggering conditions for the task are met:
   - For timer functions: The specified delay time has passed, though it's not guaranteed to be precise
   - For event handlers: The corresponding event has been fired
   - For AJAX callback functions: Triggered when receiving data from the server (when the `readyState` changes)

**The browser itself is multi-threaded (multi-process)**

1. Rendering of page tabs;
2. Network communication;
3. Parsing and running of JavaScript;


```javascript
// Timer function
setTimeout(function(){ 
    console.log('Executes after 2 seconds');
}, 2000);

// Event handler
var oDiv = document.getElementById('div');
oDiv.onclick = function(e){
    console.log('Click me!');
}

// AJAX callback function
xhr.onreadystatechange = function(){
    if(xhr.readyState == 4){
        if(xhr.status == 200){
            console.log(xhr.responseText);
        } 
    }
}
```

The event loop is a fundamental concept in JavaScript's concurrency model. It allows JavaScript to perform non-blocking operations, despite being single-threaded, by offloading operations that would block the thread to the environment's APIs and handling the completed operations once the main thread is available.

### What is JSON

JSON stands for JavaScript Object Notation.

JSON is a data format:

- Consists of key-value pairs;
- Keys must be enclosed in double quotes;
- Values can be strings, booleans, or numbers. Reference types can be arrays or objects;

```json
{
  "name": "zhangsan",
  "age": 20
}
```

JSON is a lightweight data-interchange format that is easy for humans to read and write, and easy for machines to parse and generate. It is based on a subset of JavaScript but is language-independent, with parsers available for many languages. JSON is ideal for sending data between a server and a web application.