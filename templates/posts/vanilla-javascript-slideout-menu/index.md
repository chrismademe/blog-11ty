---
author: Chris Galbraith
title: Create a Simple Slideout Menu using Vanilla Javascript
date: "2019-08-17T22:40:32.169Z"
description: In this tutorial, we'll create a slick slideout menu using Vanilla Javascript
tags:
    - post
    - code
    - javascript
    - css
layout: post
---

One of the most important parts of any site is the navigation, especially with responsive design since you don't always have much [space to place with](https://uxmag.com/articles/10-responsive-design-problems-and-fixes). That's why I put together this super simple yet effective slide out menu, using good old fashioned HTML, CSS and Javascript. If you're looking to get way from jQuery, this is [definitely for you](http://youmightnotneedjquery.com/).

_If you have a small site or you only need a few links showing in your main navigation, you should consider whether you actually need a hidden menu._

### The HTML

First, layout the markup for your menu.

```html
<nav id="slideout-menu" class="slideout-menu">
    <a id="slideout-close" class="slideout-close" href="#">&times;</a>
    <ul>
        <li><a href="#" title="Our homepage">Home</a></li>
        <li><a href="#" title="About CompanyX">About Us</a></li>
        <li><a href="#" title="Services we offer">Our Services</a></li>
        <li><a href="#" title="Get in touch!">Contact Us</a></li>
    </ul>
</nav>

<button id="slideout-toggle" class="slideout-toggle" href="#">
    <span></span>
    <span></span>
    <span></span>
</button>
```

Let's break this down in to pieces.

```html
<nav id="slideout-menu" class="slideout-menu">
    ...
</nav>
```

We're using the HTML5 `nav` element, with an ID for toggling (more on this later) and a class for styling.

```html
<button id="slideout-close" class="slideout-close" href="#">&times;</button>
```

Next, we create a `button`. This will be used for closing the menu when it's open.

```html
<ul>
    <li><a href="#" title="Our homepage">Home</a></li>
    <li><a href="#" title="About CompanyX">About Us</a></li>
    <li><a href="#" title="Services we offer">Our Services</a></li>
    <li><a href="#" title="Get in touch!">Contact Us</a></li>
</ul>
```

Now our navigation links.

```html
<button id="slideout-toggle" class="slideout-toggle" href="#">
    <span></span>
    <span></span>
    <span></span>
</button>
```

Finally, we'll create a simple but awesome looking [hamburger button](https://en.wikipedia.org/wiki/Hamburger_button).

### The CSS

Let's make this thing look awesome!

```css
body {
    color: #444;
    font-family: sans-serif;
    font-size: 14px;
}

.slideout-menu {
    background-color: #eee;
    padding: 42px 0;
    position: absolute;
    left: -280px;
    transition: left 0.4s;
    top: 0;
    height: 100vh;
    width: 280px;
}

.slideout-menu.is-open {
    left: 0;
}

.slideout-menu ul {
    list-style: none;
    margin: 0;
    padding: 0;
}

.slideout-menu ul li {
    display: block;
    margin: 0;
    padding: 0;
}

.slideout-menu ul li a {
    color: #555;
    display: block;
    font-size: 1.4em;
    padding: 8px 24px;
    text-decoration: none;
}

.slideout-menu a.slideout-close {
    color: #888;
    display: block;
    font-size: 2em;
    padding: 24px 42px;
    position: absolute;
    right: 0;
    top: 0;
    text-decoration: none;
}

.slideout-toggle {
    display: inline-block;
    padding: 24px;
    width: 18px;
}

.slideout-toggle span {
    background-color: #888;
    display: block;
    height: 2px;
    width: 100%;
    margin: 3px 0;
}
```

Alright, the breakdown. First, we want to style the menu itself.

```css
.slideout-menu {
    background-color: #eee;
    padding: 42px 0;
    position: absolute;
    left: -280px;
    transition: left 0.4s;
    top: 0;
    height: 100vh;
    width: 280px;
}

.slideout-menu.is-open {
    left: 0;
}
```

To make sure it's hidden from view, we're positioning it absolutely and setting the value of `left` to `-280px`, which coincidently happens to be the width of the menu. If you change the width, be sure to amend the `left` value accordingly. There's also a `transition` there so the menu appears nicely, not just like BAM! (Nobody needs that)

And of course, the `is-open` class. We'll use this with our Javascript to show the menu when its toggled.

```css
.slideout-menu ul {
    list-style: none;
    margin: 0;
    padding: 0;
}

.slideout-menu ul li {
    display: block;
    margin: 0;
    padding: 0;
}

.slideout-menu ul li a {
    color: #555;
    display: block;
    font-size: 1.4em;
    padding: 8px 24px;
    text-decoration: none;
}
```

The menu styling. I've opted for a simple, well spaced list (remember, we're aiming this at mobile users so large [tap targets](https://developers.google.com/speed/docs/insights/SizeTapTargetsAppropriately?hl=en) are a must!)

```css
.slideout-menu a.slideout-close {
    color: #888;
    display: block;
    font-size: 2em;
    padding: 24px 42px;
    position: absolute;
    right: 0;
    top: 0;
    text-decoration: none;
}
```

Next, the close button. Again, I've added plenty of padding so it's easy to use from a mobile device. It looks pretty, too.

```css
.slideout-toggle {
    display: inline-block;
    padding: 24px;
    width: 18px;
}

.slideout-toggle span {
    background-color: #888;
    display: block;
    height: 2px;
    width: 100%;
    margin: 3px 0;
}
```

And finally, the hamburger. Yum. This is quite simply some `span` tags styled to look like a burger.

### The Javascript

Pulling it all together. Without this, our menu is pretty much useless. Now, before we go any further I just want to say this can of course be achieved, very easily, with jQuery but I wanted to create something that doesn't require any frameworks.

Onwards...

```js
document.addEventListener("DOMContentLoaded", function() {
    var menu, toggleButton, closeButton;

    // Set Elements
    menu = document.getElementById("slideout-menu");
    toggleButton = document.getElementById("slideout-toggle");
    closeButton = document.getElementById("slideout-close");

    // Toggle Menu
    toggleButton.addEventListener("click", function(e) {
        e.preventDefault();
        menu.classList.toggle("is-open");
    });

    // Close Menu
    closeButton.addEventListener("click", function(e) {
        e.preventDefault();
        menu.classList.remove("is-open");
    });
});
```

So, let's break this down:

```js
document.addEventListener('DOMContentLoaded', function() {
    ...
});
```

Before anything else, let's make sure the DOM has loaded properly by listening out for the `DOMContentLoaded` event. For jQuery users, this is the same as `$(document).ready`.

```js
var menu, toggleButton, closeButton;

// Set Elements
menu = document.getElementById("slideout-menu");
toggleButton = document.getElementById("slideout-toggle");
closeButton = document.getElementById("slideout-close");
```

Next, we're defining a few variables that we'll use and finding the elements we need to manipulate by their IDs (as I mentioned earlier).

```js
// Toggle Menu
toggleButton.addEventListener("click", function(e) {
    e.preventDefault();
    menu.classList.toggle("is-open");
});
```

So now we've got our elements, we're going to listen for clicks on the toggle button. (for jQuery, this would be `$('#slideout-toggle').click(function(e)) {})` and then we add the `is-open` class if it's not there, otherwise we remove it.

In my example, the toggle button is positioned in such a way that when the menu is open you can't use it, but if it was visible, clicking it while the menu is open will close it.

```js
// Close Menu
closeButton.addEventListener("click", function(e) {
    e.preventDefault();
    menu.classList.remove("is-open");
});
```

And finally, we listen out for clicks on our close button (inside the menu) and then remove the `is-open` class.

That's it! You have an awesome slideout menu for your next site.

### Demo

For a working demo, head over to [Codepen](http://codepen.io/chrismademe/pen/bEMQbK) :).
