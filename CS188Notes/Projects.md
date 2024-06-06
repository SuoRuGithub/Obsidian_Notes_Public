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

可以看到，我们要做的就是把`variables`，`edges`，`variableDomainsDict`这三个变量确定好，之后代码就会自动调用`bn.constructEmptyBayesNet`来构建一个贝叶斯网络。

那其实没有那么难，`variable`就是所有的结点