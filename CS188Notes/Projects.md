# Project 3

**Q5 Q-Learning & Pacman**

我们要用Q-Learning的方法做一个吃豆人

# Project 4

在这个任务中，我们需要写一个进阶版的吃豆人——通过贝叶斯网络进行推断，得到鬼魂的位置。

## Question 1: Bayes Net Structure

这道题搞了我一中午，但其实只有寥寥几行代码而已。主要原因是没有搞清楚应该干什么。

```python
def constructBayesNet(gameState: hunters.GameState):

    """

    Construct an empty Bayes net according to the structure given in Figure 1

    of the project description.

  

    You *must* name all variables using the constants in this function.

  

    In this method, you should:

    - populate `variables` with the Bayes Net nodes

    - populate `edges` with every edge in the Bayes Net. we will represent each

      edge as a tuple `(from, to)`.

    - set each `variableDomainsDict[var] = values`, where `values` is a list

      of the possible assignments to `var`.

        - each agent position is a tuple (x, y) where x and y are 0-indexed

        - each observed distance is a noisy Manhattan distance:

          it's non-negative and |obs - true| <= MAX_NOISE

    - this uses slightly simplified mechanics vs the ones used later for simplicity

    """

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

    # 问题1就是让我们创建一个贝叶斯网络，只需要把variables, deges, variableDomainDict完成就可以

    # 我现在非常困惑，这到底是要我干个啥，网上的题解也没看懂

    variables.append(PAC)

    variables.append(GHOST0)

    variables.append(GHOST1)

    variables.append(OBS0)

    variables.append(OBS1)

    # edge形式为(from, to)

    edges.append((GHOST0, OBS0))

    edges.append((PAC, OBS0))

    edges.append((PAC, OBS1))

    edges.append((GHOST1, OBS1))

    # variable的domain指的是?也许是值域？比如Pacman能取所有坐标，OBS是观察到的两个曼哈顿距离，它们最大取X_range + Y_range

    variableDomainsDict[PAC]=[(i,j) for i in range(X_RANGE) for j in range(Y_RANGE)]

    variableDomainsDict[GHOST0]=[(i,j) for i in range(X_RANGE) for j in range(Y_RANGE)]

    variableDomainsDict[GHOST1]=[(i,j) for i in range(X_RANGE) for j in range(Y_RANGE)]

    variableDomainsDict[OBS0]=[i for i in range((X_RANGE+Y_RANGE+MAX_NOISE-1))] # 此处是否应该断言i是非负的？

    variableDomainsDict[OBS1]=[i for i in range((X_RANGE+Y_RANGE+MAX_NOISE-1))]

  

    # raiseNotDefined()

    "*** END YOUR CODE HERE ***"

  

    net = bn.constructEmptyBayesNet(variables, edges, variableDomainsDict)

    return net
```