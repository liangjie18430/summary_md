# word2vec
	- word2vec直观解释：参考网址:https://www.zhihu.com/question/44832436
	- 下采样的方法解释： 
		* 会将softmax的问题转换为是否共现和非共现的二分类问题。
		* 该二分类问题会采用sigmoid函数，sigmoid函数
	- table表的初始化
		* 可以参考网址: https://blog.csdn.net/jingquanliang/article/details/82886645
		* 注意，table的大小任意指定，但是table中不同的位置对应的不同的词，该词在该table中的频率通过3/4这种概率来进行的指定。
		* 
