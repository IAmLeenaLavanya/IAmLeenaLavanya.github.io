---
layout: post
title:  "Lexicographically Lowest Concatenation of Strings - Facebook Hacker Cup 2011 Qualification Round"
date:   2019-01-29 14:30:00 +0800
tags: [c++, facebook hacker cup, competitive programming]
published: true
---

Given an array of a maximum of 9 strings, the below code outputs the lexicographically lowest concatenation of said strings. A normal sort function would compare `string a < string b` but will not output the lexicographically lowest combination given there a different number of characters in each string, hence the `(a + b) < (b + a)`.

If there were a maximum of about 5 strings, then we could generate all possible combinations and select their minimum but with 9 strings, that would result in 362,880 combinations - not a time efficient solution.

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
