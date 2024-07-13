---
title: Cross-Origin Solutions
date: 2016-06-30 21:53:43
toc: true
categories:
- ajax

---

**Content: Introduction to Cross-Origin Requests and Cross-Origin Solutions**
<!--more-->

What is Cross-Origin?

Cross-Origin refers to a situation where a web page at one domain tries to access resources from a different domain. This is restricted by browsers due to security concerns.

The key factors for determining Cross-Origin are differences in port, domain name, and protocol. If any of these factors are not the same, the request is considered Cross-Origin, and browsers impose security restrictions, preventing the access of resources from a different domain.

#### Cross-Origin with the Same Main Domain

To resolve Cross-Origin issues when the main domain is the same, you can set the `document.domain` property to the same value in both pages.

```javascript
<script>
    document.domain = "example.com";
</script>
```

#### JSONP for Cross-Origin Access

**First Method:** Use jQuery's AJAX with the `dataType: jsonp` property.

When `dataType: jsonp` is set, jQuery sends the request using JSONP.

```javascript
$.ajax({
    type: "get",
    url: "http://api.jisuapi.com/shouji/query",
    data: {
      appkey: "se3dr3sdx25721e5",
      shouji: telnumber
    },
    dataType: "jsonp",
    success: function (data) {
      span.html(data.result.province);
    }
})
```

To modify the default callback parameter name and the name of the callback function, use:

```javascript
jsonp: "cb", // Modify the callback parameter name (default is "callback")
jsonpCallback: "getInfo", // Modify the callback function name
```

**Second Method:** Simulate JSONP using low-level JavaScript to make a Cross-Origin request.

**JSONP Principle:**

JSONP sends a request by dynamically creating a `script` tag.

1. Create a `script` tag dynamically to send the request.
2. Pass a callback function name to the server, usually named "callback".
3. Define a global callback function on the client.
4. The server responds by calling the callback function and passing the response data as a parameter.

*Browsers have Cross-Origin restrictions on the XMLHttpRequest object but not on the `script` tag.*

```javascript
// Define a global callback function
function getInfo(data) {
    console.log(data);
}

window.onload = function () {
    var script = document.createElement("script");
    // Pass the callback function as a parameter
    script.src = "04-jsonpDemo.php?callback=getInfo";
    document.body.appendChild(script);
};
```

```php
<?php
    // Receive data using GET
    $callback = $_GET["callback"];
    $data = '{"username":"zhangsan"}';

    // Return the callback function call with data as a parameter
    echo $callback."(".$data.")";
?>
```

#### CORS (Cross-Origin Resource Sharing)

CORS stands for Cross-Origin Resource Sharing.

To enable CORS, set the response header "Access-Control-Allow-Origin" to specify which domains are allowed to access the resource.

```php
<?php
    header("Content-Type:text/json;charset=utf-8;");
    // Add domains that are allowed to access
    header("Access-Control-Allow-Origin: www.example1.com, www.example2.com");
    $data = $_GET["username"];
    echo $data;
?>
```

```javascript
var xhr = new XMLHttpRequest();
xhr.open("get", "http://127.0.0.1/01-cors.php?username=zhangsan");
xhr.send(null);
xhr.onreadystatechange = function () {
    if (xhr.readyState == 4 && xhr.status == 200) {
        var data = xhr.responseText;
        alert(data);
    }
};
```

#### Differences Between JSONP and CORS

| JSONP                   | CORS                            |
| ----------------------- | ------------------------------- |
| Supports only GET       | Supports both GET and POST      |
| Limited data size       | Can handle larger data          |
| Supports older browsers | Does not support older browsers |

#### Other Cross-Origin Solutions

1. Use a reverse proxy to solve Cross-Origin issues.
2. Use Flash plugins to handle Cross-Origin requests.