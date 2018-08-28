---
layout: post
title:  "Using Canvas to Create Cloth that Moves"
date:   2018-08-27 19:30:00 +0800
categories: ""
tags: "canvas, javascript, html"
published: true
---

Last week, I completed a pen that turned any image into swaying cloth. At first, it had 0 hits but the next day, after it was picked, I got over 1139 hits in a matter of 24 hours. That's why I decide to write a post on how to create such an effect with the HTML5 Canvas.

### The HTML/CSS

```html
<canvas id="c" width="560" height="350"></canvas>

<canvas id="canv"></canvas>
<img id="imgt" src="http://vignette4.wikia.nocookie.net/pixar/images/a/a0/Brave_tapestry_new.jpg/revision/latest?cb=20130224170155"></img>
```

```css
html,body{margin:0;padding:0;height:100%;width:100%;background:#f0f0f0}#c{max-width:calc(100% - 20px);margin:0px auto;display:block}#canv,#imgt{display:none}
```

The first canvas (`#c`) is the main canvas and is where the cloth will be drawn. The image at the very bottom of the code is the image that will be used to make the cloth (it can be linked to any image url) and the other canvas (`#canv`) is used to resize the image to the size of the cloth as well move the image with the swaying of the cloth.

### Drawing Strings
#### The Variables

```js
var c = document.getElementById("c");
var ctx = c.getContext('2d');
ctx.lineWidth = 1;
var boxWidth = 5;
var boxHeight = 5;
var verticalLimit = c.height - 79;
var range = -2;
var change = 0.1;
var linesNumber = (c.width - 40) / boxWidth + ((verticalLimit - 20) / boxHeight) + 1;
var times = -1 * boxWidth;
var times2 = 0;
var i;
```

The code above fetches the main canvas and declares a number of variables:
- lineWidth = the thickness of the string
- boxWidth/boxHeight = the spacing between each string
- verticalLimit = the height of the cloth
- range = the left and right boundaries for which the cloth will move
- change = the amount that the cloth changes position every few seconds.
- linesNumber = an approximate calculation of the total number of strings. It is used in a loop to make sure the loop doesn't run too many times.
- times/i = variables also used in the loop

### The Loop

```js
function drawCircle() {
	ctx.clearRect(0, 0, c.width, c.height);
	times = 20;
	times2 = 20;
	i = 0;
	for (i = 0; i < linesNumber; i++) {
		if (times <= c.width - 20) {
			ctx.beginPath();
			ctx.moveTo(times, 10);
			ctx.quadraticCurveTo(times + range * 3, verticalLimit - 200, times + range, verticalLimit);
			ctx.stroke();
			times += boxWidth;
		} else if (times2 <= verticalLimit) {
			ctx.beginPath();
			ctx.moveTo(12, times2);
			ctx.lineTo(c.width - 12, times2);
			ctx.stroke();
			times2 += boxHeight;
		}
	}
	window.setTimeout(drawCircle, 1000 / 60);
	if (range >= 2) {
		change = -0.1;
	} else if (range <= -2) {
		change = 0.1;
	}
	range += change
}

```

The function (`drawCircle()`) is **very** inappropriately named but I would ignore it for now. It clears the canvas, draws the horizontal lines, then the vertical ones, updates the new positions (to make it move) and then starts the process again and again to give it an animated effect.

Placing an Image as the Background

```js
	loadBackground(range * 1.2, 0);
	var img = document.getElementById("canv");
	var pat = ctx.createPattern(img, "repeat");
	ctx.strokeStyle = pat;
```

By inserting this piece of code above in the loop and the function below in the script file, the lines/strings will be drawn (not using a static color) but with the background of another canvas, which is used to resize and move the image with the swaying of the cloth.

```js
var ct = document.getElementById('canv');
ct.width = c.width;
ct.height = c.height;
var ctxt = ct.getContext('2d');
var imgt = document.getElementById('imgt');

function loadBackground(a, b) {
	ctxt.drawImage(imgt, a, b, c.width + a, c.height + b)
}
```
