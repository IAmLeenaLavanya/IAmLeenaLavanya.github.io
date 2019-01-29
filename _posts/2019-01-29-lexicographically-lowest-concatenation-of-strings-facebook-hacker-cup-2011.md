---
layout: post
title:  "Lexicographically Lowest Concatenation of Strings - Facebook Hacker Cup 2011 Qualification Round"
date:   2019-01-28 17:00:00 +0800
tags: [c++, facebook hacker cup, competitive programming]
published: false
---



```c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

bool c(string a, string b) {
    return (a + b) < (b + a);
}

int main() {
	int n, m, i, k; cin >> n;
	for (i = 0; i < n; i++) {
	    cin >> m;
	    vector<string> s (m);
	    
	    for (k = 0; k < m; k++) cin >> s[k];
	    
	    sort(s.begin(), s.end(), c);
	    
	    cout << "Case #" << (i + 1) << ": ";
	    
	    for (k = 0; k < m; k++) cout << s[k];
	    
	    cout << endl;
	}
	return 0;
}
```
