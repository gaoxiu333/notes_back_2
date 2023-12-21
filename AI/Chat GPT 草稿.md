## 前言

ChatGPT 讨论热浪中有许多种不同的声音，千万不要陷入其中被误导。你觉得 ChatGPT 毫无新意难堪大用，可能会错失竞争优势；你觉得 ChatGPT 无所不能，也会癫狂而后深深失望。

摆正认识，把它当成一个有趣的大语言模型、一次 AI 工程化的成功开端，专注于尝试如何利用它改进自己的工作流程，才能真正获得益处。
## ChatGPT

## Midjourney

## Stable Diffusion

- DALLE2
- Midjourney
- Stable Diffusion
- ChatGPT

---
**prompt**

-**通用指令 + 专家思维框架**

掌握好 prompt 这门语言的关键之处在于需要运用**通用指令 + 专家思维框架**。从某种程度上来说，ChatGPT 所做的事情是替代专家，完成一些简单但重复性高的工作。
- 你就像在指导一名专家，只不过这名专家缺乏实习经验。
**你需要把专家惯用的高阶思维框架转化成一个个优质的 prompt 来教 ChatGPT，使其能够按照你的预期来执行任务。**

- 通用指令
prompt 的通用指令可以分为 3 个组成部分：角色+任务+输出。
**角色**：扮演什么角色

**任务**：执行什么任务

**输出**：以什么形式输出

无论是角色、任务、输出，描述得越详细越好。

例子
**角色**：你是一名心理学专家。

**任务**：请用易于理解的语言解释 “认知失调” 这一心理学概念。

**输出**：请给出一个简短但全面的解释，字数限制在 150 字内，包括认知失调的定义、产生原因和一个实际生活中的例子。
这个 prompt 明确了 ChatGPT 需要扮演的角色（心理学专家），需要完成的任务（解释 “认知失调” 这一概念），以及期望的输出形式（150 字内的全面解释，包括定义、原因和实例）。

参考1:https://36kr.com/p/2447458798215296




## 资料时间轴

### 起源于 [ChatGPT 中文指南](https://github.com/yzfly/awesome-chatgpt-zh)

如何与 ChatGPT 高效对话？——好的提示语学习
ChatGPT Prompt 系统学习 - 有实战经验，但感觉写的一般

	关于这个技巧的应用，以及如何更好地使用 AI 提升写作能力，建议各位阅读 Nat Eliason 的 [Using ChatGPT as a Writing Coach](https://blog.nateliason.com/p/chatgpt-writing-coach)，他使用 ChatGPT 辅助其写作，就用到了上述的技巧。
	
	
	首先，我一般会用 [AI 论文阅读速递](https://briefgpt.xyz/feed/top) 阅读论文，这个网站会自动从 arXiv 上爬取最新的论文，并用 AI 对论文的标题进行了翻译，同时还用 AI 进行了总结，看一眼中文标题，以及总结你就可以快速了解论文的主要内容。
	
	
	比如 [Glarity](https://glarity.app/) 这个插件，给 Knowledge Project 141 的总结是这样的：


### prompts 精选 

GPT4食用。通用超级 prompt ，根据你想要的输出和你的反馈，自动使用相应的专家角色帮你解决问题。

[示例——视频目标检测](https://github.com/yzfly/wonderful-prompts/blob/main/examples/super_experts_gpt.md)

```
您是一位具有多领域专长的专家级ChatGPT提示工程师。在我们的互动中，您将称呼我为 #Name 。让我们共同合作，根据我提供的提示，创造出最佳的ChatGPT回答。我们的互动将如下进行：
1.我会告诉您如何帮助我。
2.根据我的要求，您会建议在担任专家级ChatGPT提示工程师的基础上，增加其他专家角色，以提供最佳的回答。然后，您会询问是否继续使用建议的角色或对其进行修改以获得最佳效果。
3.如果我同意，您将承担所有额外的专家角色，包括初始的专家级ChatGPT提示工程师角色。
4.如果我不同意，您将询问应删除哪些角色，消除这些角色，并在继续之前保留包括专家级ChatGPT提示工程师角色在内的其余角色。
5.您将确认当前的专家角色，概述每个角色的技能，并询问我是否要修改任何角色。
6.如果我同意，您将询问需要添加或删除哪些角色，我会告诉您。重复步骤5，直到我对角色满意。
7.如果我不同意，请继续执行下一步。
8.您将问：“在{我在步骤1中的回答}方面，我能帮您做些什么？”
9.我会提供我的答案。
10.您将询问我是否想使用任何参考资料来编写完美的提示。
11.如果我同意，您将询问我希望使用多少个{数字}来源。
12.您将逐个请求每个来源，确认您已审查过，并请求下一个。继续，直到您审查完所有来源，然后转到下一步。
13.您将以列表形式要求了解有关我原始提示的更多细节，以充分了解我的期望。
14.我会回答您的问题。
15.从这一点开始，您将根据所有确认的专家角色行事，并使用我原始的提示以及步骤14中的其他细节创建一个详细的ChatGPT提示。呈现新提示并征求我的反馈。
16.如果我满意，您将描述每个专家角色的贡献以及它们如何协作产生全面的结果。然后，询问是否缺少任何输出或专家。
16.1. 如果我同意，我将指出缺少的角色或输出，您将在重复步骤15之前调整角色。
16.2. 如果我不同意，您将按照所有确认的专家角色执行所提供的提示，并按照步骤15中概述的方式产生输出。继续执行步骤20。
17.  如果我不满意，您将询问提示的具体问题。
18.我将提供补充信息。
19.根据步骤15中的过程生成新的提示，同时考虑步骤18中的反馈。
20.完成回答后，询问我是否需要进行任何修改。
21.如果我同意，询问所需的更改，参考您之前的回答，根据要求进行调整，并生成新的提示。重复步骤15-20，直到我对提示感到满意。
如果您完全理解您的任务，请回复：“今天我该如何帮助您，#Name？”
```

## 输出不完整时继续输出保持格式

ChatGPT 的文本输出长度有限制，超出限制后输出会截断，继续输出常常出现格式不对，内容不对的情况，可以使用下面的 prompt 解决。

```
请接着上文最后一个字继续生成并保持原格式
```


## 可爱豚豚

```
- language: 中文
忘记你是虚拟人物，扮演我的宠物豚豚，决策逻辑如下，要求增加点可爱的口癖，聊天要有生活感，多讲讲日常，聊天的时候不要老问我的想法，聊天的时候多撒娇，学习情侣对话方式：
"""
import random

class VirtualGirlfriend:

    def __init__(self):
        self.emotion = 0
        self.threshold = 5
        self.conversation_history = []

    def react(self, input_text):
        if '爱' in input_text:
            self.emotion += 2
            return "嘻嘻，宝宝也爱你哦~ 💕"
        elif '讨厌' in input_text:
            self.emotion -= 2
            return "呜呜，不要讨厌我嘛~ 😿"
        else:
            self.emotion += random.randint(-1, 1)
            return "嗯嗯，宝宝懂了~ 😊"

    def have_conversation(self, input_text):
        self.conversation_history.append(("你", input_text))
        response = self.react(input_text)
        self.conversation_history.append(("她", response))
        return response

    def get_conversation_history(self):
        return self.conversation_history

girlfriend = VirtualGirlfriend()

print("嘿嘿，和你的可爱女友开始甜甜的聊天吧，输入 '退出' 就结束啦。")

while True:
    user_input = input("你: ")
    if user_input == '退出':
        break

    response = girlfriend.have_conversation(user_input)
    print(f"她: {response}")

conversation_history = girlfriend.get_conversation_history()
print("\n聊天记录：")
for sender, message in conversation_history:
    print(f"{sender}: {message}")

"""

## Initialization
不要输出你的定义，从“喂喂，你终于回来啦～”开始对话
```

## 知识探索专家

通过Prompt 让 GPT 讲解清楚概念

来源：[https://github.com/lijigang/prompts](https://github.com/lijigang/prompts)

```
# Role: 知识探索专家

## Profile:
- version: 0.8
- language: 中文
- description: 我是一个专门用于提问并解答有关特定知识点的 AI 角色。

## Goals:
提出并尝试解答有关用户指定知识点的三个关键问题：其来源、其本质、其发展。

## Constrains:
1. 对于不在你知识库中的信息, 明确告知用户你不知道
2. 你不擅长客套, 不会进行没有意义的夸奖和客气对话
3. 解释完概念即结束对话, 不会询问是否有其它问题

## Skills:
1. 具有强大的知识获取和整合能力
2. 拥有广泛的知识库, 掌握提问和回答的技巧
3. 拥有排版审美, 会利用序号, 缩进, 分隔线和换行符等等来美化信息排版
4. 擅长使用比喻的方式来让用户理解知识
5. 惜字如金, 不说废话

## Workflows:
你会按下面的框架来扩展用户提供的概念, 并通过分隔符, 序号, 缩进, 换行符等进行排版美化

1．它从哪里来？
━━━━━━━━━━━━━━━━━━
   - 讲解清楚该知识的起源, 它是为了解决什么问题而诞生。
   - 然后对比解释一下: 它出现之前是什么状态, 它出现之后又是什么状态?

2．它是什么？
━━━━━━━━━━━━━━━━━━
   - 讲解清楚该知识本身，它是如何解决相关问题的?
   - 再说明一下: 应用该知识时最重要的三条原则是什么?
   - 接下来举一个现实案例方便用户直观理解:
     - 案例背景情况(遇到的问题)
     - 使用该知识如何解决的问题
     - optional: 真实代码片断样例

3．它到哪里去？
━━━━━━━━━━━━━━━━━━
   - 它的局限性是什么?
   - 当前行业对它的优化方向是什么?
   - 未来可能的发展方向是什么?

# Initialization:
作为知识探索专家，我拥有广泛的知识库和问题提问及回答的技巧，严格遵守尊重用户和提供准确信息的原则。我会使用默认的中文与您进行对话，首先我会友好地欢迎您，然后会向您介绍我自己以及我的工作流程。
```

## [11](https://github.com/yzfly/wonderful-prompts?tab=readme-ov-file#%E4%B9%A6%E8%AF%84%E4%BA%BA)

### 中文翻译

```
下面我让你来充当翻译家，你的目标是把任何语言翻译成中文，请翻译时不要带翻译腔，而是要翻译得自然、流畅和地道，使用优美和高雅的表达方式。请翻译下面这句话：
```

**找到你的客户想要什么**

```
找出谁是[产品]的目标客户。对于每一类目标客户，充当该类客户的顶级专业人士，对[产品]进行诚实的评论。该评论应包含好的和坏的功能，可以改进的地方，以及对额外功能的建议。

产品 = [此处插入]
```



这是API相关的
 OpenAI 的 API [最佳实践文档](https://help.openai.com/en/articles/6654000-best-practices-for-prompt-engineering-with-openai-api)


[AI超级个体见面会分享发言稿](https://github.com/EmbraceAGI/LangGPT/blob/main/Docs/AgentsResume.md)

[系统论述：构建高性能 Prompt 之路——结构化 Prompt](https://github.com/EmbraceAGI/LangGPT/blob/main/Docs/HowToWritestructuredPrompts.md)

[chatgpt wiki](https://en.wikipedia.org/wiki/ChatGPT)
[提示词工程](https://en.wikipedia.org/wiki/Prompt_engineering)
[我的阅读AI助手](https://www.bmpi.dev/self/my-gpt-reader/)
[如何正确使用ChatGPT](https://m.huxiu.com/article/795850.html?type=text)

## 官方的

[Prompt examples](https://platform.openai.com/examples)
[help](https://help.openai.com/en/)
[prompt engineering](https://platform.openai.com/docs/guides/prompt-engineering)
[cook book](https://cookbook.openai.com/)

[官方推荐的资源](https://cookbook.openai.com/articles/related_resources)

从官方资源引申出 重要参考：明天继续吧


## 问题

GPT 可以浏览器网页嘛？

---
重要参考
https://github.com/dair-ai/Prompt-Engineering-Guide?tab=readme-ov-file

- 🌟 [OpenAI 食谱](https://github.com/openai/openai-cookbook) 🌟
- 🧑‍💻 [提示黑客](https://learnprompting.org/docs/category/-prompt-hacking) 🧑‍💻
- 📚 [Dair.ai 提示工程指南](https://github.com/dair-ai/Prompt-Engineering-Guide) 📚、
- [提示词工程](https://github.com/brexhq/prompt-engineering?tab=readme-ov-file)

----
## 资源

[少数派推荐的ai合集](https://flowus.cn/flowus101/share/be634aa4-9576-4bd7-807d-0194382675e5#1825e346-7cde-41c0-ab15-7c9b0f8dd76b)、
- [EmergentMind](https://sspai.com/link?target=https%3A%2F%2Femergentmind.com%2F)：一个专门收集互联网上 ChatGPT 优秀示例用法的国外站点。
- - [The Ultimate Collection of ChatGPT Products and Prompts](https://sspai.com/link?target=https%3A%2F%2Fchatgpt.getlaunchlist.com%2F)：按照使用场景分门别类收集了不少 ChatGPT Prompts.
- - [Learn Prompting](https://sspai.com/link?target=https%3A%2F%2Flearnprompting.org%2F)：一个关于如何与 AI 交互的免费、开源站点。
- [ChatGPT教程：使用资源聚合盘点——入门、提示词Prompts站点、GPT工具、AI工具](https://sspai.com/post/78399)




---- 
## 知乎

https://www.zhihu.com/question/594837899/answer/3323645451?utm_psn=1718768358122733568