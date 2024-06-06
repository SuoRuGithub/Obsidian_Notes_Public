在上一篇笔记中，我们引入了Probabilitics inference的概念，并且介绍了直接通过枚举的方法进行推断。但是这种方法的问题在于会占据大量内存。于是，我们将介绍贝叶斯网络来解决这个问题。其基本想法是使用一个有向无环图（directed acyclic graph）来描述变量之间的关系，接下来我们将详细介绍

# Structure of Bayesian Network

贝叶斯网络是一个有向无环图，结点数目等于随机变量的数目，每个结点存储一个**conditional probability table**。

