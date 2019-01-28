---
layout: post
title:  "How Many Pairs of Perfect Squares? - Facebook Hacker Cup 2011 Qualification Round"
date:   2019-01-28 17:00:00 +0800
tags: [javascript]
published: false
---

We had to find

```javascript
var t = [];

function number_of_square_pairs(t) {
    var c = 0;
    if (t == 0 || t == 1) c = 1;
    else {
        for (var j = 0; j < Math.pow(t / 2, 0.5); j++) {
            var v = Math.pow((t - j * j), 0.5);
            if (v == Math.round(v)) c++;
        }
    }
	return c;
}

function main() {
	var n = t.length;
	for (var i = 0; i < n; i++) {
	    console.log("Case #" + (i + 1) + ": " + number_of_square_pairs(t[i]));
	}
}
```
