---
layout: post
title:  "Trouble Sort Solution - 2nd Try at Google Code Jam"
date:   2018-08-31 16:30:00 +0800
tags: [c++, google code jam]
published: false
---

This is the second piece of C++ code I've written. It's bound to be awful - do forgive me. It's the solution to the 2018 Google Code Jam Qualifying Round B. I'm going to split the solution into parts.

## Function TroubleSort() In C++

The below code just performs the trouble sort function. It returns the sorted list of integers as a vector object.

```c++
#include <vector>
using namespace std;

vector<int> trouble(vector<int> ints) {
    int done = false;
    while (done == false) {
     done = true;
     for (int i = 0; i < (ints.size() - 2); i++){
      if (ints[i] > ints[i + 2]) {
       done = false;
       int v = ints[i];
       ints[i] = ints[i + 2];
       ints[i + 2] = v;
      }
     } 
    }
    return ints;
}
```

## Solution to Test Set 1

Given that `3 ≤ N ≤ 100`, the following solution did not exceed the time limit.

```c++
#include <iostream>
using namespace std;

int main()
{
    int t;
    cin >> t;
    
    for (int i = 0; i < t; ++i) {
        int result = -1;
        int n;
        cin >> n;
        vector<int> ns (n);   
        
        for (int j = 0; j < n; ++j) {
            int x;
            cin >> x;
            ns[j] = x;
        }
        
        vector<int> ns1 = trouble(ns);
        
        for (int k = 0; k < (ns1.size() - 1); ++k) {
            if (ns1[k] >  ns1[k + 1]) {
                result = k;
                cout << "Case #" << (i + 1) << ": " << result << endl;
                break;
            }
        }
        
        if (result == -1) {cout << "Case #" << (i + 1) << ": OK" << endl;}
    }
    return 0;
}
```

## Solution to Test Set 2

```c++
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    int t;
    cin >> t;
    
    for (int i = 0; i < t; ++i) {
        int result = -1;
        int n;
        cin >> n;
        vector<int> ns (n);   
        
        for (int j = 0; j < n; ++j) {
            int x;
            cin >> x;
            ns[j] = x;
        }
        
        if (result == -1) {cout << "Case #" << (i + 1) << ": OK" << endl;}
    }
    return 0;
}
```
