---
title: An example title
summary: Here we describe how to add a page to your site.
date: "2018-06-28T00:00:00Z"

reading_time: false  # Show estimated reading time?
share: false  # Show social sharing links?
profile: false  # Show author profile?
comments: false  # Show comments?

# Optional header image (relative to `static/media/` folder).
header:
  caption: ""
  image: ""
---

Add your *content* here...<br>
# Solution(?) for "New year and handle change"

First, let's guess some $dp$ states:
$$
dp[n][k]=\text{solve the problem for the prefix of leght n allowing k operations}\\
$$
Now, we will going down throughout the complexities all along till we hit the lowest achievable.

- $tran(i,j)$ is a function which will tell us the number of uppercase and lowercase letters in order to make the difference *if we apply an operation in this range*. This function can be implemented to give results in O(1) with precomputation.
- $f(i,j)$ is very like $tran(i,j)$ but this function just give the difference in the range $[i,j]$ if no operation have been applied there. This function can be implemented to give results in O(1) with precomputation.

## $O(n^3)$ :

$$
dp[n][k]=min\{dp[n-1][k],\mathop{\stackrel{n-1}{min}}_{i=k}\{dp[i-1][k-1]+tran(i,i+l-1)+f(i+l,n)\} \}\\
$$

## $O(n^2)$ : 

In this case I have explode the fact that our $dp$ will pass through all pairs of $(n,k)$ so now it isn't necessary to make an intern process like $\stackrel{n-1}{min}$. Our variable $acum$ will take care of that process, so now for each pair $(n,k)$ we just have to compute what could be the result if we place our index on $n-1$ with $1$ more operation allowed(because we have already use $k-1$ operations -> because of the $acum$ variable).
$$
dp[n][k]=min\{acum,dp[n-2][k-1]+tran((n-2),(n-2)+l-1)+f(n-2,n_{total})\}\\
acum=min(acum,dp[n][k])
$$

## $O(n\log_2 n)$ :

As ***ElAlienMaster*** is already expecting, this approach is using the Alien's Trick. For this approach all we do is an interpolation in order to include a $\lambda$ to act as a cost. 
$$
dp_\lambda[n]=min\{dp_\lambda[n-1],\mathop{\stackrel{n-1}{min}}_{i=k}\{dp_\lambda[i-1]+\lambda+tran(i,i+l-1)+f(i,n_{total}) \}\}
$$
