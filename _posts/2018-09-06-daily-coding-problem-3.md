---
layout: post
title:  "Daily Coding Problem: Problem #3"
date:   2018-09-04 12:30:00 +0800
tags: [c++,daily coding problem]
published: true
---

The Daily Coding Problem (Day 3) was given an array of integers, to return the first postive integer missing. The solution below was to first create a vector of all the non-negative and non-zero integers inputed and then loop from 1 to the largest integer in the vector, looking for the first one missing.


```c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main()
{
    vector<int> ints;
    int n;
    
    while (cin >> n)  if (n > 0)  ints.push_back(n);
    
    for (int i = 1; i <= (*max_element(ints.begin(), ints.end()) + 1); i++) if (find(ints.begin(), ints.end(), i) == ints.end()) {cout << i << endl; break;}
}
```
