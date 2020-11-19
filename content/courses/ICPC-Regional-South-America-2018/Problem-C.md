---
title: C-Cheap Trips
linktitle: C
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  ICPC-Regional-South-America-2018:
    parent: Problems and Solution
    weight: 3

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

This problem can be solved by dynamic programming. Let's break it down in three parts.
Let's define $dp[i]=\text{the solution for the problem for position }i$
- Current element as a new sequence : $dp[i]=dp[i-1]+c[i]$ and $dur=d[i]$
- Update the following number as if it were the second element of the sequence if $dur[i]<120$ : $dp[i+1]=dp[i-1]+c[i]+0.5\times c[i+1]$
- Complete the reamining four trips with discount $0.25%$ until the condition of the time interval break
<br>
<details><summary>code</summary>

```cpp
#include <bits/stdc++.h>

using namespace std;

typedef long long ll;
const ll MAX = 1e6 + 5;

vector <ll> lista[MAX];

int n, d[MAX];
double dp[MAX], c[MAX];

int main() {
    ios_base::sync_with_stdio(0);
    cin.tie(0);

    cin >> n;

    for(int i = 1; i <= n; i++)
        cin >> d[i] >> c[i], dp[i] = 1e15;

    for(int i = 1; i <= n; i++) {
        dp[i] = min(dp[i], dp[i - 1] + c[i]);
        int dur = d[i];
        if(dur < 120)
            dp[i + 1] = min(dp[i + 1], dp[i - 1] + c[i] + 0.5 * c[i + 1]);
        double s = 0;
        for(int j = 1; j <= 4; j++) {
            dur += d[j + i];
            s += c[i + j + 1];
            if(dur < 120)
                dp[i + j + 1] = min(dp[i + j + 1], dp[i - 1] + c[i] + 0.5 * c[i + 1] + 0.25 * s);
        }
    }

    cout << setprecision(2) << fixed;
    cout << dp[n] << '\n';
}
```
</details>
