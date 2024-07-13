---
title: The Essence of jQuery Plugins
date: 2018-12-08 21:50:30
toc: false
categories:
- javascript

---

**The Essence of jQuery Plugins**

**jQuery Core**

1. The jQuery Instantiation Process - Class Arrays
2. The Essence of Plugins - Extending jQuery
3. Chaining Operations - return this
4. Implicit Iteration - each

**Syntax for jQuery Plugins**

```javascript
(function ($) {
    // Extending the Prototype
    // First Method:
    $.fn.hello = function () {
        $(this).html('hello');
    };
    $.fn.hi = function () {
        $(this).html('hi');
    };

    // Second Method - Using the extend Copying Method:
    $.fn.extend({
        hello: function () {
            $(this).html('hello');
        },
        hi: function () {
            $(this).html('hi');
        }
    });

    // Extending Globally
    // First Method:
    $.hello = function () {
        alert('hello');
    };
    $.hi = function () {
        alert('hi');
    };

    // Second Method - Using the extend Copying Method:
    $.extend({
        hello: function () {
            alert('hello');
        },
        hi: function () {
            alert('hi');
        }
    })

})(jQuery);

// Using the Plugin
$(function () {
    $("#dv1").hello();
    $.hi();
});
```

**Simple Implementation of jQuery's extend**

```javascript
(function ($) {
  	// A Simple Implementation of jQuery's extend
    $.fn.extend = function (obj) {
        for (var key in obj) {
            this[key] = obj[key];
        }
    }
})(jQuery);
```