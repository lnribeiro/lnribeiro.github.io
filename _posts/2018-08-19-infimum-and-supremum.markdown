---
layout: post
title:  "Supremum and infimum"
date:   2018-08-19 13:13:01 -0300
external-url: https://lnribeiro.github.io/2018/08/19/infimum-and-supremum/
---

Sometimes when reading math books, like [Convex Optimization](https://web.stanford.edu/~boyd/cvxbook/bv_cvxbook.pdf), I stumble upon the infimum ($$\inf$$) and supremum ($$\sup$$) operators. For example, let $$L(x,\lambda,\nu)$$ denote the Lagrangian associated with an optimization problem. The *Lagrange dual function* is defined as 

$$
g(\lambda,\nu) = \inf_{x \in \mathcal{D}} L(x,\lambda,\nu),
$$

where $$\mathcal{D}$$ stands for the domain of $$x$$. But what exactly is the infimum? And the supremum? What are their relation to the minimum ($$\min$$) and the maximum ($$\max$$) operators?

To better understand these operators, I read the great Wikipedia article [Infimum and supremum](https://en.wikipedia.org/wiki/Infimum_and_supremum). Therein, we have the following definitions. Let $$P$$ be a partially ordered set and $$S$$ a subset, $$S \subseteq P$$.

**Infimum**

* A *lower bound* of $$S$$ is any element $$l \in P$$ such that $$l \leq x$$ for all $$x \in S$$.
* $$l^* \in P$$ is the *infimum* of $$S$$ if it is larger than any other lower bound, i.e., $$l^* \geq l$$.


**Supremum**

* An *upper bound* of $$S$$ is any element $$u \in P$$ such that $$u \geq x$$ for all $$x \in S$$.
* $$u^* \in P$$ is the *supremum* of $$S$$ if it is larger than any other upper bound, i.e., $$u^* \leq u$$.

Consider the following examples to illustrate these definitions:

1. Let $$P = \mathbb{R}$$ and $$S = \{ x \in P \mid 0 < x < 1\}$$. Then $$\inf{P} = 0$$ and $$\sup{P} = 1$$. 
2. Let $$P = \mathbb{Z}$$ and $$S = \{1,2,3\}$$. Then $$\inf{P} = 1$$ and $$\sup{P}=3$$.

In the first example, $$P$$ does not have minimum and maximum values: for any $$x \in S$$, we can always define a $$y > x$$, and a $$z < x$$. So, infimum and supremum may be useful to describe sets which may not have minimum and maximum. In the second example, the infimum and supremum coincide with minimum and maximum: we have that $$\max{S} = \sup{S}=3$$ and $$\min{S} = \inf{S} = 1$$.



