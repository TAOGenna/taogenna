---
title: C-Cheap Trips
linktitle: C
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  ICPC-Regional-South-America-2018:
    parent: Problems and Solution
    weight: 3

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

This problem can be solved by dynamic programming. Let's break it down in three parts.
Let's define $dp[i]=\text{the solution for the problem for position }i$
- Current element as a new sequence : $dp[i]=dp[i-1]+c[i]$ and $dur=d[i]$
- Update the following number as if it were the second element of the sequence if $dur[i]<120$ : $dp[i+1]=dp[i-1]+c[i]+0.5\times c[i+1]$
- Complete the reamining four trips with discount $0.25%$ until the condition of the time interval break
