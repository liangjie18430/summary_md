# 参考网址
https://www.zhihu.com/question/28641663/answer/825184220

1. 变量分布分析
	- 定类: a(属性).离散无序	b(示例).性别	c(描述性统计).频率、占比、众数	d(可视化).条形图、饼图
	- 定序: a.有序比较  b.期末绩点	c.频率、分位数、百分位数	d.条形图、饼图、箱型图
	- 定距: a.数值差别	b.温度	c.频数、众数、标准差、方差中位数	d.条形图、饼图、箱型图、直方图
	- 定比: a.连续，存在绝对零点	b.重量、收入	c.均值，标准差	d.同定比
2. 变量处理
	- 有序变量：存在大小关系，比如期末成绩绩点：(A,B,C,D,E)，使用标签编码变成1，2，3, 4, 5
	- 类型变量：进行onehot
	- 数值型变量：分箱处理
	- 删除掉缺失特征的行，删除之后，我们还需要看看数据的分布，对比目标占比、特征分布与先前的是否存在明显差异，如果是的话，建议不要使用这种办法。
	- 缺失值填充，可以采用均值，unknown、中位数填充



3. 文本变量处理
	- bag of words: 分词（tokenizing）、计数（counting）、归一化（normalizing）
	- CountVectorizer: 将文本转换为矩阵，每列代表一个词语，每行代表一个文档，所以一般出来的矩阵会是非常稀疏
	- TF-IDF 
