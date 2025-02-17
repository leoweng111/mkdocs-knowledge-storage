# AFML笔记6： bet sizing

书的第三部分主要讲述了回测时候的注意点。首先介绍了bet sizing。

1. 个人认为bet sizing可以理解为因子值（对于期货时序策略，因子值也可以理解为仓位），而本书的很多写法其实都是针对衍生品的。
那么，我们如何根据信号，得到恰当的bet size呢？作者介绍了很多种方法，其中我认为重要的方法是meta-labelling标签转化为因子值，
具体如下：将前几章的meta-labelling获得的概率转换为因子值。具体转换方法是假设信号的sharpe服从Gauss分布， 然后使用CDF函数值作为bet size。
且注意需要对bet size 做[-1, 1]的归一化（2*x - 1）。
2. 计算average active bets。这是因为每个信号都有一定的生命周期，在每个时刻基本都会同时存在多个信号。
我们当然可以在出发新信号的同时，就直接关闭旧信号（平仓），但是这样不好，因为旧信号还没有出发止损条件，不能将新信号的出现作为旧信号的止损条件！
更好的方式是在每个时刻取信号的平均值。其实仔细琢磨，个人认为构造因子时候常见的对因子值平滑处理和这里的计算平均活跃bet是异曲同工的，
不过平滑化处理假设了所有bet的生命周期相同。
3. 仓位离散化：为了降低换手，从而降低可能的交易手续费。这里就是常规的离散化仓位处理。
4. 动态调整bet size：随着我们预测的价格和实际的价格波动，我们可以动态调整bet size。当实际价格和预测价格之间的价差收敛时，
我们会缓慢出场，因为想要锁定profit。


