---
layout: post
title:  "Waffle Choppers - Test Set 1 Solution for Google Code Jam 2018"
date:   2018-10-04 11:50:00 +0800
tags: [c++, google code jam, competitive programming]
published: true
---

The Small Test Set for Round 1A Google Code Jam 2018 required that given an `n` number of test cases (each containing information on the number of rows and columns of a waffle (waffle squares?) and whether or not each waffle square has a chocolate chip) one should determine whether any combination of one vertical slice and one horizontal slice can result in four pieces with exactly the same number of chocolate chips.

Given that the maximum number of possible horizontal and vertical cuts combinations is `(9 - 1) x (9 - 1) = 81`, one possible solution was to identify all the possible combinations and see how many chocolate chips each slice would get. If in any combination, the number of chocolate chips in all four slices are the same, then the case is POSSIBLE.

```c++
#include <iostream>
#include <string>
#include <vector>
using namespace std;

int main()
{
  int n; cin >> n;
  
  for (int i = 1; i <= n; i++) {
      int row, col, h_cut, v_cut;
      cin >> row >> col >> h_cut >> v_cut;
      
      string r = "IMPOSSIBLE";
      vector<vector<int>> qs(row, vector<int> (col));
      
      for (int i_n = 0; i_n < row; i_n++) {
        string q; cin >> q;
        for(int i_q = 0; i_q < q.size(); i_q++) qs[i_n][i_q] = q[i_q];
      }
      
      for (int i_r = 0; i_r < (row - 1); i_r++) {
          for (int i_c = 0; i_c < (col - 1); i_c++) {
              if (cookie(row, col, i_c, i_r, qs) == true) r = "POSSIBLE"; break;
          }
      }
      
      cout << "CASE #" << i << ": " << r << endl;
  }
}
```

We need to check whether given a horizontal cut and a vertical cut, each of the four resultant waffle pieces have an equal number of chocolate chips. This can be done by the function below (I am aware that a function counting chocolate chips should not be named cookie - but I seemed to have gotten that mixed up):

```c++
bool cookie(int row, int col, int i_c, int i_r, vector<vector<int>> waffle) 
{
    vector<int> cookies (4, 0);
    for (int i_v = 0; i_v < row; i_v++) {
        for (int i_h = 0; i_h < col; i_h++) {
            if (waffle[i_v][i_h] == 64) {
                if (i_v <= i_r && i_h <= i_c) cookies[1]++;
                else if (i_v <= i_r && i_h > i_c) cookies[2]++;
                else if (i_v > i_r && i_h <= i_c) cookies[3]++;
                else cookies[4]++;
            }
        }
    }
    if (cookies[1] == cookies[2] && cookies[2] == cookies[3] && cookies[3] == cookies[4]) return true;
    else return false;
}
```
