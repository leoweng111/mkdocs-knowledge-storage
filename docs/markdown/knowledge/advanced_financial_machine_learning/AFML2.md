# AFML笔记2: Model

最近这几天继续看AFML。我分了几篇笔记继续总结。求个赞[偷笑R]，感兴趣的朋友也可以看我的其他笔记。
首先model这块主要以RF为例概述了机器学习模型。重点在于方法论的介绍而不是具体模型的算法。如果想要深入了解具体模型，建议额外寻找资料学习。

1. 首先是集成学习模型，主要分为bagging和boosting。对于bagging模型，只要基学习器之间相关性较低，就可以降低方差，防止过拟合同时提升正确率。bagging模型也是作者主要推荐用在金融领域的，因为boosting模型主要处理的是underfit，这在金融领域上一般没有overfit问题重要。
2.  观察值的冗余（样本之间的相关性）会对bagging有不好影响：首先每次bootstrap抽取的样本之间相关性强，导致训练出的基分类器之间相关性也强；其次out-of-bag accuracy会受到影响（被高估）。
3. bagging的经典模型随机森林相比基础的bagging classifier，引入了两次相关性（还有一次是在每次分支的时候只考虑一个随机的子特征集合）。
4. bagging模型无法承担过大的样本量（比如SVM），那么可以对基模型使用早停，然后再利用bagging降低集成模型的方差。


