# 一面说明
业务方向： 骑手定价
1. ple为什么可以解决跷跷板问题。
    gate网络有权重
    本身分层，任务k的独享专家模块融合了上一层网络中任务k的独享专家模块和共享专家模块，而共享专家模块则融合了上一层所有的专家模块.
MMOE 忽略了专家网络间的差异性和交互信息, PLE采用一种渐进式分离 routing 的方案来从所有的底层 experts 中获取信息，抽取成高阶的共享知识，并逐渐分离 task-specific 参数。




2. 介绍下ppo的actor网络和critic网络


3. 在推荐技术方向上，后续有什么可以有优化的方向.
    答的迁移学习，在大模型时代，更优质的数据和更多的
4. 算法题
    合并重叠区间



# 新部门一面

1. 假设有多个不同的业务，是每个业务，单独部署一个，还是多个业务，采用一个基座，多个adapter的方式做inference
    * 可以对比一下对应的响应时间，因为LLM的响应时间影响还是大的
    * 一个基座本身会带来更多的单点问题，假设做一些修改，导致基座出问题，会同时影响10个业务
    * 面试反馈更多的可能是一个模型的吞吐量，感兴趣可以去了解下

2. 如果提升模型的响应时间
    * 给定的prompt词可以更可能的短，attn会影响效果
    * flash attention等手段
    * 量化剪枝等手段

3. 为什么使用deepspeed？？？
	todo： 待

算法题：
    找到循环链表的入口
    给一个链表，若其中包含环，请找出该链表的环的入口结点，否则，返回null。
输入描述：输入分为2段，第一段是入环前的链表部分，第二段是链表环的部分，后台将这2个会组装成一个有环或者无环单链表
返回值描述：返回链表的环的入口结点即可。而我们后台程序会打印这个节点
示例1
输入：{1,2},{3,4,5}
返回值：3
说明：返回环形链表入口节点，我们后台会打印该环形链表入口节点，即3
  未做出来，只提供了快慢指针的思路
	面试官非常友好



# 新部门二面
    算法题：调整list，将倒数第一个插入第一个数和第二个数之间，将倒数第二个插入第二个数和第三个数之间
        重排链表，先翻转，后插入
