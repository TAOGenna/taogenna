---
title: D-Database of Clients
linktitle: D
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  ICPC-Regional-South-America-2018:
    parent: Problems and Solution
    weight: 4

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---
There's not much to say about this problem. Probably the easiest one
<details><summary>code</summary>

```cpp
#include <bits/stdc++.h>
using namespace std;

#define rep(i, a, b) for(lli i = a; i < (b); ++i)
typedef long long int lli;
set<string> ss;

int main(){

	int n; cin>>n;
	rep(i,0,n){
		string s; cin>>s;
		int arroba=-1,simbolo=-1;
		rep(j,0,sz(s)) if(s[j]=='@'){arroba=j;break;}
		rep(j,0,sz(s)) if(s[j]=='+'){simbolo=j;break;}
		string wyn;
		if(simbolo==-1) simbolo=arroba;
		rep(j,0,min(arroba,simbolo)) if(s[j]!='.')wyn+=s[j];
		rep(j,arroba,sz(s)) wyn+=s[j];
		ss.insert(wyn);
	}
	cout<<sz(ss)<<endl;
	return 0;
}
```
</details>
