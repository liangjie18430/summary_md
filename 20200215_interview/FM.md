# 公式推导



# 为什么DNN也是可以学习交叉特征
	- 参考网址: https://zhuanlan.zhihu.com/p/52876883
	- 从网址上可以看出，FM中学习到的是vec wise的，而DNN学习到的是bit-wise的，即使一个离散特征经过embedding后，同一个embedding之前也是可以进行bit-wise的交叉的。
	- 为什么dnn可以实现bit-wise的特征交叉，可以理解为每个特征都会和下个单元层的神经作为输入，而且神经网络可以拟合任何的曲线。从网上看，神经网络学习到的交叉特征并不好解释，并不知道是多少维的。
