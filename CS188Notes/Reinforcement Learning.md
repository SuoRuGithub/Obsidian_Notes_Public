**Review**
在之前我们学习的Value Iteration和Policy Iteration的方法都建立在我对对于所处环境的马尔可夫模型有着充分的了解，因此可以进行离线学习。但是，如果所处环境的$R$与$T$都是未知的呢？这时我们就需要使用强化学习的方法进行在线学习了。

---

# 基本概念
强化学习过程中，智能体与环境会进行交互。智能体在某状态采取某行动，其状态将会改变且环境会给予其一定的奖励。
智能体会先进行exploration，然后使用自己的道德策略进行exploitation。
智能体与环境进行一次交互的过程中有信息$(s, a, s^{\prime}, r)$，被称作一个sample，agent的一个生命周期内的所有sample组成了一个episode。
强化学习又分为model-based-learning与