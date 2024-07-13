---
title: Media Queries
date: 2016-03-18 09:21:33
toc: true
categories:
- Mobile Web

---

**Content**: Introduction to media queries and their usage, along with a comparison with mobile web development.
<!--more-->


## Media Queries

### Media Queries

| Device                            | Pixel Range      |
| --------------------------------- | ---------------- |
| Extra Small Devices (Mobile)      | 0px - 768px      |
| Small Devices (Tablet)            | 768px - 992px    |
| Medium Devices (Desktop)          | 992px - 1200px   |
| Large Devices (Laptops, Monitors) | 1200px and above |



### Usage of Media Queries:

**First Method - Non-Shorthand**

```css
<style>
  /*1. Wide Screens*/
  @media screen and (min-width: 1200px) {
      ...
  }
  /*2. Medium Screens*/
  @media screen and (min-width: 992px) and (max-width: 1200px) {
      ...
  }
  /*3. Small Screens*/
  @media screen and (min-width: 768px) and (max-width: 992px) {
      ...
  }
  /*4. Extra Small Screens*/
  @media screen and (max-width: 768px) {
      ...
  }
</style>
```



**Second Method - Shorthand**

```css
<style>
  /*1. Extra Small Screens*/
  /*Write corresponding styles directly, for example*/
  .container{
    width: 100%;
    background: yellow;
  }
  /*2. Small Screens*/
  @media (min-width: 768px){
    ...
  }
  /*3. Medium Screens*/
  @media(min-width: 992px){
    ...
  }
  /*4. Wide Screens*/
  @media(min-width:1200px){
    ...
  }
</style>
```



### Media Queries Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        html,body{
            padding: 0;
            margin: 0;
            height: 100%;
        }
        .container {
            width: 1200px;
            height: 1000px;
            margin:0 auto;
            background: orange;
        }

        /*1. Extra Small Screens  100% width, yellow background*/
        /*2. Small Screens  750px width, blue background*/
        /*3. Medium Screens  970px width, green background*/
        /*4. Wide Screens  1170px width, pink background*/

        /*1. Extra Small Screens  100% width, yellow background*/
        .container{
            width: 100%;
            background: yellow;
        }
        /*2. Small Screens  750px width, blue background*/
        @media (min-width: 768px){
            .container{
                width: 750px;
                background: skyblue;
            }
        }
        /*3. Medium Screens  970px width, green background*/
        @media(min-width: 992px){
            .container{
                width: 970px;
                background: yellowgreen;
            }
        }
        /*4. Wide Screens  1170px width, pink background*/
        @media(min-width:1200px){
            .container{
                width: 1170px;
                background: pink;
            }
        }
    </style>
</head>
<body>
<div class="container"></div>
</body>
</html>
```



## Comparison with Mobile Web Development



| Development Approach, Corresponding Scenarios | Mobile Web Development + PC Development                      | Responsive Web Design (RWD)                                  |
| --------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Use Cases                                     | Typically used when there is an existing PC website and a separate mobile version needs to be developed. | Used for building new websites that require adaptation to mobile devices, aiming for a single codebase across various devices, providing flexibility. |
| Development                                   | Highly targeted, resulting in high development efficiency.   | Requires compatibility with various devices, resulting in more complex code and potentially slower loading times. |
| Adaptation                                    | Primarily targets mobile devices, with limited tablet support. | Adaptable to a wide range of devices.                        |
| Efficiency                                    | Simple code and fast loading times.                          | More complex code and potentially slower loading times.      |