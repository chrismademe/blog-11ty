---
author: Chris Galbraith
title: Show a message to unsupported browsers without Javascript
date: "2019-08-17T22:40:32.169Z"
tags:
    - post
    - code
    - css
layout: post
---

Sometimes you can't support every browser and whilst you should definitely strive for progressive enhancement, there are some things that just won't look right and you may not have the time or budget to fix those things.

This little snippet below uses the `@supports` query in CSS to hide a message that will be shown the browsers that don't support the feature you're checking for. For me, I usually check for `grid` support but it's upto you what you check for.

```css
.browser-message {
    /* your styles */
}

/* Hide it for modern browsers */
@supports (display: grid) {
    .browser-message {
        display: none;
    }
}
```
