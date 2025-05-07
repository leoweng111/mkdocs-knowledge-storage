# AFML笔记4: Feature Importance

1. 特征重要性也是一种有助于缓解过拟合问题的方法：回测的好结果很可能产生于过拟合。研究特征重要性，而不只看回测是更加科学的方法。
2. 有多种衡量特征重要性的方法。首先是Mean Decrease Impurity。这个是默认的推荐方法，sklearn中的RF可以直接输出（当然可以不止运用在RF上）。基本原理是度量采用一个变量进行分裂所带来的纯度下降的平均值，好处是所有变量的MDI相加等于1，可以直观比较大小，但是会受到substitution effect的影响导致重要性被低估。
3. Mean Decrease Accuracy：这个方法更好理解，主要是在OOS上计算特征重排列前后的准确率之差。但是可能所有样本的MDA都很小，同时也会受到substitution effect的影响导致重要性被低估。
4. Single Feature Importance：独立计算每个特征在OOS上的得分。好处是排除了substitution effect的影响，局限性在于SFI每次只考虑单个特征，忽视了特征之间的相互作用可能使得模型效果更好。这里我的理解是，如果有三个特征a和b和c，假设他们的SFI分别是0.1，0.2，0.5，那么我们肯定认为c最好。但是如果a和b组合之后SFI变成了0.8，那么显然a和b组合后得到了一个更好的特征。但是SFI方法没有考虑到这个。
5. 在使用MDI或MDA之前做PCA进行特征正交化可以降低substitution effect的影响，同时正交化。PCA还有额外的好处：首先有助于减少特征，加速计算；其次可以在不overfitting的情况下识别到重要特征。
6. Parallelized 和 stacked feature importance是两种使用panel data计算feature importance的方法。区别在于前者是groupby instrument然后并行计算，而后者是先合并成一个instrument然后再计算。作者推荐stack方法，主要是因为substitution effect的影响更小，而且结果更加稳健。



