---
title: Usage of JSON
date: 2017-01-20 09:03:20
toc: true
categories:
- ajax

---

**Contents: Introduction to XML, Parsing and Usage of JSON, Differences Between XML and JSON**
<!--more-->

#### 1. XML

XML, or Extensible Markup Language, is a markup language in which tags are user-defined, such as `<person></person>`.

Specifications:

1. The first line must be a document declaration.
2. There must be a root element.
3. No spaces, numbers, or dots are allowed at the beginning of tag names, and it is case-sensitive.
4. Nesting cannot cross boundaries.
5. Attribute values must be enclosed in double quotes (browsers automatically correct to double quotes).
6. Special symbols must be represented using entities.
7. Comments are similar to HTML.

Although XML can be used to describe and transmit complex data, its parsing is complex, and the file size tends to be large. Therefore, it is rarely used in practical development.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<root>
    <arrayList>
        <array>
            <src>images/banner.jpg</src>
            <newPrice>12.00</newPrice>
            <oldPrice>30.00</oldPrice>
        </array>
        <array>
            <src>images/banner.jpg</src>
            <newPrice>12.00</newPrice>
            <oldPrice>30.00</oldPrice>
        </array>
    </arrayList>
</root>
```

```php
<?php 
    header('Content-Type:text/xml;charset=utf-8');
    /*When transmitting data in XML format, the response content format must be text/xml.*/

    /*Retrieve the content of the file using file_get_contents*/
    $xml = file_get_contents('01.xml');

    /*Output XML content*/
    echo $xml;
?>
```

```javascript
var xhr = new XMLHttpRequest;
xhr.open('get','01.php');
xhr.send(null);
xhr.onreadystatechange = function(){
    if(xhr.status == 200 && xhr.readyState == 4){
        /*Retrieve XML format content; it returns a DOM object, similar to document*/
        var xml = xhr.responseXML;
        /*XML data can be obtained using selectors*/
        console.log(xml.querySelectorAll('array')[0].querySelector('src').innerHTML);
    }
}
```

**Differences Between XML and HTML**

1. XML is an extensible markup language, while HTML is a hypertext markup language.
2. XML tags are user-defined, while HTML tags follow W3C specifications and must adhere to those standards.
3. XML is primarily used for software configuration files and data transmission, often requiring custom parsing.
4. HTML is used for displaying web content and is parsed by web browsers.

#### 2. JSON

JSON, which stands for JavaScript Object Notation, is another lightweight text-based data interchange format that is language-independent.

When interacting between clients and servers, minimizing the number of interactions for performance reasons is important, and caching is often used to reduce data transfer.

1. Data is stored in name/value pairs.
2. Data is separated by commas (the last key/value pair must not have a trailing comma).
3. Objects are enclosed in curly braces, and arrays are enclosed in square brackets.
4. Double quotes are used for property names and string values.

```JSON
[
  {"src":"images/detail01.jpg","oldPrice":"10.12","newPrice":"130.00"},
  {"src":"images/detail02.jpg","oldPrice":"1.00","newPrice":"11.00"},
  {"src":"images/detail03.jpg","oldPrice":"100.00","newPrice":"1000.00"}
]
```

JSON data is transmitted as strings in different programming languages, each with its own parsing methods. The data needs to be parsed to be accessed.

**2.1 PHP Parsing Methods**  
json_encode() and json_decode().

```PHP
<?php 
    header('Content-Type:text/html;charset=utf-8');
    /*When transmitting data in JSON format, the response content format should be application/json.*/
    /*It's a good practice to set the response content type, although it's not mandatory.*/

    /*Retrieve the content of the file using file_get_contents*/
    $json = file_get_contents('01.json');

    /*Output JSON content*/
    echo $json;
    echo '<br><br>';

    $array = array(
        array('src'=>'images/detail01.jpg','newPrice'=>'12.00','oldPrice'=>'455.00'),
        array('src'=>'images/detail02.jpg','newPrice'=>'65.00','oldPrice'=>'878.00'),
        array( 'src'=>'images/detail01.jpg','newPrice'=>'100.00','oldPrice'=>'1000.00')
    );

    /*Convert a PHP array to a JSON string*/
    $json_array = json_encode($array);
    echo $json_array;
    echo '<br><br>';

    /*Convert a JSON string to a PHP array*/
    $array_json = json_decode($json_array);
    echo $array_json;
    echo '<br><br>';
?>
```

**2.2 JavaScript Parsing Methods**  
Converting JSON objects:

| Method            | Description                                                  |
| ----------------- | ------------------------------------------------------------ |
| eval();           | Converts a string to JSON (provided by browsers).            |
| JSON.parse();     | Converts a string to JSON (JavaScript API with some compatibility issues). |
| JSON.stringify(); | Converts JSON to a string.                                   |



In summary, JSON is lightweight, easy to parse, and efficient, making it the preferred choice in practical development.

```javascript
    var xhr = new XMLHttpRequest;
    xhr.open('get','01.php');
    xhr.send(null);
    xhr.onreadystatechange = function(){
        if(xhr.status == 200 && xhr.readyState == 4){
            /*Retrieve the content as a string*/
            var text = xhr.responseText;
            
            /*Convert the string to a JSON object*/
            var json_obj = JSON.parse(text);
            console.log(json_obj);
    
            /*You can also convert JSON objects to strings*/
            var json_str = JSON.stringify(json_obj);
            console.log(json_str);
        }
    }
```