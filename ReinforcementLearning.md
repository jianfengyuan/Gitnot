# 强化学习
## 1. Bellman 方程
状态值函数$V_{\pi}(s)$可以评价当前状态的好坏，每个状态的值不仅由当前的状态决定，还由后面的状态决定，所以状态的累计奖励求期望就可以得出当前s的状态值函数$V(s)$
$$
\begin{aligned}
V_\pi(s) = E(U(t)\vert S_t = s) \\
V_\pi(s) = E[R_{t+1}+\gamma[R_{t+2}+\gamma[....]]\vert S_t=s] \\
V_\pi(s) = E[R_{t+1}+V_\pi(s')\vert S_t=s]
\end{aligned}
$$
## 2. off-policy和on-policy 
更新价值所使用的方法是沿着既定的策略（on-policy）抑或是新策略（off-policy）
## 3.Q-Learning
更新方程
$$
Q(s,a) \leftarrow Q(s,a) + \alpha[r+\gamma max_{a'}Q(s',a')-Q(s,a)]
$$
## 4.Sasa
- [ ] TODO