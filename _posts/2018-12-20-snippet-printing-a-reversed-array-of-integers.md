---
layout: post
title:  "Printing A Reversed Array of Integers"
date:   2018-12-30 15:40:00 +0800
tags: [c++, snippets]
published: true
---

Sample Input:

`5`

`2 3 4 5 7`

Sample Output:

`7 5 4 3 2`

```c++
#include <iostream>
#include <string>
using namespace std;

int main() {
    int n, p; cin >> n;
    string s;

    while (cin >> p) s.insert(0, (" " + to_string(p)));
    cout << s.substr(1, s.size()) << endl;

    return 0;
}
```
