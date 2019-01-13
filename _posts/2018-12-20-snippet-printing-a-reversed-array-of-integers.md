---
layout: post
title:  "Printing A Reversed Array of Integers"
date:   2018-12-30 15:40:00 +0800
tags: [c++, snippets]
published: true
---

What this does is read integer by integer from cin and insert it at the beginning of a string variable. The string variable is then printed to cout. Another way to do this would be to create a vector, store the integers and then print it in reverse - but that would take two loops.

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
