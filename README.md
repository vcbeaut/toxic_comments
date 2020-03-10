
文章链接：https://shimo.im/docs/WVtRKVxh9rhvgtgy

## 任务要求
对toxic-comments.csv评论集设计模型，使得模型能够分类出评论是哪种类型。
### 数据格式
图片: https://uploader.shimo.im/f/14y3e2jFxWcdtxMj.png
### 思考
起初没仔细看数据的时候，一位每一句comments只会对应一种类型，那么就是一个简单的多分类模型了。
后来仔细一看，发现每一句comments可能会对应多种类型。并且每个类型的值是0,1.所以这里设计N个2分类模型（N为6）
## 数据预处理
笔者对数据做了一个简单的清洗工作，把不用的id信息去掉，其它字段信息都是有用的。对comment_text去除换行空格等，这些十分容易实现。

笔者在这里遗留下了一个问题：
toxic_comments数据分布是不均匀的，这样一份数据训练模型是会导致模型有偏差性。
所以，对本文的分类任务，在未来的工作中。清洗出均匀数据来提高模型鲁棒性是有必要的。

## 模型设计
笔者直接给出模型图
图片: https://uploader.shimo.im/f/8JDuXiU5zwEaz3DQ.png
Encoding：笔者直接训练Embedding matrix。读者也可以使用Glove，BERT等预训练模型
CLS：各个二分类模型，笔者使用WordAverage，将词向量平均，这是实现了一个简单的baseline。读者可以使用更多RNN,CNN,Transformer等模型来训练。可以参考笔者另外一篇文献（见参考文献部分）
模型训练
笔者使用交叉熵损失函数，计算各个模型的loss，然后将loss相加来做反向传播。

## 实验结果
笔者训练集的accuracy在89%左右，笔者上文提到了一些方案，可以来提高模型鲁棒性，可供读者参考。

## 参考文献
WordAverage/RNN/CNN三种模型情感分类
