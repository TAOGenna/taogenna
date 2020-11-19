---
title: E-Escape, Polygon!
linktitle: E
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  ICPC-Regional-South-America-2018:
    parent: Problems and Solution
    weight: 5

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---
The key observation for this problem is that there's an entire region where is impossible to construct a closed triangle.

Let's get more precise about this "region" and how can we find it.<br>
{{< figure library="true" src="EscapePolygon.jpg" title="Example" >}} 

For a fixed side, the region is limited by the gray segment, any two lines drew inside this region won't form a closed triangle. In the example above is easy to see that those red lines won't generate a triangle.

Now, when do we know we have reached the other side of the gray segment? Consider the consecutive edges after that one(green), and continue until the angle with respect to the horizontal(current edge/green) has increased by $180°$. 

Said that, we can see that we can compute the result by complement. This is, calculating the "bad ones" that doesn't contrubute nothing to the result and then taking the difference with the number of all possible triplets.

- The total number of triplets is just ${n\choose 3} = \frac{(n)(n-1)(n-3)}{6}$
- The endpoint of the gray line can be calulated by a little trick involving the cross product which basically can tell us if a point is either on the right or on the left side of a line
{{< figure library="true" src="CrossProd.jpg" title="Interpretation" >}}
So, when do we know we have reached $180°$? When the cross product is no longer $\geq 0$. Repeating this process for all the edges we'll find the answer.

- Let $cnt[i] = $ number of edges between the $i^{th}$ edge and its corresponding endpoint of the gray line
Then:
$$
Answer = {n\choose 3}-\sum_{i=1}^n{cnt[i]\choose 2}
$$
<details><summary>code</summary>

```cpp
#include <bits/stdc++.h>
using namespace std;

#define rep(i, a, b) for(lli i = a; i < (b); ++i)
typedef long long int lli;

int cmp(lli x, lli y = 0) { return (x <= y) ? (x < y) ? -1 : 0 : 1; }
struct point {
  lli x, y;
  point() : x(0), y(0) {}
  point(lli X, lli Y) : x(X), y(Y) {}
  point operator-(point a) { return point(x - a.x, y - a.y); }
  lli operator%(point a) { return x * a.y - y * a.x; }
};
int ccw(point a, point b, point c) { return cmp((b - a) % (c - a)); }

const int N=1e5+10;
lli n; 
point poly[N];

int main(){
	cin>>n;
	rep(i,0,n) cin>>poly[i].x>>poly[i].y;
	const auto edge=[](int p){return poly[(p+1)%n]-poly[p%n];};
	lli wyn=((n)*(n-1)*(n-2))/6;
	for(lli i=0,j=1;i<n;i++){
		point pi=edge(i),pj=edge(j);
		while(ccw({},pi,pj)>=0) pj=edge(++j);
		wyn-=((j-i-1)*(j-i-2))/2;
	}
	cout<<wyn<<endl;
	return 0;
}
```
</details>



  
