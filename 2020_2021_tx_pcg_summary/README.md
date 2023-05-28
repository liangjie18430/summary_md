# 说明
此处为针对一些在tx的pcg的一些工作上的一些总结，包括一些自己的疑问


# 频道间迁移
## 如何计算相似度
1. 一般迁移的时候，都是使用较大的频道，往较小的频道进行迁移（小业务冷启动），之前成功过的经验体育频道和nba频道的数据混合，对nba有帮助，娱乐和明星频道的混合训练，也有帮助。
2. 也可以使用ztl的相关进行训练后，然后使用fine-tuning的形式,在fine-tuning中，又包含俩个，第一个是固定embedding，第二个是不固定embedding，在本人的实验中，不固定embedding比固定embedding取得了更高的收益，不固定embedding的时候减小学习率。

## 账号推荐如何过滤噪声样本
比如：近7天内不关注用户的样本(因为有些用户本来就不关注)

# 投放
主要是训练embedding

# minet
attention包含俩个部分
参考网址: https://zhuanlan.zhihu.com/p/344691028
1. item_level attention
2. interest_level attention
Long-term interst across domain: 个人基本信息
Short-term interst from the source domain：对于要预测其CTR的每个目标广告，在源域中存在相应的短期用户行为（例如，用户刚刚观看的新闻）。虽然一条新闻的内容可能与目标广告的内容完全不同，但它们之间可能存在一定的相关性。例如，一个用户在观看了一些娱乐星闻之后有很大的概率点击一个游戏广告，基于这样的关系，我们就可以从源域中的有用的信息迁移到目标域中。

Short-term interest in the target domain: 用户最近点击的广告可能对用户在短期内点击的广告有很大的影响

所以在item级别的attention，都是使用目标广告和这些历史信息计算attention。
user特征进行共享，其实源域部分用于训练好user_embedding,loss是使用target域和source域进行相加的
# ddpg超参数
## 具体模型流程图
参考processon,微信登陆，

采用target目标网络更新（为什么要用target网络？因为训练的网络特别不稳定）；

# 总监级别的思考角度
这边总监的一个特点是，问你所做的项目对业务的价值，比如根据你的简历，账号推荐、UGC内容推荐在部门中有什么价值，解决什么问题（这里你可以从这个思路去讲，引入UGC内容的目的是完善原有的PGC内容为主的内容生态，PGC内容的特点是什么，UGC内容的特征是什么，市场上抖音快手B站他们是怎么做内容生态中这一块的，我们的推荐算法在这里会遇到什么与PGC不一样的问题，怎么解决的）

# wkfm
fm存在的问题，fm有一个假设，特征俩俩相关，不然会存在梯度耦合的问题。
FFM和AFM都是可以解决梯度耦合问题的模型
AFM在attention网络输出为0时，会变得难训练
