---
layout: post
title:  "Trouble Sort Solution - 2nd Try at Google Code Jam"
date:   2018-08-31 16:30:00 +0800
tags: [c++, google code jam]
published: true
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

For the second test set `3 ≤ N ≤ 10^5` so `trouble()` takes way too much time. Here's a faster solution:

```c++
#include <iostream>
#include <vector>
#include <math.h>
#include <algorithm> 
using namespace std;

int main()
{
    int t;
    cin >> t;
    
    for (int i = 0; i < t; ++i) {
        double n;
        int result = -1;
        cin >> n;
        vector<int> no (ceil(n / 2)); // Index of odd numbers
        vector<int> ne (floor(n / 2)); // Index of even numbers
        
        for (int j = 0; j < n; j+=2) {
            cin >> no[j/2];
            if(j < (n-1)) cin >> ne[j/2];
        }
        
        sort(no.begin(), no.end());
        sort(ne.begin(), ne.end()); // Sort them
        
        vector<int> noe (n); // Mix both even and odd numbers again
        
        for (int k = 0; k < n; k++) {
            if (k % 2 == 0) noe[k] = no[k/2];
            else noe[k] = ne[k/2];
        }
        
        for (int m = 0; m < (noe.size() - 1); ++m) { // Same as above
            if (noe[m] >  noe[m + 1]) {
                result = m;
                break;
            }
        }
        
        if (result == -1) cout << "Case #" << (i + 1) << ": OK" << endl;
        else cout << "Case #" << (i + 1) << ": " << result << endl;
    }
    return 0;
}
```
