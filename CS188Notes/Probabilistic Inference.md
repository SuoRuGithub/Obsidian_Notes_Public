#概统

这里需要一些简单的概率论知识，CS70我本该学的，可是我摆烂了。

**marginal distribution(边缘概率分布)**

所谓“边缘”，其实可以理解成是加和。举个例子，豌豆黄色子叶的概率是多少？回答这个问题的时候你并没有考虑这些黄色子叶的豌豆是圆粒还是皱粒，这就是边缘概率

# Probabilistic Inference

之前的学习中，我们处理的环境的状态是固定的。现在我们需要处理的情况是，环境本身的状态就非固定，而是有着自己的概率分布。

而probabilistic inference的目标就是（也许是？），推断出我们希望知道的概率。

# Inference By Enumeration

现在假设我们希望知道概率分布$P(Q1, \cdots, Q_m | e_1, \cdots, e_n )$，我们将所有的随机变量分为：1）Query variables，2）Evidence variables，3）Hidden variables。我们使用下面的方法计算要求的概率分布：

1. 找到所有Evidence variables发生的事件
2. marginalize所有的Hidden variables
3. Normalization，使得概率分布总和为1

这个方法有些过于直观了，就像高中生物题目列表格一样。