---
layout: post
title:  "Solution for SnackDown 2019: Qualifying to Pre-Elimination"
date:   2018-10-18 11:50:00 +0800
tags: [c++, competitive programming, codechef]
published: true
---

Problem QUALPREL in the Online Qualifiers of the Code Chef SnackDown 2019 required that given a `N` number of scores `S` and an integer `K`, one should output the number the number of scores that are higher than or equal to the `Kth` highest score.

```c++
#include <iostream>
#include <algorithm> 
#include <vector>
using namespace std;

bool sort_t (int i,int j) {return (i>j);}

int main() {
	int n;
	cin >> n;
	
	for (int i = 1; i <= n; i++) {
	    int n_t, qual;
	    cin >> n_t >> qual;
	    
	    vector<int> scores(n_t);
	    
	    for (int i_n = 0; i_n < n_t; i_n++) {
	        int score; 
	        cin >> score; 
	        scores[i_n] = score;
	    }
	    
	    sort (scores.begin(), scores.end(), sort_t);
	    
	    int s = qual;
	    
	    for (int i_q = qual; i_q < n_t; i_q++) {
	        if (scores[i_q] == scores[qual - 1]) s++;
	        else break;
	    }
	    
	    cout << s << endl;
    }
	
	return 0;
}
```
