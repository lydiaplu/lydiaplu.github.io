---
title: AJAX Programming
date: 2017-01-10 20:10:28
toc: true
categories:
- AJAX

---

**Content**: Introduction to AJAX requests and responses, XMLHttpRequest, AJAX usage in JavaScript, and AJAX usage in jQuery.
<!--more-->

## AJAX Programming

> AJAX stands for Asynchronous JavaScript And XML. It's not a new programming language but a combination of existing technologies. At its core, AJAX is about making asynchronous requests to a server using HTTP.

#### 1. Asynchronous

Asynchronous means that a program can continue running without waiting for a specific task to complete. In programming, it implies that the execution sequence of a program doesn't depend on the order of code writing. The advantages of asynchronous programming include improved overall efficiency.

XMLHttpRequest is used to handle AJAX requests asynchronously.

#### 2. XMLHttpRequest

XMLHttpRequest is a built-in browser object used for background communication (data exchange) with a server. It allows partial updates to a web page without refreshing the entire page.

```javascript
/* Built-in HTTP request object in JavaScript */

/* 1. How to use this built-in object */
var xhr = new XMLHttpRequest();

/* 2. How to compose a request */
/* Request Line */
xhr.open('post', '01.php');

/* Request Header */
// No need to set for GET requests
// For POST requests, set Content-Type: application/x-www-form-urlencoded
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');

/* Request Body */
/* 3. Sending the request */
xhr.send("name=xjj&age=10");
```

##### 2.1 Request

Components of an HTTP request and their correspondence with XMLHttpRequest methods:

1. Request Line

```javascript
xhr.open('post', '01.php');
```

2. Request Header

```javascript
xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
// For GET requests, this step may be omitted
```

3. Request Body

```javascript
xhr.send("name=xjj&age=10");
// For GET requests, you can send null
```

**Pay attention to the order of these steps.**

##### 2.2 Response

Components of an HTTP response and their correspondence with XMLHttpRequest methods or properties:

To handle responses, we need to check and confirm the response status from the server. It's important to monitor the server's response status, which may take time due to factors like slow internet speed.

**onreadystatechange** is an event in JavaScript used to listen to the XMLHttpRequest's status.

```javascript
xhr.onreadystatechange = function () {
    // xhr.readyState == 4 means the server response is complete
    // xhr.status == 200 means the response was successful
    if (xhr.readyState == 4 && xhr.status == 200) {
        console.log('OK');
        console.log(xhr.responseText);
        /* Render the content on the page */
        document.querySelector('#result').innerHTML = xhr.responseText;
    }
}
```

**readyState**:

```
0: Request not initialized (open has not been called yet).
1: Connection established (open has been called).
2: Request received (send has been called and headers received).
3: Processing request (responseText holds partial data).
4: Request finished and response is ready.
```

1. Get the status line (including status code & status message)

```javascript
xhr.status // Status code
```

```javascript
xhr.statusText // Status message (e.g., OK)
```

2. Get the response header

```javascript
xhr.getResponseHeader('Content-Type');
xhr.getAllResponseHeaders();
```

3. Get the response body

```javascript
xhr.responseText
xhr.responseXML
```

We need to check the MIME type in the response header to determine whether to use `request.responseText` or `request.responseXML`.

##### 2.3 API Details

```javascript
xhr.open() // Initiates the request, can be GET or POST
xhr.setRequestHeader() // Sets request headers
xhr.send() // Sends the request body; for GET requests, you can send null
xhr.onreadystatechange = function () {} // Listens to response status changes
xhr.status // Represents the response code, e.g., 200
xhr.statusText // Represents the response message, e.g., OK
xhr.getAllResponseHeaders() // Gets all response headers
xhr.getResponseHeader('key') // Gets a specific header
xhr.responseText and xhr.responseXML // Represent the response body
```

#### 3. Compatibility

Regarding compatibility with Internet Explorer (IE), it's important to understand but may not be necessary for modern web development. For older IE versions, ActiveXObject is required with specific identifiers.

```javascript
function XHR() {
    var xhr;
    try {
        xhr = new XMLHttpRequest();
    }
    catch(e) {
        var IEXHRVers = ["Msxml3.XMLHTTP", "Msxml2.XMLHTTP", "Microsoft.XMLHTTP"];

        for (var i = 0; i < IEXHRVers.length; i++) {
            try {
                xhr = new ActiveXObject(IEXHRVers[i]);
            }
            catch(e) {
                continue;
            }
        }
    }
    return xhr;
}
```

#### 4. Encapsulation of AJAX Utility Functions

```javascript
/**
 * Customized AJAX function
 *
 * @param {Object} options - Configuration options for the AJAX request.
 */
window.$ = {};

$.ajax = function(options) {
    if (!options || typeof options !== 'object') {
        return false;
    }

    var type = options.type || 'get';
    var url = options.url || location.pathname;
    var async = (options.async === false) ? false : true;
    var contentType = options.contentType || "text/html";
    var data = options.data || {};
    var dataStr = '';

    for (var key in data) {
        dataStr += key + '=' + data[key] + '&';
    }

    dataStr = dataStr && dataStr.slice(0, -1);

    var xhr = new XMLHttpRequest();

    xhr.open(type, (type == 'get') ? (url + '?' + dataStr) : url, async);

    if (type == 'post') {
        xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
    }

    xhr.send((type == 'get') ? null : dataStr);

    xhr.onreadystatechange = function() {
        if (xhr.readyState == 4 && xhr.status