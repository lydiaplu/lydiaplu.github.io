---
title: Canvas Text Drawing
date: 2018-01-03 22:10:30
toc: true
categories:
- canvas

---

**Content:** How to draw text on a Canvas element
<!--more-->

### Text Drawing

You can draw text on a Canvas using the following methods:

```javascript
// To draw outlined text
strokeText(text, x, y, maxWidth)
// To draw filled text
fillText(text, x, y, maxWidth)
```

#### Parameters

- **text**: The text to be drawn.
- **x, y**: The coordinates for drawing the text (default at the text's bottom-left corner).
- **maxWidth**: Optional, it sets the maximum width for the text.

#### Setting Font

You can specify the font size and style for text drawing. The default font is "10px sans-serif".

```javascript
ctx.font = "40px 'Microsoft YaHei'";
```

**Example**

```javascript
var canvas = document.getElementById("canvas");
var ctx = canvas.getContext("2d");

ctx.strokeStyle = "pink";
ctx.fillStyle = "skyblue";
var text = "Hello, World!";
ctx.font = "40px 'Microsoft YaHei'";
ctx.strokeText(text, 100, 100);
ctx.fillText(text, 100, 200);
```

![Text](/images/10-3/text.png)

#### Setting Horizontal Alignment

**textAlign Property**

This property sets the text alignment relative to the drawing coordinates.

```javascript
ctx.textAlign = "start";
```

- left
- center
- right
- start (default)
- end
- direction (CSS property, rtf ltr), start and end are related to this:
  - If it's "ltr", start behaves the same as left.
  - If it's "rtl", start behaves the same as right.

#### Setting Vertical Alignment

**textBaseline Property**

```javascript
ctx.textBaseline = "top";
```

- top: The text's baseline is at the text's top with some distance.
- middle: The text's baseline is in the middle of the text.
- bottom: The text's baseline is at the text's bottom with some distance.
- hanging: The text's baseline is above the text and sticks to it.
- alphabetic: Default value, the baseline is below the text and crosses through it.
- ideographic: Similar to bottom, but not the same.

**Example**

```javascript
function TextDot(canvasId) {
    this.canvas = document.getElementById(canvasId);
    this.ctx = this.canvas.getContext("2d");
}

TextDot.prototype.init = function () {
    var horizontalAlignments = ["left", "center", "right"];
    var verticalAlignments = ["top", "middle", "bottom"];

    for (var i = 0; i < horizontalAlignments.length; i++) {
        for (var j = 0; j < verticalAlignments.length; j++) {
            var x = this.canvas.width / 6 + this.canvas.width / 3 * i;
            var y = this.canvas.height / 6 + this.canvas.height / 3 * j;
            var text = horizontalAlignments[i] + " --- " + verticalAlignments[j];
            this.drawText(text, x, y, horizontalAlignments[i], verticalAlignments[j]);
            this.drawDot(x, y);
        }
    }
};

TextDot.prototype.drawDot = function (x, y) {
    var width = 20;
    this.ctx.beginPath();
    this.ctx.strokeStyle = "deeppink";
    this.ctx.moveTo(x - width / 2, y);
    this.ctx.lineTo(x + width / 2, y);
    this.ctx.moveTo(x, y - width / 2);
    this.ctx.lineTo(x, y + width / 2);
    this.ctx.stroke();
};

TextDot.prototype.drawText = function (text, x, y, textAlign, textBaseline) {
    this.ctx.font = "20px 'Microsoft YaHei'";
    this.ctx.fillStyle = "#333";
    this.ctx.textAlign = textAlign;
    this.ctx.textBaseline = textBaseline;
    this.ctx.fillText(text, x, y);
};

window.onload = function () {
    var textDot = new TextDot("canvas");
    textDot.init();
};
```

![Align](/images/10-3/align.png)

#### measureText() for Text Width

```javascript
var canvas = document.getElementById("canvas");
var ctx = canvas.getContext("2d");

var text = "Hello, World!";
ctx.font = "20px 'Microsoft YaHei'";
ctx.strokeText(text, 100, 100);
var obj = ctx.measureText(text);
console.log(obj.width);
```

Rotation, translation, and other operations are done in the canvas coordinate system and do not affect previously drawn layers. Subsequent drawings are relative to the modified coordinate system.