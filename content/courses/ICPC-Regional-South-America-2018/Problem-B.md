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

figcaption {
  text-align: center;
}

First of all let's stablish some notation:
- $i^{th}$ arc differece: $v[i]=$ $i^{th}$
- The arc of the $i^{th}$ point: $sum[p]=\sum_{i=1}^m v[i]$

Let $A$,$B$,$C$,$D$ be the points given in counterclockwise order of any existing rectangle incribed in the circunference. We know that $A-C$ and $B-D$, segment formed by opposite corners, are both diameters.<br>
<br>
If we are in the $j^{th}$ point and $S=sum[n]=\sum_{i=1}^n arc[i]$, then if that position form a diameter with other point in the circunfernce we say that $\exists \text{ an index } k \text{ such that } sum[k]=(sum[i]+\frac{S}{2})\mod sum[n]$. With this observation what is left is to find two different points that generate a diameter.<br>
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
 
