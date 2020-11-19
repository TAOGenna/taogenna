---
title: A-A Symmetrical Pizza
linktitle: A
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
