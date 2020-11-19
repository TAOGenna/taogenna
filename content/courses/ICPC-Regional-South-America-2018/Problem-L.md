---
title: L-Looking for the Risk Factor
linktitle: L
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  ICPC-Regional-South-America-2018:
    parent: Problems and Solution
    weight: 12

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---
Consider that for each numer $x$ we have saved all the queries which take place there(query of the form $(x,k)$). Now since we a re interested in knowing the asnwer for all numbers $\leq x$ it just don't have any sense to be worried about the values $\geq x$. With that in mind we can update on the way what is the greatest prime divisor for number/position $x$.

| Number | Max Prime Divisor |
|--------|-------------------|
| 10 | 5 |
| 11 | 11|
|12  | 3 |
| 13 | 13|
| 14 | 7 |
| 15 | 5 |
| x | ? |
| ... | ... |

Once we have reached position $x$ we have to make an update because $k\geq x$. Now, here comes the real solution:
- Construct a segment tree from $1$ to $N=10^5$
- Each time we update the max prime divisor for a number $x$ we also update the occurrence of that prime number on our segment tree. That is, if we are on position $x=18$ the $st[5]=3$ because we have passed already for $5,10,15$.
- To answer a query we have to make a sum over range from $[2,n]$ on our ST
- Obviously we have to asnwer the queries in a offline mode
<details><summary>code</summary>

```cpp
#include <bits/stdc++.h>
using namespace std;

#define rep(i, a, b) for(lli i = a; i < (b); ++i)
typedef long long int lli;

const int N=1e5+10;
int st[2*N],lar[N],wyn[N];
vector<pair<int,int> > quer[N];

int get(int n) {
  int maxi=0;
  for (int x = 2; x*x <= n; x++) {
    while (n%x == 0) {
      maxi=max(x,maxi);//push_back(x);
      n /= x;
    }
  }
  if (n > 1) maxi=max(maxi,n);//f.push_back(n);
  return maxi;
}

void update(int pos,int val){
	pos=pos+N-1;
	st[pos]+=val;
	for(pos/=2;pos>=1;pos/=2){
		st[pos]=st[pos<<1]+st[pos<<1|1];
	}
}

int query(int a,int b){
	a+=N-1,b+=N-1;
	int sum=0;
	while(a<=b){
		if(a%2==1) sum+=st[a++];
		if(b%2==0) sum+=st[b--];
		a/=2,b/=2;
	}
	return sum;
}

int main(){
	int q; //cin>>q;
	scanf("%d\n",&q);
	rep(i,0,q){
		int a,b;scanf("%d %d\n",&a,&b);// cin>>a>>b;
		quer[a].pb({min(a,b),i});
	}

	rep(i,0,N){
		lar[i]=get(i);
	}

	rep(i,2,N){
		update(lar[i],1);
		for(auto x : quer[i]){
			wyn[x.ss]=query(0,x.ff);
		}
	}
	rep(i,0,q) printf("%d\n",wyn[i]);
	return 0;
}
```
</details> 

