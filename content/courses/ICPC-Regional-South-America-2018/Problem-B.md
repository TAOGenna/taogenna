---
title: B-Building a Field
linktitle: B
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
This problem can be approach in many ways, some more complicated than others. But the easiest way is given by the following observation: Let $A$,$B$,$C$,$D$ be a rectangle incribed in the circunference and be $acum[p]$ the sum acumulation of the arcs till position $p$, this is $acum[p]=\sum_{i=1}^{p} arc[i]$. We know that $A-B$ and $C-D$, opposite corners, are both diameters. What I mean by this is that if we are in the position $j$ of the given arcs and $S=\sum_{i=1}^n arc[i]$ then if that position form a diameter with other point in the circunfernce, that point must be in $acum[i]+\frac{S}{2}$. With this observation what is left is to find two different points that generate a diameter. 
 
