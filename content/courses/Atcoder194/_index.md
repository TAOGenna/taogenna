---
title: "AtCoder Beginner Contest 194"  # Add a page title.
summary: "March 20, 2021"  # Add a page description.
date: "2021-03-20T00:00:00Z"  # Add today's date.
type: "widget_page"  # Page type is a Widget Page
---

Contest Link: [AtCoder Beginner Contest 194](https://atcoder.jp/contests/abc194) <br>

## [pA: I Scream](https://atcoder.jp/contests/abc194/tasks/abc194_a)
<details><summary>code</summary>

```cpp
#pragma GCC optimize ("Ofast")
#pragma GCC target ("avx,avx2")
#pragma GCC optimize ("trapv")
 
 
#include <bits/stdc++.h>
using namespace std;
 
#define fastio ios_base::sync_with_stdio(0); cin.tie(0); cin.exceptions(cin.failbit);
#define rep(i, a, b) for(lli i = a; i < (b); ++i)
#define ff first
#define ss second
#define pb push_back
#define all(x) (x).begin(), (x).end()
#define sz(x) (int)(x).size()
#define wis cout<<endl<<"I already speak english, bitch"<<endl<<endl;
 
typedef long long int lli;
typedef vector<lli> vi;
typedef pair<lli,lli> ii;
typedef vector<ii> vii;
 
#define trace(args...) { string  _s =#args; replace(_s.begin(), _s.end(), ',',' '); stringstream _ss(_s); istream_iterator<string> _it(_ss); err(_it, args);}
void err(istream_iterator<string> it){}
template<typename T, typename... Args>
void err(istream_iterator<string> it, T a, Args... args){
    cout <<  *it  << " : " << a << endl;
    err(++it, args...);
}
 
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/trie_policy.hpp>
using namespace __gnu_pbds;
 
template <typename T, class compare>
using ordered_set = tree<T, null_type, compare, rb_tree_tag, tree_order_statistics_node_update>;
//usage: ordered_set< el tipo , el comparador> nombre;

int main(){
	int a,b; cin>>a>>b;
	int c=a+b;
	if(c>=15 and b>=8) cout<<1;
	else if(c>=10 and b>=3) cout<<2;
	else if(c>=3) cout<<3<<endl;
	else cout<<4;
	cout<<endl;
	return 0;
}

```
</details>

## [pB: Job Assignment](https://atcoder.jp/contests/abc194/tasks/abc194_b)
<details><summary>code</summary>

```cpp
#pragma GCC optimize ("Ofast")
#pragma GCC target ("avx,avx2")
#pragma GCC optimize ("trapv")
 
 
#include <bits/stdc++.h>
using namespace std;
 
#define fastio ios_base::sync_with_stdio(0); cin.tie(0); cin.exceptions(cin.failbit);
#define rep(i, a, b) for(lli i = a; i < (b); ++i)
#define ff first
#define ss second
#define pb push_back
#define all(x) (x).begin(), (x).end()
#define sz(x) (int)(x).size()
#define wis cout<<endl<<"I already speak english, bitch"<<endl<<endl;
 
typedef long long int lli;
typedef vector<lli> vi;
typedef pair<lli,lli> ii;
typedef vector<ii> vii;
 
#define trace(args...) { string  _s =#args; replace(_s.begin(), _s.end(), ',',' '); stringstream _ss(_s); istream_iterator<string> _it(_ss); err(_it, args);}
void err(istream_iterator<string> it){}
template<typename T, typename... Args>
void err(istream_iterator<string> it, T a, Args... args){
    cout <<  *it  << " : " << a << endl;
    err(++it, args...);
}
 
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/trie_policy.hpp>
using namespace __gnu_pbds;
 
template <typename T, class compare>
using ordered_set = tree<T, null_type, compare, rb_tree_tag, tree_order_statistics_node_update>;
//usage: ordered_set< el tipo , el comparador> nombre;


int main(){
	int n; cin>>n;
	vector<pair<int,int> > v;
	for(int i=0;i<n;i++){
		int a,b; cin>>a>>b;
		v.pb({a,b});
	}
	int wyn=1e9;
	for(int i=0;i<n;i++){
		for(int j=0;j<n;j++){
			if(i==j){
				wyn=min(wyn,v[i].ff+v[i].ss);
			}else{
				wyn=min(wyn,min(max(v[i].ff,v[j].ss),max(v[i].ss,v[j].ff)));
			}
		}
	}
	cout<<wyn<<endl;
}

```
</details>

## [pC: Squared Error](https://atcoder.jp/contests/abc194/tasks/abc194_c)
<details><summary>code</summary>

```cpp
#pragma GCC optimize ("Ofast")
#pragma GCC target ("avx,avx2")
#pragma GCC optimize ("trapv")
 
 
#include <bits/stdc++.h>
using namespace std;
 
#define fastio ios_base::sync_with_stdio(0); cin.tie(0); cin.exceptions(cin.failbit);
#define rep(i, a, b) for(lli i = a; i < (b); ++i)
#define ff first
#define ss second
#define pb push_back
#define all(x) (x).begin(), (x).end()
#define sz(x) (int)(x).size()
#define wis cout<<endl<<"I already speak english, bitch"<<endl<<endl;
 
typedef long long int lli;
typedef vector<lli> vi;
typedef pair<lli,lli> ii;
typedef vector<ii> vii;
 
#define trace(args...) { string  _s =#args; replace(_s.begin(), _s.end(), ',',' '); stringstream _ss(_s); istream_iterator<string> _it(_ss); err(_it, args);}
void err(istream_iterator<string> it){}
template<typename T, typename... Args>
void err(istream_iterator<string> it, T a, Args... args){
    cout <<  *it  << " : " << a << endl;
    err(++it, args...);
}
 
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/trie_policy.hpp>
using namespace __gnu_pbds;
 
template <typename T, class compare>
using ordered_set = tree<T, null_type, compare, rb_tree_tag, tree_order_statistics_node_update>;
//usage: ordered_set< el tipo , el comparador> nombre;

map<lli,lli> m;

int main(){
	int n; cin>>n;
	rep(i,0,n){
		lli foo; cin>>foo;
		m[foo]++;
	}
	lli wyn=0;
	for(auto &x : m){
		lli num1=x.ff,cant1=x.ss;
		for(auto &y : m){
			lli num2=y.ff,cant2=y.ss;
			wyn+=(num1*num1+num2*num2-2*num1*num2)*cant1*cant2;
		}
	}
	cout<<wyn/2<<endl;
	return 0;
}
	

```
</details>

## [pD: Journey](https://atcoder.jp/contests/abc194/tasks/abc194_d)
The equation to solve in expected values is:
$$
E[X_n]=\frac{N-(n-1)}{N}E[X_{n-1}+1] + \frac{n-1}{N}E[X_n+1]
$$
The reasoning behind the expression is as follows.(1) the first term correspond to the case in which in an operation we choose an unexplorared node, so we count an operation and the operation that we have made beforehand($E_{n+1}$).(2) the second term corresponds to the case in which we choose an already visited node, so we must try again. In both cases we must make an operation, that is why the $+1$.
<details><summary>code</summary>

```cpp
#pragma GCC optimize ("Ofast")
#pragma GCC target ("avx,avx2")
#pragma GCC optimize ("trapv")
 
 
#include <bits/stdc++.h>
using namespace std;
 
#define fastio ios_base::sync_with_stdio(0); cin.tie(0); cin.exceptions(cin.failbit);
#define rep(i, a, b) for(lli i = a; i < (b); ++i)
#define ff first
#define ss second
#define pb push_back
#define all(x) (x).begin(), (x).end()
#define sz(x) (int)(x).size()
#define wis cout<<endl<<"I already speak english, bitch"<<endl<<endl;
 
typedef long long int lli;
typedef vector<lli> vi;
typedef pair<lli,lli> ii;
typedef vector<ii> vii;
 
#define trace(args...) { string  _s =#args; replace(_s.begin(), _s.end(), ',',' '); stringstream _ss(_s); istream_iterator<string> _it(_ss); err(_it, args);}
void err(istream_iterator<string> it){}
template<typename T, typename... Args>
void err(istream_iterator<string> it, T a, Args... args){
    cout <<  *it  << " : " << a << endl;
    err(++it, args...);
}
 
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/trie_policy.hpp>
using namespace __gnu_pbds;
 
template <typename T, class compare>
using ordered_set = tree<T, null_type, compare, rb_tree_tag, tree_order_statistics_node_update>;
//usage: ordered_set< el tipo , el comparador> nombre;

int main(){
	int n; cin>>n;
	double wyn=0.0;
	for(int i=2;i<=n;i++){
		wyn=wyn+double(n)/(double(n)-double(i)+1.0);
	}
	cout<<fixed;
	cout<<setprecision(9);
	cout<<wyn<<endl;
}

```
</details>

## [pE: Mex Min](https://atcoder.jp/contests/abc194/tasks/abc194_e)
The problem can be easily solved by using a segment tree like update approach plus sliding window. The window will be of lenght $M$ and it will be running from left to right always making an update on the endpoints. If a value is no longer present we update the segment tree and check what is current $MEX$. On the other hand if a value is now present the segment tree is now updated such that it is no longer considered. 
<details><summary>code</summary>

```cpp
#pragma GCC optimize ("Ofast")
#pragma GCC target ("avx,avx2")
#pragma GCC optimize ("trapv")
 
 
#include <bits/stdc++.h>
using namespace std;
 
#define fastio ios_base::sync_with_stdio(0); cin.tie(0); cin.exceptions(cin.failbit);
#define rep(i, a, b) for(lli i = a; i < (b); ++i)
#define ff first
#define ss second
#define pb push_back
#define all(x) (x).begin(), (x).end()
#define sz(x) (int)(x).size()
#define wis cout<<endl<<"I already speak english, bitch"<<endl<<endl;
 
typedef long long int lli;
typedef vector<lli> vi;
typedef pair<lli,lli> ii;
typedef vector<ii> vii;
 
#define trace(args...) { string  _s =#args; replace(_s.begin(), _s.end(), ',',' '); stringstream _ss(_s); istream_iterator<string> _it(_ss); err(_it, args);}
void err(istream_iterator<string> it){}
template<typename T, typename... Args>
void err(istream_iterator<string> it, T a, Args... args){
    cout <<  *it  << " : " << a << endl;
    err(++it, args...);
}
 
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/trie_policy.hpp>
using namespace __gnu_pbds;
 
template <typename T, class compare>
using ordered_set = tree<T, null_type, compare, rb_tree_tag, tree_order_statistics_node_update>;
//usage: ordered_set< el tipo , el comparador> nombre;

const int N=1500000+100;
int tr[2*N],n;


void update(int pos,int val,bool mode){ 
	// mode=true is for add something to the MEX set,
	// mode=false is to set the inexistence of a value 
	pos+=N-1;
	tr[pos]=(mode?1e9:val);
	for(pos/=2;pos>=1;pos/=2){
		tr[pos]=min(tr[pos<<1],tr[pos<<1|1]);
	}
}



map<int,int> my;
int main(){
	fastio;
	int m; cin>>n>>m;
	vector<int> v(n);
	for(int i=0;i<n;i++){
		cin>>v[i];
	}
	for(int i=0;i<2*N;i++) tr[i]=1e9;
	for(int i=0;i<m-1;i++){		
		my[v[i]]++;
	}
	for(int i=1;i<N;i++){
		update(i,i-1,my[i-1]);
	}
	int wyn=2*1e9;
	for(int i=0;i<n-m+1;i++){
		my[v[i+m-1]]++;
		update(v[i+m-1]+1,v[i+m-1],true);
		wyn=min(wyn,tr[1]);
		my[v[i]]--;
		update(v[i]+1,v[i],my[v[i]]);
	}
	cout<<wyn<<endl;
	return 0;
}

```
</details>

## [pF: Digits Paradise in Hexadecimal](https://atcoder.jp/contests/abc194/tasks/abc194_f)
<details><summary>code</summary>

```cpp

```
</details>
