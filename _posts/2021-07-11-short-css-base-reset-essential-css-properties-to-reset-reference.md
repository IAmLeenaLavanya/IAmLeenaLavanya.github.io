---
layout: post
title: Short CSS Base Reset - Essential CSS Properties to Reset [Reference]
date: 2021-07-11 12:00:00 +0800
tags: [css]
published: true
---

As a general CSS reset applied across all elements of a website, use the below.  I've included some (not very helpful) comments to explain the most common use case I have found for each of the properties. 

```css
* {
    margin: 0;/* the amount of space that a paragraph has by default is enormous */
    padding: 0; /* eliminates that little bit of space that the body / html has */
    box-sizing: border-box; /* when you want the width of an element to include padding */
    position: relative; /* for position: absolute to work later */
    border: 0; /* think buttons and their pretty outdated design */
    outline: 0; /* ... */
    background: none; /* again, buttons */
    vertical-align: top; /* to ensure images don't have a weird gap below them */
}
```

### Hyperlink CSS Reset

```css
a {
    text-decoration: none;
    color: inherit; /* takes the color of the parent */
}
a:active {
    outline: 0; /* don't want a blue line once it's been clicked on */ 
}
```

### List CSS Reset

When you use unordered or ordered lists for other website components such as menus.

```css
ul, ol {
    list-style-type: none
}
```
