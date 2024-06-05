**Review**
在一周以前，我们学习了马尔可夫决策过程(MDP)。
所谓马尔可夫决策过程指的是，采取一个action，下一时刻state如何只由当前state决定。**而我们的目的，就是学习一个策略，它是一个从状态空间到动作空间的映射。**
为了解决MDP问题，我们引入了Bellman方程：
$$U(s) = \max_a Q(s, a)$$
其中
$$Q(s, a) = \sum_{s^{\prime}} T(s, a, s^{\prime})(R(s, a, s^{\prime}) + \gamma U(s^{\prime}))$$
我们从数学上证明了只要上面式子中的折扣小于一，