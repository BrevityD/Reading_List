# EMNLP

## Quality Matters: Evaluating Synthetic Data for Tool-Using LLMs

用两种方法评估训练模型使用外部工具的数据的可靠性。第一种是使用人定义的直观的评判标准；第二种是使用模型驱动的上下文评测。后者评估一个数据实例对上下文学习的帮助。

第一种：认为一个数据实例具有高质量：需要讨论query和API调用序列，一共六个属性。
query要有以下属性：specificity、coherence、solvability
API调用序列要满足以下属性：Parameter alignment、Sufficiency、Minimality
少量手动标注了一些pair，逐个属性query了GPT，值得一提的是，直接query让GPT回答是否满足属性是不行的。需要逐个属性进行属性问题的变换（多数是变换成抽取任务）。这种GPT自动评估和手动标注结果是高度一致的。

第二种ICE：由于*最近的学习在上下文学习和微调之间发现了联系，指明LM在上下文学习时隐式的实现了梯度下降*。于是把要评估的实例作为上下文示例，查看这个示例对结果的影响（和gt的levenshtein距离），以这作为数据可靠性的评估。

尽管从混淆矩阵来看，两种方法相关性有限，但在微调结果来看，第二种是对第一种的有效补充。