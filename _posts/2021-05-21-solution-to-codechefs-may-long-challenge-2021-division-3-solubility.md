---
layout: post
title:  "Solution to CodeChef's May Long Challenge 2021 Division 3 Solubility"
date:   2021-05-21 20:00:00 +0800
tags: [c++, competitive programming, codechef]
published: true
---

The solution to SOLBLTY from Codechef's May Challenge 2021 Division 3 (Rated). We start off with 1000ml of water that can be dissolved at Ag/100ml. For a unit increase in temperature, the solubility of sugar increases by Bg/100ml.

The answer can thus be found with the equation:

Max amount of sugar = `(((100 - A) * B) + A) * 10`

```c++
#include <iostream>
using namespace std;

int main() {
	int n, i, initialtemp, initialsolubility, increaseinsolubility;
	
	cin >> n;
	
	for (i = 0; i < n; i++) {
	    cin >> initialtemp >> initialsolubility >> increaseinsolubility;
	    
	    cout << (((100 - initialtemp) * increaseinsolubility) + initialsolubility) * 10 << endl;
	}
	return 0;
}
```
