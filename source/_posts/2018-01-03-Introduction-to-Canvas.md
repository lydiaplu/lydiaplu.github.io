---
title: Introduction to Canvas
date: 2018-01-03 18:09:31
toc: true
categories:
- canvas

---

**Content:** Introduction to Canvas, basic drawing APIs, and style settings
<!--more-->

### Canvas Coordinate System

The canvas coordinate system has its origin at the top-left corner, with the following rules:

- The positive x-direction is to the right.
- The positive y-direction is down.

![Canvas Coordinate System](/images/10-1/location.jpg)

### Basic Steps for Drawing on Canvas

```javascript
// Get the canvas element
var canvas = document.getElementById("canvas");
// Get the drawing context
var ctx = canvas.getContext("2d");
// Set the starting point for drawing
ctx.moveTo(100, 100);
// Draw the path
ctx.lineTo(300, 100);
// Stroke the path (outline)
ctx.stroke();
```

### Canvas Width and Height

By default, a canvas has a width of 300 pixels and a height of 150 pixels. You can set the canvas width and height using the HTML attributes, and you cannot use CSS to set these dimensions.

```html
<canvas id="canvas" width="600" height="400" style="border:1px solid #ccc"></canvas>
```

```javascript
var canvas = document.getElementById("canvas");
// Get the canvas width and height
console.log(canvas.width);
console.log(canvas.height);
```

### Basic Drawing APIs in Canvas

| Simple API          | Description            |
| ------------------- | ---------------------- |
| moveTo(x, y)        | Set the starting point |
| lineTo(x, y)        | Draw a path            |
| stroke()            | Stroke the path        |
| fill()              | Fill the path          |
| stroke() and fill() | Both stroke and fill   |
| beginPath()         | Start a new path       |
| closePath()         | Close the path         |

#### Stroke and Fill

- `stroke()`: Draw the outline of a path.
- `fill()`: Fill the area enclosed by a path.
- `stroke()` and `fill()`: Both stroke and fill the path.

```javascript
var canvas = document.getElementById("canvas");
var ctx = canvas.getContext("2d");
ctx.lineWidth = 10;
ctx.moveTo(100, 100);
ctx.lineTo(300, 100);
ctx.stroke();

// Begin a new path; styles won't affect previous path
ctx.beginPath();
ctx.lineWidth = 20;
ctx.moveTo(100, 150);
ctx.lineTo(300, 150);
ctx.stroke();
```

### Style Settings in Canvas

| Style API      | Description                                              |
| -------------- | -------------------------------------------------------- |
| strokeStyle    | Stroke color                                             |
| fillStyle      | Fill color                                               |
| lineWidth      | Line width                                               |
| lineCap        | Line cap style (butt, round, square)                     |
| lineJoin       | Line join style (miter, round, bevel)                    |
| setLineDash()  | Set line dash pattern                                    |
| getLineDash()  | Get line dash pattern                                    |
| lineDashOffset | Set line dash offset (negative values move to the right) |

#### Line Width, Stroke Color, and Fill Color

```javascript
var canvas = document.getElementById("canvas");
var ctx = canvas.getContext("2d");
ctx.lineWidth = 10;
ctx.strokeStyle = "#ccc";
ctx.fillStyle = "skyblue";
ctx.moveTo(100, 100);
ctx.lineTo(300, 100);
ctx.lineTo(300, 300);
ctx.lineTo(100, 300);
ctx.lineTo(100, 100);
ctx.stroke();
ctx.fill();
```

#### getLineDash() to Get the Line Dash Pattern

#### lineDashOffset for Line Dash Offset

A positive value moves the line dash pattern to the left, while a negative value moves it to the right.

### Other Drawing Techniques in Canvas

#### Drawing Curves

To draw curves on a canvas, you can draw a series of points that follow the curve's equation.

```javascript
var canvas = document.getElementById("canvas");
var ctx = canvas.getContext("2d");

ctx.moveTo(0, 0);
for (var i = 0; i < 1000; i++) {
    var x = i;
    var y = 100 * Math.sin(x / 50) + 100;
    ctx.lineTo(x, y);
}
ctx.stroke();
```

#### Gradient Fill

To create gradient effects, draw one point at a time and change the color attribute.

```javascript
var canvas = document.getElementById("canvas");
var ctx = canvas.getContext("2d");

ctx.lineWidth = 30;
for (var i = 0; i < 255; i++) {
    ctx.beginPath();
    ctx.moveTo(100 + i, 100);
    ctx.strokeStyle = 'rgb(' + i + ',0,0)';
    ctx.lineTo(100 + i + 1, 100);
    ctx.stroke();
}
```