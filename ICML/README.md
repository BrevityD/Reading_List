# ICML

## (2402.04833) Long Is More for Alignment:  A Simple but Tough-to-Beat Baseline for Instruction Fine-Tuning

简单的准则：长的数据质量比较好。由于先前的工作发现RLHF的奖励可能隐含了优化响应长度，即响应长度可视为实例质量的指标。从几个公开数据集中选择了最长的1000条数据，和GPT挑选的1000条高分数据对比。但是LIMA的平均长度是这篇工作（Refine+Alpaca+1klongest，244.3）的两倍（531.3），而效果不如这篇工作的该baseline，所以，这个结论真的没问题吗？而且Refine比不Refine的效果好、长度低。

接下来用了 EvolInstruct，token长度扩展到了1218.8/687.5，效果最好。但由于有上面LIMA效果差于Refine的情况，只能说明Evol数据集是明显质量高于Alpaca的，不能说明这个高质量一定和token长度有关。

重点说明了（人为强行增加）生成长度对模型性能影响不大（也即模型judge不会偏向更长的答案），
但我个人觉得还存在一个需要确定的问题：token数量一致吗？如果长句的长度是短句的十倍，那是不是需要对比一下确定到底这种质量是长句特征适合学习导致的、还是单纯的token量大了。

这篇文章还没有openreview的forum，看不到审稿细节
提到一个通过噪声增强IFT的工作，NEFTune。
