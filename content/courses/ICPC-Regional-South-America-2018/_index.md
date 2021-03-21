---
title: "ICPC Regional South America 2018"  # Add a page title.
summary: "My solutions for the ICPC Regional South America held on november of 2018"  # Add a page description.
date: "2019-01-01T00:00:00Z"  # Add today's date.
type: "widget_page"  # Page type is a Widget Page
---

This was the first regional in which I took part so being able to solve it now with more knowledge makes it worthy.<br>
<br>
As a whole by now I was just able to solve 9 problems, not bad, but the best team of the region accomplish 10 problems which is a huge amount of problems for the 5 hours.
Aside that, I think that the explanation of why the preformance of Peru was so poor on the ICPC World Finals is because seven problems of the wholse set were, if not directly, not so difficult. So, it's not surprise that a team going to the WF is going to perform badly if they were just able to solve the easiest problems during contest.<br>
<br>
Anyway, on the menu you fan find my solutions to the problems:<br>
<br>
[Problems Judge Links and Discussion :](https://codeforces.com/blog/entry/63157)<br>
<br>


## [A — A Symmetrical Pizza](https://www.urionlinejudge.com.br/judge/es/problems/view/2903)
The way I found the solution for this problem was through playing with the input. It's no hard tho to arrive to the following relation:
$$
Answer=\frac{mcm(R,360)}{R}\\
or \\
Answer=\frac{360}{gcd(R,360)}
$$
Maybe the hard thing to realise is that you have to make a parsing on the input in order to get the correct solution.
<details><summary>code</summary>

```cpp
lli mcm(lli a,lli b){
	return (a*b)/__gcd(a,b);
}
int main(){
    string s;
    cin>>s;
    int ind=0;
    rep(i,0,sz(s)) if(s[i]=='.') ind=i;

    vector<int> v1,v2;
    rep(i,0,ind) v1.pb(s[i]-'0');
    rep(i,ind+1,sz(s)) v2.pb(s[i]-'0');

    lli num=0;
    if(sz(v1)==3) num+=v1[0]*10000+v1[1]*1000+v1[2]*100+v2[0]*10+v2[1];
    else if(sz(v1)==2) num+=v1[0]*1000+v1[1]*100+v2[0]*10+v2[1];
    else num+=v1[0]*100+v2[0]*10+v2[1];

  	cout<<(mcm(num,36000)/num)<<endl;
    return 0;
}
```
</details>

## [B — Building a Field](https://www.urionlinejudge.com.br/judge/es/problems/view/2904)
First of all let's stablish some notation:
- $i^{th}$ arc differece: $v[i]=$ $i^{th}$
- The arc of the $i^{th}$ point: $sum[p]=\sum_{i=1}^m v[i]$

Let $A$,$B$,$C$,$D$ be the points given in counterclockwise order of any existing rectangle incribed in the circunference. We know that $A-C$ and $B-D$, segment formed by opposite corners, are both diameters.<br>
<br>
If we are in the $j^{th}$ point and $S=sum[n]=\sum_{i=1}^n arc[i]$, then if that position form a diameter with other point in the circunfernce we say that $\exists$ an index $k$ such that $sum[k]=(sum[i]+\frac{S}{2})\mod sum[n]$. With this observation what is left is to find two different points that generate a diameter.<br>
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

## [C — Cheap Trips](https://www.urionlinejudge.com.br/judge/es/problems/view/2905)
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

## [D — Database of Clients](https://www.urionlinejudge.com.br/judge/es/problems/view/2906)
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

## [E — Escape, Polygon!](https://www.urionlinejudge.com.br/judge/es/problems/view/2907)
he key observation for this problem is that there's an entire region where is impossible to construct a closed triangle.

Let's get more precise about this "region" and how can we find it.<br>
{{< figure library="true" src="EscapePolygon.jpg" title="Example" >}} 

For a fixed side, the region is limited by the gray segment, any two lines drew inside this region won't form a closed triangle. In the example above is easy to see that those red lines won't generate a triangle.

Now, when do we know we have reached the other side of the gray segment? Consider the consecutive edges after that one(green), and continue until the angle with respect to the horizontal(current edge/green) has increased by $180°$. 

Said that, we can see that we can compute the result by complement. This is, calculating the "bad ones" that doesn't contrubute nothing to the result and then taking the difference with the number of all possible triplets.

- The total number of triplets is just
$$
{n\choose 3} = \frac{(n)(n-1)(n-3)}{6}
$$
- The endpoint of the gray line can be calulated by a little trick involving the cross product which basically can tell us if a point is either on the right or on the left side of a line
{{< figure library="true" src="CrossProd.jpg" title="Interpretation" >}}

So, when do we know we have reached $180°$? When the cross product is no longer $\geq 0$. Repeating this process for all the edges we'll find the answer.

- Let $cnt[i] = $ number of edges between the $i^{th}$ edge and its corresponding endpoint of the gray line<br/>

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

## [F — Fantastic Beasts](https://www.urionlinejudge.com.br/judge/es/problems/view/2908)
<details><summary>code</summary>

```cpp
```
</details>

## [G — Gathering Red-Black Fruits](https://www.urionlinejudge.com.br/judge/es/problems/view/2909)
<details><summary>code</summary>

```cpp
```
</details>

## [H — Highway Decommission](https://www.urionlinejudge.com.br/judge/es/problems/view/2910)
The problem can be solved with a little modification of the Dijkstra Algorithm in order to consider the minimun among all possibe paths leading to a shortest path.
Each time that we have to update a path to make the distance shorter we also have to build a new set of *cost values* for all paths arriving at that node with same shortest path distance.
Let's call 
$$edges[node]=\text{set of costs arriving with the same shortest path value at node}$$

So now all we have to compute is:
$$
wyn=\sum_{node=1}^{n}min( edges[node])
$$
Which is the answer we were looking for.
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

## [I — Ink Colors](https://www.urionlinejudge.com.br/judge/es/problems/view/2911)
The problem can be solved with a greedy approach. It reaches the maximun amount they ask for ifwe assume that by filling our tree with "stick men" from the bottom of the tree to the root. Now to keep things simple, the idea to solve the problem is not to explicitly draw the stick man in our tree if we find one, but rather to play with the degree of each node. Since we go from the leaves to the root, we only have to worry about the node that acts as the head of the stick man decreasing its degree by one if we find a stick man made with it.
Notice the following:
- The chest of the stick man is made up of two nodes, the top node has three edges and the bottom node has two edges. This is:
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

## [J — Jeopardized Election](https://www.urionlinejudge.com.br/judge/es/problems/view/2912)
<details><summary>code</summary>

```cpp
```
</details>

## [K — KryptoLocker Ate my Homework](https://www.urionlinejudge.com.br/judge/es/problems/view/2913)
<details><summary>code</summary>

```cpp
```
</details>

## [L — Looking for the Risk Factor](https://www.urionlinejudge.com.br/judge/es/problems/view/2914)
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

## [M — Mount Marathon](https://www.urionlinejudge.com.br/judge/es/problems/view/2915)
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
