---
title: HTML5 New Semantic Tags
date: 2016-03-05 20:12:13
toc: true
categories:
- HTML5

---

**Content**: HTML5's new semantic tags and compatibility handling for these new tags.
<!--more-->

## New Semantic Tags

HTML5's new semantic tags are similar to `div` but provide a more meaningful structure, helping to avoid naming conflicts.

*Important notes:*

1. The `main` tag is not supported in IE.
2. IE8 and below do not support the new tags, but they can be used with dynamic JavaScript creation (make sure to set the created elements to `display: block`).

| Tag     | Description      |
| ------- | ---------------- |
| header  | Header           |
| main    | Main content     |
| footer  | Footer           |
| nav     | Navigation       |
| aside   | Content aside    |
| article | Document         |
| section | Document section |

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <header>
    <nav></nav>
  </header>
  <main>
    <aside></aside>
    <article>
      <section></section>
      <section></section>
      <section></section>
    </article>
  </main>
  <footer></footer>
</body>
</html>
```

## Compatibility Handling

**Method 1:**

Use JavaScript to dynamically create the new tags for compatibility.

```HTML
<!-- Generate [if lte IE 8] conditional comment -->
<!--[if lte IE 8]>
  <script>
    var headerDom = document.createElement('header');
    document.body.appendChild(headerDom);
    headerDom.style.display = 'block';
    console.log('I am called');
  </script>
<![endif]-->
```

**Method 2:**

Use the JavaScript library (html5shiv.min.js) to achieve compatibility with semantic tags.

```HTML
  <!-- Load this js file only for specified IE versions using conditional comments -->
  <!--[if lte IE 8]>
    <script src='js/html5shiv.min.js'></script>
  <![endif]-->
```

## Conditional Comments

Expanding on the knowledge mentioned earlier, we used conditional comments. Here's an extension:

The "emmpty" syntax for conditional comments: `cc:ie6 + tab`.

*Note: The "emmpty" syntax generates "[if lte IE 6]," and if you need to check for other versions, you should modify it manually.*

```
<!--[if lte IE 6]>
    <script src='js/html5shiv.min.js'></script>
<![endif]-->
```

The above code means that if it's IE6 or below, it will load html5shiv.min.js.

**Detailed Syntax:**

- lt: Less than the specified version
- lte: Less than or equal to the specified version
- gt: Greater than the specified version
- gte: Greater than or equal to the specified version

```
<!-- Less than IE9 -->
<!--[if lt IE 9]>
<![endif]-->

<!-- IE9 and below -->
<!--[if lte IE 9]>
<![endif]-->

<!-- Greater than IE9 -->
<!--[if gt IE 9]>
<![endif]-->

<!-- IE9 and above -->
<!--[if gte IE 9]>
<![endif]-->
```

Other information:

1. Typing "lorem" + tab generates placeholder text, and for multiple paragraphs, you can use "lorem1000" + tab.