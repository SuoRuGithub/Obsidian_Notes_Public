==**Review**==
在一周以前，我们学习了马尔可夫决策过程(MDP)。
所谓马尔可夫决策过程指的是，采取一个action，下一时刻state如何只由当前state决定。**而我们的目的，就是学习一个策略，它是一个从状态空间到动作空间的映射。**
为了解决MDP问题，我们引入了Bellman方程：
$$U(s) = \max_a Q(s, a)$$
其中
$$Q(s, a) = \sum_{s^{\prime}} T(s, a, s^{\prime})(R(s, a, s^{\prime}) + \gamma U(s^{\prime}))$$
我们从数学上证明了只要上面式子中的折扣小于一，Bellman算子就是一个收缩映射，我们就可以使用迭代的方法进行计算，从而得到每个状态的$U(s)$，进而得到对应的动作$a$。以上这种方法被称作Value-Iteration。

---

针对上次的Value Iteration，我们可以分析其复杂度。
假设总共有$|S|$个状态和$|A|$个动作，每次迭代的过程中我们遍历了所有的状态，在计算一个状态的价值（也就是$U$！）的时候，我们遍历了所有动作对应的价值（也就是$Q$！），而计算$Q$的时候，我们又一次计算了所有的状态。因此算法的复杂度是$O(|S|^2|A|)$，**所以Value Iteration的问题在于太慢了！**
在完成Value Iteration的任务的时候，我们注意到Policy收敛得比Value更快，这启示我们直接对Policy进行迭代。于是我们提出Policy Iteration：
1. 随机设置初始的Policy $\pi$
2. 通过下面的方法进行迭代：
计算每个状态在当前Policy下的价值：
$$\displaystyle U^{\pi_i}_{k+1}(s) \gets \sum_{s^{\prime}} T(s, \pi(s), s^{\prime})(R(s, \pi(s), s^{\prime}) + U^{\pi_i}_k(s^{\prime}))$$
根据价值改进策略：
$$\begin{aligned}
\pi_{i + 1}(s) &= {\arg\max}_a U(s) \\
 &={\arg\max}_a \sum_{s^\prime}T(R + \gamma U^{\pi_i})
\end{aligned}$$
3. 当$\pi$收敛，我们就成功了
