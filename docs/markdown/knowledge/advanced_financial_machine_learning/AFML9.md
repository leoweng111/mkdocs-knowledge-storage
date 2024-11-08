# AFML笔记9: Backtesting on Synthetic Data

如果我们不通过历史数据回测，那么还有什么方法可以评估策略的有效性呢？我们可以通过生成的模拟数据对策略进行测试。
通过模拟数据而不是历史数据测试还有一个好处，就是可以降低过拟合问题，因为保证了策略不会因为过拟合于某一个特定历史时期上的数据。

1. 首先，需要理解trading rule（R）。我个人理解是任何策略本质上都可以抽象为一个触发交易信号（多头or空头）、一个止盈信号、一个止损信号。其中止盈止损信号也可以省略。这里的trading rule就是一个特定策略的止盈止损信号。
2. 在定义了trading rule后，对某个特定策略，我们可以给定一个R的集合Ω，然后网格搜索IS得到最佳的R*。同时，我们可以定义R*存在过拟合的条件：R*在OOS上表现甚至不如R的中位数（类比PBO的定义）。
3. 作者先假定价格服从O-U process，然后根据给定每种策略估计O-U process的参数，接着利用估计的参数进行蒙特卡洛模拟：生成价格路径，对每个R∈Ω计算sharpe，然后选出最佳的R。
4. 最后作者通过实验测试了上述方法，结论是给定价格和策略，存在一个最佳的R*，使得策略的sharpe最大。


