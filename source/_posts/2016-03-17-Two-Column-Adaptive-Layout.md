---
title: Two-Column Adaptive Layout
date: 2016-03-17 21:35:12
toc: true
categories:
- Mobile Web

---

**Content**: A left-fixed, right-adaptive layout.
<!--more-->

## Left-Fixed, Right-Adaptive Layout

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <style>
        html, body {
            height: 100%;
            margin: 0;
            padding: 0;
        }

        div {
            box-sizing: border-box;
        }

        .left {
            float: left;
            width: 100px;
            height: 100%;
            background: yellowgreen;
            border: 1px solid orchid;
        }

        .right {
            height: 100%;
            overflow: hidden;
            background: skyblue;
            border: 1px solid orange;
        }
    </style>
</head>
<body>
<div class="left">Left</div>
<div class="right">Right</div>
</body>
</html>
```

Preview:

![Two-Column Adaptive Layout](/Users/lupan/study/blog/Englilsh-Blog/source/_posts/images/2016-03-17-Two-Column-Adaptive-Layout.gif)