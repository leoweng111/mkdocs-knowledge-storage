# AFML笔记8: Backtesting Through Cross-Validation

这章主要讲了交叉验证如何应用在回测中。

1. walk forward backtesting (WF)方法是最常规的回测方法，但是很容易过拟合，并且一开始的很多预测结果是基于小样本量的，会导致sharpe等参数估计方差过大，同时walk backward的结果可能和WF的结果相差很大，说明WF方法不具备对未来可能情形的稳健性。
2. CV可以解决上述很多的WF方法的缺点。首先我们要明确CV的目的：不是为了查看历史数据上策略的真实表现，而是查看策略在未知情形下的表现，这就是前面提到过的情形模拟。这可以帮助降低过拟合。
3. CV也有一些缺点，比如也只存在一条path（虽然不是沿着时间流向的path）。
4. 作者提出CPCV的方式，主要是将CV结合了前面章节的purge和embargo方法，同时通过在每次交叉验证的时候给测试集安排大于一份的分割后的子样本，增加了交叉验证的path数量，减小了估计结果的方差。如果测试集包含的子样本数量等于1，那么CPCV就会退化成为普通的CV。因此，CPCV可以理解为 a generalization of CV。
5. CPCV需要再产生每条path所使用的训练集大小、path的数量之间进行权衡。这两者其中一个增加，另外一个就需要减小。这点我理解本质上是偏差方差均衡。
6. CPCV为什么可以缓解overfit的问题？首先，WF导致sharpe等指标的计算很大程度上受到小部分样本的影响，方差很大，方差大就会导致false discovery。CV方法虽然降低了false discovery，但是path仍然只有一条。而CPCV方法通过多条path有效降低了估计的方差。


