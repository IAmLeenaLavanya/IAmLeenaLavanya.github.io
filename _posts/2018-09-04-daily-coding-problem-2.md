---
layout: post
title:  "Daily Coding Problem: Problem #2"
date:   2018-09-04 12:30:00 +0800
tags: [c++,daily coding problem]
published: true
---

The Daily Coding Problem (Day 2) was given an array of integers, to return another array of integers consisting of the product of all the integers of the original array except the one at place i (i being the place of each integer in the original list). For instance, an array of [1, 2, 3] should return [6, 3, 2].


```c++
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    vector<int> ints;
    int product = 1;
    int n;
    
    while (cin >> n) {ints.push_back(n); product*=n;}
    
    for (int i = 0; i < ints.size(); ++i) cout << (product / ints[i]) << " ";
}
```
