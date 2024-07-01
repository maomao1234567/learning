## Prompt  Engineering
提示词（prompt）是用来微调大模型，通过输入prompt来提高大模型输出的能力，相当于与大模型沟通交流方式。它是来自于GPT-3 提出的In-Context的微调，通过In-Context来进行模型微调。
### prompt learning
是一种使用预训练语言模型的方法，它不会修改模型的参数权重。在这种方法中，模型被给予一个提示（prompt）这个提示是模型输入的一部分，它指导模型产生特定类型的输出。
### In-Context Learning
是指模型在处理一系列输入的时候，使用前面的输入与输出作为后续输入的上下文。

#### Chain-of-Thought (思维链)
https://arxiv.org/pdf/2201.11903
通过在大语言模型里引入COT，让其逻辑推理能力达到更高的水平。
l. 对于小模型来说，CoT Prompting无法带来性能提升，甚至可能带来性能的下降。
2. 对于大模型来说，CoT Prompting涌现出了性能提升。
3. 对于复杂的问题，CoT Prompting能获得更多的性能收益。

#### Self-Consistency(自洽性)
多路径推理
#### Tree-of-Thought(思维树)
利用数的结构来表现大模型的si we
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzODg4MTgxMDEsLTEzNDcwMDM4OTcsLT
E0NTkxODQ2ODIsMjQyMjUxMTY2LC0xOTgxMTQzNzI5LC0yMTQ0
ODEwNTI4LDczMDk5ODExNl19
-->