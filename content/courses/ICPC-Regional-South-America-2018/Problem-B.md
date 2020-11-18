---
title: B-Building a Field
linktitle: B
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  ICPC-Regional-South-America-2018:
    parent: Problems and Solution
    weight: 1

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---
This problem can be approach in many ways, some more complicated than others. But the easiest way is given by the following observation: Let $A$,$B$,$C$,$D$ be a rectangle incribed in the circunference and be $acum[p]$ the sum acumulation of the arcs till position $p$, this is $acum[p]=\sum_{i=1}^{p} arc[i]$. We know that $A-B$ and $C-D$, segment formed by opposite corners, are both diameters. What I mean by this is that if we are in the position $j$ of the given arcs and $S=\sum_{i=1}^n arc[i]$ then if that position form a diameter with other point in the circunfernce, that point must be in $acum[i]+\frac{S}{2}$. With this observation what is left is to find two different points that generate a diameter.<br>
<details><summary>code</summary>

```cpp
#include <bits/stdc++.h>
using namespace std;

#define rep(i, a, b) for(lli i = a; i < (b); ++i)
typedef long long int lli;

map<lli,lli> m;
set<lli> s;
int main(){
	lli n,total=0; cin>>n;
	vi v(n+10),sum(n+10);
	rep(i,1,n+1){
		cin>>v[i];
		total+=v[i];
		sum[i]=v[i]+sum[i-1];
		m[sum[i]]++;
	}

	if(total%2!=0){
		cout<<"N"<<endl;
		return 0;
	}

	int cnt=0;

	rep(i,1,n+1){
		lli num=(sum[i]+total/2)%total;
		if(!s.count(num) and m[num]){
			s.insert(num);
			s.insert(sum[i]);
			cnt++;
		}
	}

	if(cnt>=2) cout<<"Y"<<endl;
	else cout<<"N"<<endl;

	return 0;
}
```
</details>
 
