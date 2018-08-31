---
layout: post
title:  "Trouble Sort - Code Jam Solution"
date:   2018-08-31 16:30:00 +0800
tags: [c++, google code jam]
published: false
---

```c++
#include <iostream>
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
