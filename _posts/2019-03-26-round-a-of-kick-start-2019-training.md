---
layout: post
title:  "Round A of Google Kick Start 2019 - Training"
date:   2019-03-26 18:00:00 +0800
tags: [c++, competitive programming, google kickstart]
published: true
---

Below is a solution for both test sets of Training (7pts, 13pts), Round A of Kick Start 2019. It first sorts all the students by descending order of skill and then calculates the number of hours required for a 'fair' `n - (p - 1)` combinations to find the minimum number of hours.

```c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

bool desc (int i, int j) {return (i > j);}

int main() {
	int t; cin >> t;
	for (int i = 0; i < t; i++) {
	    int hours = 0, n, p; cin >> n >> p;
	    
	    vector <int> st (n);
	    for (int j = 0; j < n; j++) cin >> st[j];
	    sort (st.begin(), st.end(), desc);
	    
	    for (int j = 0; j < n - (p - 1); j++) {
	        int h = 0;
	        for (int k = 0; k < p; k++) h += st[j + k];
	        if ((st[j] * p - h) < hours || j == 0) hours = (st[j] * p - h);
	    }
	    
	    cout << "Case #" << (i + 1) << ": " << hours << endl;
	}
	return 0;
}
```
