---
layout: post
title:  "Code Chef February Challenge Div. 2 2019 - Appy and Contest"
date:   2018-10-18 11:50:00 +0800
tags: [c++, competitive programming, codechef, math]
published: false
---

Problem HMAPPY2 in the February Challenge 2019 Code Chef (Division 2) .

Given the below constraints, the program can loop through all integers from 1 to N, counting the number of integers that are either divisible by A and not B or B and not A.

* 1 ≤ T ≤ 15
* 1 ≤ K ≤ N ≤ 10^6
* 1 ≤ A, B ≤ 10^3

```c++
#include <iostream>
using namespace std;

int main() {
	int t, n, a, b, k, i, r; cin >> t;
	while (t--) {
	    r = 0; cin >> n >> a >> b >> k;
	    for (i = 1; i <= n; i++) if ((i % a == 0 && i % b != 0) || (i % b == 0 && i % a != 0)) r++;
	    cout << ((r >= k) ? "Win" : "Lose") << endl;
	}
	return 0;
}
```

A larger set of constraints disallows us from iterating through each integer. Instead, using the Euclidean algorithm we find the greatest common difference of A and B and divide (A x B) by it to find the lowest common multiple of the two integers. With the lowest common multiple are able to calculate the number of integers between 1 and N that are divisible by *both* A and B and subtract this from the number of integers divisible by A and the number of integers divisible by B.

* 1 ≤ T ≤ 15
* 1 ≤ K ≤ N ≤ 10^18
* 1 ≤ A, B ≤ 10^9

```c++
#include <iostream>
using namespace std;

int main() {
	int t; cin >> t;
	unsigned long long n, a, b, k, lcm;
	while (t--) {
	    cin >> n >> a >> b >> k;
	    unsigned long long q = ((a > b) ? b : a), r = ((a > b) ? a : b), i = 0;
	    while (r != 0) i = q % r, q = r, r = i;
	    lcm = (a * b) / q;
	    cout << ((((n / a) + (n / b) - ((n / lcm) * 2)) >= k) ? "Win" : "Lose") << endl;
	}
	return 0;
}
```
