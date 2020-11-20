---
title: I-Ink Colors
linktitle: I
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  ICPC-Regional-South-America-2018:
    parent: Problems and Solution
    weight: 9

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---
The problem can be solved with a greedy approach. It reaches the maximun amount they ask for ifwe assume that by filling our tree with "stick men" from the bottom of the tree to the root. Now to keep things simple, the idea to solve the problem is not to explicitly draw the stick man in our tree if we find one, but rather to play with the degree of each node. Since we go from the leaves to the root, we only have to worry about the node that acts as the head of the stick man decreasing its degree by one if we find a stick man made with it.
Notice the following:
- the chest of the stick man is made up of two nodes, the top node has three edges and the bottom node has two edges. This is:
```cpp
if(degree[upper_node]>=3 and degree[bottom_node]>=2){...}
```
- We need to ensure that there's a edge that acts as the head. This is(where s is just set containing identifiers for each edge based on {depth,node}):
```cpp
if(uppder_node!=1 and s.find({..})!=s.end()){...}
```
<details><summary>code</summary>

```cpp

#include <bits/stdc++.h>
using namespace std;

#define rep(i, a, b) for(lli i = a; i < (b); ++i)
typedef long long int lli;

const int N=1e5+10;
vector<int> g[N];
int level[N],P[N],deg[N];

void dfs(int node,int fat,int de){
	level[node]=de;
	for(auto x : g[node]) if(x!=fat) dfs(x,node,de+1); 
}


int main(){

	int n; cin>>n;

	P[1]=-1;
	for(int i=2;i<=n;i++){
		cin>>P[i];
		deg[P[i]]++;
		g[P[i]].pb(i),g[i].pb(P[i]);
	}
	dfs(1,-1,0);
	set<pair<int,int> > s;
	rep(i,1,n+1) s.insert({-level[i],i});
	int wyn=0;
	while(sz(s)){
		auto x=*s.begin();
		s.erase(s.begin());
		int upper_body=P[x.ss],lower_body=x.ss;
		pair<int,int> aux={-level[upper_body],upper_body};
		if(deg[upper_body]>=3 and deg[lower_body]>=2 and upper_body!=1 and  s.find(aux) != s.end()){
			deg[P[upper_body]]--;
			s.erase(aux);
			wyn++;
		}
	}
	cout<<wyn<<endl;
	return 0;
}
```
</details>
