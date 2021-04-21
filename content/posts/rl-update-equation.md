---
title: "Value Update Comparsion among Basical RL"
date: 2020-11-30T11:13:00+08:00
draft: false
categories: ComputerTech
tags:
  - reinforcement learning
---

In this post, we will compare the state value update or state-action value update equation in fundamental rl methods.

# Monte Carlo

$$V(s)\leftarrow V(s)+\frac{1}{N}\[G_t-V(s)\]$$

recall that, monte carlo update use average $V(s)=\sum G_t/N$. After simple transformation, we will have the error form equation:point_up_2:.

and the corresponding state-action value update is:

$$Q(s,a)\leftarrow Q(s,a)+\frac{1}{N}\[G_t-Q(s,a)\]$$

# Temporal Difference

TD is driven from $\alpha$ - Monte Carlo, but replace the $G_t$ with $R_t+\gamma V(s')$, since we want a instant update per step rather than till terminal.

$$V(s)\leftarrow V(s)+\alpha \[R_t + \gamma V(s') -V(s)\]$$

The state-action one is simply change the $V(s)$ to $Q(s,a)$, and becomes **Sarsa** (omitted).

# Q-learning

Q-learning is a **off-policy** method, where the update ignores the policy while other **on-policy** only use the state-action value determinted by $\pi(a|s)$. Recall that, even $s$ and $a$ are connected in $Q(s,a)$, but the $s'$ is determineted by environment, and $a$ is chosen by $\pi(a|s)$.

$$Q(s,a)\leftarrow Q(s,a)+\alpha[R_t+\gamma Q_{max}(s',a')-Q(s,a)]$$

