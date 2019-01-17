---
layout: post
title:  "The Basic Lazy Load (ft. Images & IFrames)"
date:   2019-01-17 16:00:00 +0800
tags: [javascript,html,site performance,images]
published: true
---

bLazy, Echo.js, Yet Another Lazy Loader, jQuery / Wordpress plugins are some of the many libraries designed to speed up initial load, reduce data usage, lighten server load as well as provide a host of other benefits resulting from a site not attempting to call and display every image, script, add-on, iframe (wherever they may be in the page) before it renders itself.

However, for many sites that are running with a hodgepodge of often un-updated and conflicting JavaScript libraries, installing and implementing a library lazy load doesn’t work. Sometimes it’s unresponsive or glitchy and when neither, it just doesn’t run altogether. And anyway, for a site owner that spent the last few days compressing, deleting, combining script / style files to reduce resource requests, calling yet another additional library doesn’t quite have the kick.

Recently I've had to optimize the initial load speed of a client's site via front-end. The site mainly loaded images and iframes. Apart from three images, the rest of these were not in the initial window viewport. Some were nearly at the end of the 3000px-long site, but were being loaded before the site could display.

### My Solution

```javascript
$('.llazy[data-loaded="false"]').each(function() {
    var llazy = $(this);
    //...
});
```

The images / iframes are given the class `llazy`, their `src` switched to `data-src` and an attribute `data-loaded` is set to `false`. To prevent the structure of the site from collapsing, the initial `src` of the images is set to a gray ~1KB placeholder SVG (with the same width-height ratio of the images). The iframes already had fixed heights.

```javascript
llazy[0].getBoundingClientRect().top - window.innerHeight < 0
```

The above code was written before I discovered the IntersectionObserver, but I suppose since the site doesn’t scroll horizontally, it will do for now. You could change the zero of course to say 50 or 200 or whatever and the images / iframes would load when they and the user's viewport have that much (or less than that much) of distance before it appears on screen.

#### The Final Code

```javascript
jQuery.noConflict();
window.addEventListener("scroll", function() {
    jQuery('.llazy[data-loaded="false"]').each(function() {
        var llazy = jQuery(this);
        if (llazy[0].getBoundingClientRect().top - window.innerHeight < 0) {
            jQuery(this).attr("data-loaded", "true");
            jQuery(this).attr("src", jQuery(this).attr("data-src"));
        }
    });
});
```

Mootools *and* jQuery were present, hence the `.noConflict()`.

#### PROS

1. Loads on scroll, so it would be possible to save on server requests and bandwidth.
2. 293B when compressed.
3. One code for both images and iframes.

#### CONS

1. Requires jQuery. *A vanilla solution could be written though. I would just need to find IE's fall-back for getBoundingClientRect.*
2. Only vertical scrolling is considered.
3. Doesn’t work on scripts and whatever else.
4. Only triggered on scroll so if the site is somehow loaded mid-page, users will see placeholders for as long as until they initiate a scroll.

I will be working on those cons time to time but till then, here's the live demo.

<p data-height="300" data-theme-id="21171" data-slug-hash="gjGWqg" data-default-tab="html,result" data-user="leenalavanya" data-pen-title="A Really Simple Lazy Load - Images & IFrames" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid black; margin: 1em 0; padding: 1em;" class="codepen"><span>See the Pen <a href="https://codepen.io/leenalavanya/pen/gjGWqg/">A Really Simple Lazy Load - Images & IFrames</a> by Leena Lavanya (<a href="https://codepen.io/leenalavanya">@leenalavanya</a>) on <a href="https://codepen.io">CodePen</a>.</span></p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
