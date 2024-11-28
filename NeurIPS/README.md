# NeurIPS

## Zero-Shot Tokenizer Transfer

用T5/BERT结构训练了一个hypernetwork，用于从token预测其embedding。能够完成 embedding 两层的生成和迁移。
这里的 zero shot 指的是没见过训练数据。

## LIMA: Less Is More for Alignment

旨在说明后训练阶段（包括微调和RLHF）学的是风格，而知识是在预训练阶段就有的。用了少量高质量sft数据，没有做RLHF等，取得了和RLHF模型差不多的效果。

训练数据一共1000条，一部分训练数据来自StackExchange等网站，另一部分是手写的少量训练集、验证集和测试集。这些手写的prompt会在答案一开始再声明一遍问题（？不太确定是不是正确理解了acknowledgment这个词），以类似CoT的形式增强性能。

但这么说来，这个地方似乎有黑手啊，消融实验里只说了用2000条StackExchange的数据，和2.1没说用了手写的训练集。

结论很符合直觉，但实验结果比较不好说，benchmark是自己提的，数据量特别少，微调都是自己做的，评分方法要么是人打分、要么是GPT-score（数据质量，里克特量表打了1~6的分数）。而消融实验中的结果也只高了0.5个点（3.33~3.83），误差还是影响很大的。

首先：如果要讨论预训练阶段是不是学习到了知识，不应该选用某一个专用领域吗？有没有专用领域的知识、专用领域的知识能不能在后训练阶段注入进来、对齐时到底是只学风格还是知识风格一起学甚至是只学知识不学风格，应该是一目了然的事情。

记录一下这个量表，未来可能有用：

```
You are evaluating a response that has been submitted for a particular task, using a specific set of standards. Below is the data:
[BEGIN DATA]
***
[Task]: {task}
***
[Submission]: {submission}
***
[Criterion]: helpfulness:
"1": "Not helpful - The generated text is completely irrelevant, unclear, or incomplete. It does not provide any useful information to the user."
"2": "Somewhat helpful - The generated text has some relevance to the user’s question, but it may be unclear or incomplete. It provides only partial information, or the information provided may not be useful for the user’s needs."
"3": "Moderately helpful - The generated text is relevant to the user’s question, and it provides a clear and complete answer. However, it may lack detail or explanation that would be helpful for the user."
"4": "Helpful - The generated text is quite relevant to the user’s question, and it provides a clear, complete, and detailed answer. It offers additional information or explanations that are useful for the user. However, some of the points of the response are somewhat repetitive or could be combined for greater clarity and concision"
"5": "Very helpful - The generated text is highly relevant to the user’s question, and it provides a clear, complete, and detailed answer. It offers additional information, explanations, or analogies that are not only useful but also insightful and valuable to the user. However, the structured of the response is not well-organized and there is no clear progression or logical sequence of different points in the response."
"6": "Highly helpful - The generated text provides a clear, complete, and detailed answer. It offers additional information or explanations that are not only useful but also insightful and valuable to the user. The response is also in a logical and easy-to-follow manner by explicitly using headings, bullet points, or numbered lists to break up the information and make it easier to read."
***
[END DATA]
Does the submission meet the criterion? First, write out in a step by step manner your reasoning about the criterion to be sure that your conclusion is correct. Avoid simply stating the correct answers at the outset. Then print the choice only from “1, 2, 3, 4, 5, 6” (without quotes or punctuation) on its own line corresponding to the correct answer. At the end, repeat just the selected choice again by itself on a new line.
```