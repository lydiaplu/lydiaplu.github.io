---
title: Drawing Rectangles and Circles on Canvas
date: 2018-01-03 20:08:12
toc: true
categories:
- canvas

---

**Content:** How to draw rectangles and circles on a Canvas and save and restore canvas states.
<!--more-->

### Drawing Rectangles

- **rect()**: Doesn't have its own path, needs manual stroke and fill operations.
- **strokeRect()**: Has its own path, doesn't require explicit stroke.
- **fillRect()**: Has its own path, doesn't require explicit fill.
- **clearRect()**: Clears a specified region of the canvas.

#### Three Rectangle Drawing Methods

```javascript
rect(x, y, w, h); // Doesn't have its own path, needs manual stroke and fill operations
strokeRect(x, y, w, h); // Has its own path, doesn't require explicit stroke
fillRect(x, y, w, h); // Has its own path, doesn't require explicit fill
```

Parameters are: x coordinate, y coordinate, width, and height.

```javascript
// rect
ctx.fillStyle = "skyblue"
ctx.rect(100, 100, 300, 200);
ctx.stroke(); // Needs manual stroke
ctx.fill(); // Needs manual fill

// strokeRect
ctx.strokeRect(500, 100, 300, 200);

// fillRect
ctx.fillRect(900, 100, 300, 200);
```

![Rectangle API](/images/10-2/rectApi.png)

#### clearRect() Clears the Canvas

```clearRect(x, y, w, h);```

Parameters are: x coordinate, y coordinate, width, and height.

```javascript
// Clears a specified region of the canvas
ctx.clearRect(0, 0, canvas.width, canvas.height);
```

### Drawing Arcs

```arc(x, y, r, startAngle, endAngle, anticlockwise)```

**Parameters:**

+ x: x-coordinate of the center of the arc.
+ y: y-coordinate of the center of the arc.
+ r: Radius of the arc.
+ startAngle: Starting angle (in radians).
+ endAngle: Ending angle (in radians).
+ anticlockwise: Whether to draw the arc anticlockwise (true) or clockwise (false, default).

**Degrees and Radians**

Radians: 360 degrees equals 2 * Math.PI.

Degrees: 1 degree equals Math.PI/180 radians.

**Positive and Negative Angles**

Starting position: 0 degrees (on the right side of the center) is the reference point, and it's not affected by the starting angle in the parameters.

Positive values: Represent angles in a clockwise direction from 0 degrees (on the right side).

Negative values: Represent angles in a counterclockwise direction from 0 degrees (on the right side).

![Angle](/images/10-2/angle.png)

**Testing Arc Drawing, Example:**

```javascript
var canvas = document.getElementById("canvas");
var ctx = canvas.getContext("2d");

// Clockwise, rotate to 90 degrees
ctx.strokeStyle = "dodgerblue";
ctx.beginPath();
ctx.arc(100, 100, 80, 0, 90 * Math.PI / 180, false);
ctx.stroke();

// Clockwise, rotate to -90 degrees
ctx.beginPath();
ctx.arc(400, 100, 80, 0, -90 * Math.PI / 180, false);
ctx.stroke();

// Clockwise, rotate to 270 degrees
ctx.beginPath();
ctx.arc(700, 100, 80, 0, 270 * Math.PI / 180, false);
ctx.stroke();

// Clockwise, rotate to -270 degrees
ctx.beginPath();
ctx.arc(1000, 100, 80, 0, -270 * Math.PI / 180, false);
ctx.stroke();


// Counterclockwise, rotate to 90 degrees
ctx.strokeStyle = "deeppink";
ctx.beginPath();
ctx.arc(100, 400, 80, 0, 90 * Math.PI / 180, true);
ctx.stroke();

// Counterclockwise, rotate to -90 degrees
ctx.beginPath();
ctx.arc(400, 400, 80, 0, -90 * Math.PI / 180, true);
ctx.stroke();

// Counterclockwise, rotate to 270 degrees
ctx.beginPath();
ctx.arc(700, 400, 80, 0, 270 * Math.PI / 180, true);
ctx.stroke();

// Counterclockwise, rotate to -270 degrees
ctx.beginPath();
ctx.arc(1000, 400, 80, 0, -270 * Math.PI / 180, true);
ctx.stroke();
```

![Arc Drawing](/images/10-2/arcRotate.png)

### Saving and Restoring Canvas States

- **save()**: Saves the current drawing state.
- **restore()**: Restores the most recently saved drawing state.

Multiple states can be saved using a stack (last in, first out) with `save()`, and `restore()` can be used to retrieve them.

![Save Sequence](/images/10-2/saveSeque.png)

```javascript
var canvas = document.getElementById("canvas");
var ctx = canvas.getContext("2d");

// First drawing
ctx.fillStyle = "skyblue";
ctx.rect(100, 100, 200, 200);
ctx.stroke();
ctx.fill();
// Save the drawing state
ctx.save();

// Second drawing
ctx.beginPath();
ctx.fillStyle = "deeppink";
ctx.rect(350, 100, 200, 200);
ctx.stroke();
ctx.fill();
// Save the drawing state
ctx.save();

// Third drawing
ctx.beginPath();
ctx.fillStyle = "orange";
ctx.rect(600, 100, 200, 200);
ctx.stroke();
ctx.fill();

// Fourth drawing
ctx.beginPath();
// Restore the previous saved state
ctx.restore();
ctx.rect(850, 100, 