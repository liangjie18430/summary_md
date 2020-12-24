# attention 机制
	- 注意: attention机制分位俩种，一种为加法注意力机制，一种为乘法注意力机制。
	加法注意力机制就是concat后乘以权重，然后通过tanh的全联接层。
	attention机制的优势：
		1. 更容易捕获句子中的中长距离相互依赖的
		2. 可以做成并行模式
	缺点： 无法捕捉位置信息，可以加入位置信息来改善
	LSTM需要按照序列向后传播，lstm学习到长期依赖的可能性较低。
# Transformer

1. transformer采用自注意力机制

2. k、q、v传入后会先经过一层dense

3. transformer中每一层的输入和输出维度一致，不然无法使用残差连接

4. transformer中的涉及到俩种mask操作，一种为padding mask，一种为Sequence mask。

     较好的网址参考:https://www.cnblogs.com/zhouxiaosong/p/11032431.html

   * Padding mask: 对于输入序列一般我们都要进行padding补齐，也就是说设定一个统一长度N，在较短的序列后面填充0到长度为N，如果输入的序列长度大于N，则截取左边长度为N的内容，把多余的直接舍弃。对于那些补零的数据来说，我们的attention机制不应该把注意力放在这些位置上，所以我们需要进行一些处理。具体的做法是，把这些位置的值加上一个非常大的负数(负无穷)，这样经过softmax后，这些位置的权重就会接近0。Transformer的padding mask实际上是一个张量，每个值都是一个Boolean，值为false的地方就是要进行处理的地方。
   * sequence mask: 是为了使decoder不能看见未来的信息。因为Transformer不是rnn结构的，因此我们要想办法在time_step 为 t 的时刻，把 t 时刻之后的信息隐藏起来。具体做法就是产生一个上三角矩阵，上三角的值全为0，把这个矩阵作用在每一个序列上。
   * 对于 decoder 的 self-attention，里面使用到的 scaled dot-product attention，同时需要padding mask 和 sequence mask 作为 attn_mask，具体实现就是两个mask相加作为attn_mask。
     　　其他情况，attn_mask 一律等于 padding mask



5. 所有的attention都是用scaled dot-product的方法来计算的，对于self attention来说，Q=K=V，而对于decoder-encoder attention来说，Q=decoder_input，K=V=memory。
6. 在decode阶段，会先自身和自身的进行attention，自身和自身attention时，会使用上三角矩阵将未来的词进行隐藏，memory为encode阶段最后一层的输出，decode中的每一层的multi head都会拿encode的最后一层的输出进行attention。



# Bert



1、遍历layer的层数，生成12层



（1）bert主要流程是先embedding（包括位置和token_type的embedding），然后调用transformer得到输出结果，其中embedding、embedding_table、所有transformer层输出、最后transformer层输出以及pooled_output都可以获得，用于迁移学习的fine-tune和预测任务；

（2）bert对于transformer的使用仅限于encoder，没有decoder的过程。这是因为模型存粹是为了预训练服务，而预训练是通过语言模型，不同于NLP其他特定任务。在做迁移学习时可以自行添加；

（3）正因为没有decoder的操作，所以在attention函数里面也相应地减少了很多不必要的功能。
