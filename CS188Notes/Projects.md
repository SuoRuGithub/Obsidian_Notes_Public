# Project 3

**Q5 Q-Learning & Pacman**

我们要用Q-Learning的方法做一个吃豆人

# Project 4

在这个任务中，我们需要写一个进阶版的吃豆人——通过贝叶斯网络进行推断，得到鬼魂的位置。

## Question 1: Bayes Net Structure

这道题搞了我一中午，但其实只有寥寥几行代码而已。主要原因是没有搞清楚应该干什么。

```python
def constructBayesNet(gameState: hunters.GameState):
    # constants to use
    PAC = "Pacman"
    GHOST0 = "Ghost0"
    GHOST1 = "Ghost1"
    OBS0 = "Observation0"
    OBS1 = "Observation1"
    X_RANGE = gameState.getWalls().width
    Y_RANGE = gameState.getWalls().height
    MAX_NOISE = 7
    
    variables = []
    edges = []
    variableDomainsDict = {}
    "*** YOUR CODE HERE ***"

    "*** END YOUR CODE HERE ***"
    
    net = bn.constructEmptyBayesNet(variables, edges, variableDomainsDict)
    return net
```

可以看到，我们要做的就是把`variables`，`edges`，`variableDomainsDict`这三个变量确定好，之后代码就会自动调用`bn.constructEmptyBayesNet`来构建一个贝叶斯网络，其结构如下所示：
![[Pasted image 20240607060124.png]]

那其实没有那么难，`variable`就是所有的结点，`edges`中每一个元素是一个`(from, to)`的二元组，但是`domain`是什么呢？这东西困惑了我好久，但是实际上，问题的Discription已经告诉你了，`domain`就是各个变量可以取的值。比如`Ghost/Pacman`变量的取值是地图上的所有坐标点，而`Obs`是观测到的曼哈顿距离，它能取的最大值无非就是整张地图的`X_RANGE` + `Y_RANGE` + `NOISY`罢了。

这没什么难的，搞不出的原因可能就是我英语太渣，Discription没有看明白。

## Question2: Join Factors

这里就是让我们返回一个联合概率，主要就是利用概率计算的链式法则，链式法则本身是不困难的，但是运用它对一些概率的式子进行化简可能没那么容易。下面是几个例子：
1. $$\begin{align}
&P(V, W | X, Y, Z) \cdot P(X, Y | Z) \\
=& \frac{P(V, W, X, Y , Z)}{P(X, Y, Z)} \cdot P(X, Y | Z)\\
=&\frac{P(V, W, X,Y,Z)}{P(X, Y | Z) \cdot P(Z)} \cdot P(X, Y |Z) \\
=&P(V, W, X, Y|Z)
\end{align}
$$
2. $$P(X | Y, Z) \cdot P(Y) = P(X,Y|Z)$$(为什么？)
3. $$
P(V | W) \cdot P(X|Y) \cdot P(Z) = P(V, X, Z | W, Y)$$

在完成这道题目的时候，需要用到`Factor`这个类，但是啥是`Factor`？它有什么作用？

事实上，这里的`Factor`表示了一个？

表示了一个什么我也不知道，这个问题我看了一下午，到现在还没搞懂自己在做什么，抄了[CS188-Project-4/factorOperations.py at main · caigun/CS188-Project-4 (github.com)](https://github.com/caigun/CS188-Project-4/blob/main/factorOperations.py)这里的代码

## Question3: Eliminate

说太多没用，直接看我们希望得到的输入输出吧。

**输入**：一个`factor`、一个`eliminationVariable`

**输出**：一个新的`factor`

具体来说，原来的`factor`对应的CPT是这样子的：
![[Pasted image 20240607141803.png]]

设置，最后得到的CPT是这样的：
![[Pasted image 20240607141847.png]]

