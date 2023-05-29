# GBDT
gbdt 无论用于分类还是回归一直都是使用的CART 回归树。这里面的**核心**是因为gbdt 每轮的训练是在上一轮的训练的残差基础之上进行训练的。这里的残差就是当前模型的负梯度值 。这个要求每轮迭代的时候，弱分类器的输出的结果相减是有意义的。**残差相减是有意义的，类别相减是没有意义的。**

树模型可以不需要归一化就可以使用数据。
bagging 主要关注降低方差

第m次学习的目标，是前m-1棵树预测值的累加和的残差
1、GBDT中分类和回归都是采用的回归树:（低方差高偏差，因为训练的过程是降低偏差来不断提高最终分类器的精度）,一般树的深度为6
2、为什么每棵树学习的是前n-1颗树的负梯度。 参考网址:https://www.zhihu.com/question/63560633/answer/801224574
   需要注意的是，知乎上说的，其他的一阶泰勒展开是对x求导，而梯度提升树是对前n-1颗树求导。

3、二分类的损失函数为什么为负二项对数似然损失
	参考网址:  https://www.cnblogs.com/Luv-GEM/p/10661327.html
4、选择最优变量和最优切分点
	遍历每个特征，遍历切分点，计算最小值后获取最优的特征和最优的切分点 代码参考:  https://www.cnblogs.com/ModifyRong/p/7744987.html
5、树节点内部分裂的特征选择则是固定为 CART 的均方差，目标损失函数可以自定义。
6、GBDT缺失值处理会将该样本放入到所有分支中，并调整该样本的权重
# GBDT 和LR
 reference: https://zhuanlan.zhihu.com/p/60952744
6、而对于 GBDT，其更适合处理稠密特征，如 GBDT+LR 的Facebook论文中，对于连续型特征导入 GBDT 做特征组合来代替一部分手工特征工程，而对于 ID 类特征的做法往往是 one-hot 之后直接传入 LR，或者先 hash，再 one-hot 传入树中进行特征工程，而目前的主流做法是直接 one-hot + embedding 来将高维稀疏特征压缩为低纬稠密特征，也进一步引入了语意信息，有利于特征的表达

7. 参考网址:https://www.jianshu.com/p/96173f2c2fb4
   - LR更适合稀疏特征是因为LR的惩罚项为对权重的惩罚，树模型的惩罚项通常为叶子节点个数和树的深度等
# GBDT如何做特征选择

# xgboost 和GBDT的不同点
1、注意，GBDT和xgboost对应缺失值的处理方式不一样，GBDT对应缺失值的处理参考网址
	- https://www.jianshu.com/p/f24534a131e1




# bagging 方法和boosting方法的不同点
	* bagging: 该方法通常考虑的是同质弱学习器，相互独立地并行学习这些弱学习器，并按照某种确定性的平均过程将它们组合起来。
		- 重点在于获得一个方差比其组成部分更小的集成模型,可以并行化训练
	* boosting: 该方法通常考虑的也是同质弱学习器。它以一种高度自适应的方法顺序地学习这些弱学习器（每个基础模型都依赖于前面的模型），并按照某种确定性的策略将它们组合起来。
	* stacking: 该方法通常考虑的是异质弱学习器，并行地学习它们，并通过训练一个「元模型」将它们组合起来，根据不同弱模型的预测结果输出一个最终的预测结果。
		- boosting 和 stacking 则将主要生成偏置比其组成部分更低的强模型