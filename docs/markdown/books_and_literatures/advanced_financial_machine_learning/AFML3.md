# AFML笔记3: Cross Validation

这块主要介绍了交叉验证的使用。

1. 金融领域中交叉验证失败的主要原因是informational leakage，主要原因仍然是前面介绍的样本冗余导致的相关性。注意，只有训练集和测试集中的X和y同时相关，我们才能说存在informational leakage。
2. 解决informational leakage的方法：
   - Purge：解决的是样本标签之间的相关性。 
   - embargo：解决的是时间序列数据的serial correlation。 
3. 最终的结果：使用PurgedKFold，注意这里定义了新的类，可以直接用于后续的GridSearchCV中的cv参数，实现自定义网格搜索交叉验证（或随机搜索也行）。


