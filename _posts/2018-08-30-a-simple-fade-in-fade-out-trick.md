---
layout: post
title:  "Fade-In Fade-Out Hover Effect Using CSS Transitions"
date:   2018-08-27 19:30:00 +0800
tags: [css,transition]
published: true
---

jQuery's `fadeToggle()` is literally the *easiest* way to fade in and fade out elements - onmouseover, onclick or whatever. But what if we wanted the same effect using **only CSS**? Below is a short code to achieve a fade-in fade-out effect on hover - purely using CSS transitions:

### The Initial CSS

```css
.element {
    opacity: 0; /* obviously, it's invisible first */

    /* we scale(0) it so that it virtually takes up no space and acts like a display: none element */
    transform: scale(0);

    /* umm, well */
    transition: opacity 0.3s, transform 0s 0.3s;
}
```

### The On Hover CSS

```css
.element_parent:hover .element {
    opacity: 1; /* now it's visible */
    
    /* and scale(1) so it takes up the space it's supposed to */
    transform: scale(1);
    
    /* again, the confusing bit */
    transition: transform 0s, opacity 0.3s;
}
```

That should be it. Add all the necessary browser prefixes you need. Change the 0.3s **everywhere** if you want to change the speed of the animation.
