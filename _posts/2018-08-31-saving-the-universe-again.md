---
layout: post
title:  "Saving The Universe Again - An Amateur Solution"
date:   2018-08-31 09:30:00 +0800
tags: [c++, google code jam, competitive programming]
published: true
---

This is the first time I'm writing a C++ code (or program or whatever). I decided I would learn a new langauge for the Google Code Jam and I'm going to do that by just attempting the previous years' questions. This is the working solution for 'Saving The Universe Again' - the 2018 Qualifying Round Qustion A for the Google Code Jam. It did not exceed the memory or time limit.

```c++
#include <iostream>
#include <string>
#include <cstring>
using namespace std;


int impact(char program[]) {
    int power = 1;
    int imp = 0;
    for (int i = 0; i < strlen(program); i++) {
        if (program[i] == 'S') {
            imp += power;
        }
        if (program[i] == 'C') {
            power = power * 2;
        }
    }
    return imp;
}

int main()
{
    int t, n;
    string c;
    cin >> t;
    
    for (int i = 1; i <= t; ++i) {
        cin >> n >> c;
        auto result = 0;
        
        char * c0 = new char [c.length()+1];
        strcpy (c0, c.c_str());
        
        int im = impact(c0);
        
        while (im > n) {
           int p = c.rfind("CS");
           if (p == -1) {
               result = -1;
               cout << "Case #" << i << ": IMPOSSIBLE" << endl;
               break;
           }
           c.replace(p, 2, "SC");
        
           char * c0 = new char [c.length()+1];
           strcpy (c0, c.c_str());
           
           im = impact(c0);
           result++;
        }
        
        if (result != -1) {cout << "Case #" << i << ": " << result << endl;}
    }
    return 0;
}
```
