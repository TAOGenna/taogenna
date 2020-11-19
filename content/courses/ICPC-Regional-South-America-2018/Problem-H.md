---
title: H-Highway Decomposition
linktitle: H
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  ICPC-Regional-South-America-2018:
    parent: Problems and Solution
    weight: 8

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---
The problem can be solved with a little modification of the Dijkstra Algorithm in order to consider the minimun among all possibe paths leading to a shortest path.
Each time that we have to update a path to make the distance shorter we also have to build a new set of *cost values* for all paths arriving at that node with same shortest path distance.
Let's call 
$$edges[node]=\text{set of costs arriving with the same shortest path value at node}$$

So now all we have to compute is:
$$
wyn=\sum_{node=1}^{n}min \{ edges[node] \}
$$
Which is the answer we were looking for.
$\{ x+y \}$
<details><summary>code</summary>

```cpp
#include <bits/stdc++.h>
using namespace std;

#define rep(i, a, b) for(lli i = a; i < (b); ++i)
typedef long long int lli;

const lli N=1e4+10,INF=1e15;
lli dis[N];
vector<tuple<lli,lli,lli> > g[N]; //g[a] -> pair(b,w,c) 
bool processed[N];
vector<int> edges[N];

int main(){

	lli n,m; cin>>n>>m;
	rep(i,0,m){
		lli a,b,l,c; cin>>a>>b>>l>>c;
		g[a].pb(make_tuple(b,l,c));
		g[b].pb(make_tuple(a,l,c));
	}

	priority_queue<pair<lli,lli>> q; //contains pairs of form (-d,x)

	for (lli i = 1; i <= n; i++) {
	  	dis[i] = INF;
	}
	
	lli x=1,wyn=0;
	dis[x] = 0;//,C[x]=0;
	q.push({0,x});

	while (!q.empty()) {
		lli a = q.top().second; q.pop();
		if (processed[a]) continue;
		processed[a] = true;
		for (auto u : g[a]) {
			lli b,w,cost;
		  	tie(b,w,cost)=u;
		   	if(dis[a]+w < dis[b]){
			   	dis[b] = dis[a]+w;
		      	q.push({-dis[b],b});
		      	edges[b].clear();
		    }
		    if(dis[a]+w==dis[b]) edges[b].pb(cost);
		}
	}
	rep(i,1,n+1){
		sort(all(edges[i]));
		if(sz(edges[i]))wyn+=edges[i][0];
	}
	cout<<wyn<<endl;
	return 0;
}
```
</details>
 
