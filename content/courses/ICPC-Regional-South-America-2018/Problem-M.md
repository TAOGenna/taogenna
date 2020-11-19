---
title: M-Mount Marathon
linktitle: M
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  ICPC-Regional-South-America-2018:
    parent: Problems and Solution
    weight: 13

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---
This also was one of the easiest problems. Just push eveything to the right following the condition of the problem.
<details><summary>code</summary>

```cpp
#include <bits/stdc++.h>
using namespace std;

#define rep(i, a, b) for(lli i = a; i < (b); ++i)
typedef long long int lli;
 
int main(){
	int n; cin>>n;
	vi v(n);
	rep(i,0,n) cin>>v[i];

	for(int i=n-1;i>=0;i--){
		for(int j=i+1;j<n;j++){
			if(v[j]){
				if(v[i]>=v[j]){
					v[j]=v[i];
					v[i]=0;
				}
				break;
			}
		}
	}
	int wyn=0;
	for(int i=0;i<n;i++) if(v[i]){
		wyn++;
	} 
	cout<<wyn<<endl;
	return 0;
}
```
</details>
