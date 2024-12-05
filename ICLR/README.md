# ICLR

## (2405.02774) GET MORE FOR LESS: PRINCIPLED DATA SELECTION  FOR WARMING UP FINE-TUNING IN LLMS

由于标注数据获取比较耗时花钱，所以首先用无标注的数据预微调模型，然后进行微调。在2.7B的模型上有效。先前工作的主要问题是选择和目标分布完全匹配的样本，忽略了预训练的分布，导致一些已经被充分训练过的样本被重复选择。数据效率低。

这里对无标注数据的选择策略主要是优先考虑能最有效的使预训练分布更接近目标数据分布的样本（使用Optimal Transport Distance，计算OT对偶解得到距离梯度）