---
title: "epsilon-Greedy vs epsilon-Soft"
date: 2020-11-30T11:35:49+08:00
draft: false
tags:
  - reinforcement learning
---

In reinforcement learning, we can't run infinite times to update the whole $Q$ - value table or $V$ - value table, efficient update choices must be made. 

Generally thinking, which $s$ or $(s,a)$ has more opportunity to get $R$ (high value), should be updated more to converge to the optimal. But stochastic exploring is also required to jump out of sub-optimal. The simple idea to implement is $\epsilon$ -greedy.

**Tips:**

To generate a list of probability of action set, which sum to 1, we can use Dirichlet distribution, e.g.

```python
p=numpy.random.dirichlet(np.ones(n_actions))
```

![Dirichlet](/rl/dirichlet.png)

# $\epsilon$ -Greedy

$$
\begin{aligned}\max &: p=1-\epsilon+\frac{\epsilon}{|A|}\\\\ \mathrm{others}&: p=\frac{\epsilon}{|A|}\end{aligned}
$$

i.e, random chose with $\epsilon$ and chose the best with $1-\epsilon$

![epsilon-greedy](/rl/e_greedy.png)

with code

```python
p[max_value_index]=1-epsilon
p+=epsilon/n
```

# $\epsilon$ - Soft

the only requirement of $\epsilon$  -  Soft is each probability greater than $\epsilon /|A|$, Dirichlet is useful here.

![epsilon-greedy](/rl/e_soft.png)

```python
p=np.random.dirichlet(np.ones(n))*(1-epsilon)
p+=epsilon/n
```




