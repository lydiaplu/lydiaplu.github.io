---
title: Viewport for Visual Layout
date: 2016-03-17 10:20:31
toc: true
categories:
- Mobile Web

---

**Content**: Fluid layout, requirements for mobile web development, and an introduction to the viewport.
<!--more-->

## Fluid Layout

A fluid layout, also known as a percentage-based layout, adjusts its elements based on the screen's width by setting the width of containers in percentages. This approach allows content to expand and contract, adapting to different screen sizes without being limited by fixed pixel dimensions.

## Requirements for Standard Mobile Development:

1. Horizontal scrolling should be avoided. The webpage's width, or viewport, should match the browser's width.
2. The scaling ratio should be consistent with the PC version.
3. User-initiated scaling should be disabled.

## Introduction to the Viewport

### About the Viewport

1. In the context of mobile devices, the viewport refers to the area where a webpage is displayed—it's our visual window.
2. The viewport can be configured with width and height settings, allowing proportional zooming and control over user-initiated scaling.

### Viewport Properties

| Property      | Description                                    | Values                  |
| ------------- | ---------------------------------------------- | ----------------------- |
| width         | Sets the viewport's width, default unit is px  | Numeric, device-width   |
| height        | Sets the viewport's height, default unit is px | Same as above           |
| initial-scale | Default initial zoom scale                     | Numeric                 |
| user-scalable | Enables or disables user-initiated scaling     | no, yes (default), 0, 1 |
| maximum-scale | Maximum allowed zoom scale                     | Numeric                 |
| minimum-scale | Minimum allowed zoom scale                     | Numeric                 |

### Using the Viewport

```html
<head>
  <!-- Standard mobile web page configuration, commonly used international viewport settings -->
  <!-- Emmet syntax: meta:vp -->
  <!-- Ensures the current viewport matches the device's width, default scaling matches the PC version, and user-initiated scaling is disabled -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=0"/>
</head>
```