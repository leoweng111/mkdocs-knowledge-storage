# AFML笔记5: Hyper-Parameter Tuning with CV

这一章主要介绍了如何使用交叉验证调整超参数。
1. 网格搜索交叉验证和随机搜索交叉验证都可以在对参数的先验没有认知的情况下进行超参调整，只要设定参数网格和交叉验证方法cv即可。这里的cv设置参考了前几章的内容，可以看我之前的笔记。
2. 根据我的经验，网格搜索速度一般太慢了，所以我还是推荐使用随机搜索。
3. 如果模型对参数的变化敏感度非线性，那么参数网格的设置可以采用log-uniform的形式（针对参数是正数且随着参数增大模型的敏感度下降的情况）。
4. 关于参数搜索中scoring的选择，在meta-labelling的情况下，推荐使用f1 score。因为可以很好地平衡Precision和Recall（老生常谈的问题了）。
5. 其它情况 推荐使用neg_log_loss，因为可以更好地惩罚不同程度（不同预测概率）的错误分类情况，也就是对错误开仓的惩罚力度更大，
而如果使用accuracy，对任何预测概率的错误分类，惩罚力度都一样，在meta-label or triple-barrier method作为标签的情况下无法很好地模拟错误仓位带来的损失。


