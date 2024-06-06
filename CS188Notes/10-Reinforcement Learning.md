**Review**
在之前我们学习的Value Iteration和Policy Iteration的方法都建立在我对对于所处环境的马尔可夫模型有着充分的了解，因此可以进行离线学习。但是，如果所处环境的$R$与$T$都是未知的呢？这时我们就需要使用强化学习的方法进行在线学习了。

---

# 基本概念
强化学习过程中，智能体与环境会进行交互。智能体在某状态采取某行动，其状态将会改变且环境会给予其一定的奖励。
智能体会先进行exploration，然后使用自己的道德策略进行exploitation。
智能体与环境进行一次交互的过程中有信息$(s, a, s^{\prime}, r)$，被称作一个sample，agent的一个生命周期内的所有sample组成了一个episode。
强化学习又分为model-based learning与model-free learning。前者会尝试先构建出真实世界的马尔可夫模型（也就是估计$T$与$R$），而后者会直接尝试估计每个状态的价值（或者Q状态价值）。
# Model-Based Learning
# Model-Free Learning
主要介绍三个内容，direct evaluation, temporal difference learning, Q-learning。~~学完Q-Learning就可以愉快地写作业了~~
## Direct evaluation
简单的说，这个方法会直接让智能体进行若干次episode，将所有得到的$(s, a, s^\prime, r)$元组进行平均，得到每个状态的价值
## Temporal Difference Learning
和Direct evaluation对比，Temporal difference learning会从每一次经历中学习，而不是对得到奖励的总和进行平均。
在之前的Policy Iteration中，我们这样计算一个状态在一个固定策略下的价值：
$$V^\pi(s)=\sum_{s^\prime}T(s, \pi(s), s^\prime)(R(s, \pi(s), s^\prime) + \gamma V^\pi(s^\prime)$$
可是现在，我们并不知道真实世界的$T(s, \pi(s), s^\prime)$，我们应该如何计算一个状态的价值呢？Temporal Dirrerence Learning给出：
$$sample = R(s, \pi(s), s^\prime) + \gamma V^\pi(s^\prime)$$
而
$$V^{\pi(s)} \gets (1 - \alpha)V^\pi(s) + \alpha \cdot smaple $$
上式中的$\alpha$是学习率，一般学习率一开始为1，最后慢慢减小到0
之所以叫做时序差分学习，是因为在学习过程中，我们更注重最新的sample，老的sample会指数级地向0衰减。
## Q-Learning
Q-Learning的想法是直接学习Q value：$Q(s, a)$。在介绍Value Iteration的部分，我们定义了$Q(s, a) =\displaystyle \sum_{s^\prime} T(R + \gamma V)$，而$V = \displaystyle \max_a Q$，因此我们可以使用下面的方法迭代得到Q:
$$Q_{k + 1}(s, a) \gets \displaystyle \sum_{s^\prime} T(R + \gamma \max_a Q_k(s^\prime, a))$$
但是我们不知道$T$，因此我们继续沿用Temporal Difference Learning的做法：
$$sample = R + \gamma \max_aQ$$
$$Q(s, a) \gets (1 - \alpha)Q(s, a) + \alpha \cdot sample$$
一个很有趣的事情是，在Temporal Difference Learning中，我们在计算某个策略下某个状态的价值，但是在使用Q-Learning计算Q价值的时候，我们并不需要预先给定一个策略！因此，我们称Q-Learning的方法是off-policy的，而之前介绍的方法是on-policy的。

**Approximate Q-Learning**
Q Learning仍然存在着一些问题，有时候现实的情况太多，无法完全遍历，我们希望提高模型的**泛化能力**，也就是能处理没有见过的类似情形。在经典的Q-Learning中，对于每个状态（Q状态），我们是按照表格的方式记录的，但是在Approximate Q-Learning中，我们记录的是状态的**特征**。
我们可以用特征向量表示价值函数：
$$V(s) = \bf{w^T} \bf{f}(s)$$
$$
Q(s, a) = \bf{w^T}\bf{f}(s, a)$$
其中$\bf f$是特征向量，$\bf w$是权重向量。
因此，Approximate Q-Learning中，只要更新权重向量就可以了。
![[Pasted image 20240605121723.png]]
这里我没太搞懂，这定义是怎么来的？