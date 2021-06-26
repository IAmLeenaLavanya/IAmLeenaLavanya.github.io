---
layout: post
title:  "Does the Ball Bounce into the Hole? - CodeChef May Long Challenge 2021 Division 3 LKDNGOLF"
date:   2021-06-26 12:00:00 +0800
tags: [c++, competitive programming, codechef]
published: true
---

We have a floor, with an `N + 2` number of tiles. The tiles are ordered 0 to `N + 1` and a there's a hole at tile number x. We introduce a ball that bounces at a steady rate of k tiles, starting from 0 and then moving to k, 2k, 3k etc. Once the ball reaches the end of the floor, it bounces back in the opposite direction, starting from `N + 1`, moving to `N + 1 - k, N + 1 - 2k` etc.

Now the question, does it fall in? We check if x is a multiple of k or if `N + 1 - x` (x's location if we start bouncing from the opposite direction) is a multiple of k. If either of them are true, then the ball falls in.

```c++
#include <iostream>

using namespace std;

int main() {
    int t, i, n, x, k;
    cin >> t;
    for (i = 0; i < t; i++) {
        cin >> n >> x >> k;
        cout << (x % k == 0 || (n + 1 - x) % k == 0 ? "YES" : "NO") << endl;
    }
    return 0;
}
```

