---
layout: post
published: false
mathjax: true
featured: false
comments: true
title: Structuring ML Projects
description: An introduction about structuring ML projects
headline: Structuring ML Projects
---
>&quot;Nothing that I can do will change the structure of the universe.&quot;
><small><cite title="Einstein">Einstein</cite></small>

## Orthogonalization
Knowing what to tune in order to try to achieve one effect. This is a process we call orthogonalization.
The different effects should be orthogonal to each other, meaning there should be NO interferences between different features.

## Single Number Evaluation Metric
$$F1_{score}$$ = *Average* of **P** and **R**
where P is **Precision** and R is **Recall**.

**Precision** is the % of correctly recognized entity out of % of entites in the set. **Recall** on the otherside is the % of actual entities of correctly recognized.