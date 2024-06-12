---
{"dg-publish":true,"title":"Agent 的基本概念","dg-created":"2024-06-12T21:28:17.416+08:00","tags":[""],"dg-path":"Agent 的基本概念.md","permalink":"/Agent 的基本概念/","dgPassFrontmatter":true}
---

# Agent 的基本概念

Agent  现在很火，也是一个很有实践价值和前景的课题。现在也有了各种各样的 Agent 的框架和应用，如 MetaGPT, ReAct。不过在深入现在的最新发展之前，需要首先厘清 Agent 自身的定义、概念、框架和模式。

本文内容大纲：
1. Agent 的定义：什么是 Agent
2. Agent 的框架：Agent 的组成成分
3. Agent 的设计模式：Agent 可以按照怎样的思路去设计

## Agent 的定义

首先，什么是 Agent?

>[!cite]
>维基百科上关于 Agent 的解释如下：
>
>In artificial intelligence, an intelligent agent (IA) is an agent acting in an intelligent manner; It perceives its [environment](https://www.zhihu.com/search?q=environment&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22article%22%2C%22sourceId%22%3A%22679032270%22%7D), takes actions autonomously in order to achieve goals, and may improve its performance with learning or acquiring knowledge.
>
>翻译过来就是： Agent 是采取智能行动的行为主体。它能够感知环境，**为了达到一定目的**可以**自主的采取行动**，并且可以通过学习或者获取知识来提高自身性能。
### Agent 与 LLM  的区别
- LLM 不是 Agent, 因为 **Agent 需要有一个目标去达成**。但是**大模型非常适合作为 Agent 的组件**。
- 现在基于大模型的 Agent，实际上的全称应该叫：**LLM-powered autonomous Agent**

## Agent 的框架
LLM-based Agent 框架可以分为4个模块：
1. Profile：标识自身身份
2. Memory：记忆
3. Planning：规划
4. Action：执行

![](https://s1.vika.cn/space/2024/06/12/71ef9653724b4ce09195e2b9d013949a)
## Agent  的设计模式

Andrew Ng 分享了一个框架，用于对 Agent 的设计模式进行分类 [^1]
- Reflection: 检查LLM自己的工作，以提出改进它的方法。
- Tool Use
- Planning
- Multi-agent collaboration

 [^1]: [Four AI Agent Strategies That Improve GPT-4 and GPT-3.5 Performance](https://www.deeplearning.ai/the-batch/how-agents-can-improve-llm-performance/?ref=dl-staging-website.ghost.io)

### Reflection


<div class="transclusion internal-embed is-loaded"><div class="markdown-embed">



# Reflection
[Reflection](https://www.deeplearning.ai/the-batch/agentic-design-patterns-part-2-reflection/?ref=dl-staging-website.ghost.io)
![](https://www.deeplearning.ai/_next/image/?url=https%3A%2F%2Fdl-staging-website.ghost.io%2Fcontent%2Fimages%2F2024%2F03%2FAGENTS-REFLECTION-2.jpg&w=1920&q=75)
 
> Reflection: The LLM examines its own work to come up with ways to improve it.   
> 反思：检查LLM自己的工作，以提出改进它的方法。

<!--section: 4.1.1-->
方式：
- 提示其自己反思
- 提供有助于其评估输出的工具
- 使用多智能体框架

<!--section: 4.1.1.1-->
提示其自己反思：
- 直接用提示指示LLM检查输出的内容，如：
> _Check the code carefully for correctness, style, and efficiency, and give constructive criticism for how to improve it._

- 然后接着提示使用反馈的内容进行改进

<!--section: 4.1.1.2-->
提供工具：
- 通过一些单元测试运行其代码，以检查它是否在测试用例上生成正确的结果
- 搜索 Web 以仔细检查文本输出

<!--section: 4.1.1.3-->
多智能体框架：
- 发现创建两个不同的智能体很方便
	- 一个提示生成良好的输出
	- 另一个提示对第一个智能体的输出提出建设性的批评

<!--section: 4.1.2-->
- “[Self-Refine: Iterative Refinement with Self-Feedback](https://arxiv.org/abs/2303.17651?utm_campaign=The%20Batch&utm_source=hs_email&utm_medium=email&_hsenc=p2ANqtz-9dHVnW1I1bA3sPBbsikjT165Qez3QiiAssknCERwgki818YHG7PyHOQSgg-nxKDa0BuE7B),” Madaan et al. (2023)
- “[Reflexion: Language Agents with Verbal Reinforcement Learning](https://arxiv.org/abs/2303.11366?utm_campaign=The%20Batch&utm_source=hs_email&utm_medium=email&_hsenc=p2ANqtz-9dHVnW1I1bA3sPBbsikjT165Qez3QiiAssknCERwgki818YHG7PyHOQSgg-nxKDa0BuE7B),” Shinn et al. (2023)
- “[CRITIC: Large Language Models Can Self-Correct with Tool-Interactive Critiquing](https://arxiv.org/abs/2305.11738?utm_campaign=The%20Batch&utm_source=hs_email&utm_medium=email&_hsenc=p2ANqtz-9dHVnW1I1bA3sPBbsikjT165Qez3QiiAssknCERwgki818YHG7PyHOQSgg-nxKDa0BuE7B),” Gou et al. (2024)

<!--section: 4.2-->

</div></div>


### Tool Use

<div class="transclusion internal-embed is-loaded"><div class="markdown-embed">



# Tool Use
[Tool Use](https://www.deeplearning.ai/the-batch/agentic-design-patterns-part-3-tool-use/?ref=dl-staging-website.ghost.io)
![](https://www.deeplearning.ai/_next/image/?url=https%3A%2F%2Fdl-staging-website.ghost.io%2Fcontent%2Fimages%2F2024%2F04%2Funnamed---2024-04-03T140654.796-2.png&w=1920&q=75)

<!--section: 4.2.1-->
比如：
- Web 搜索工具：
	`{tool: web-search, query: "coffee maker reviews"}`
- Python 命令
	`{tool： python-interpreter， code： “100 * （1+0.07）**12”}`
- 提示LLM使用上下文，上下文给出了许多函数的详细说明（函数所执行操作的文本说明、所需的参数信息），然后让LLM自己选择正确函数来调用
- 启发式方法：选择当前步骤最相关的自己包含在上下文当中
	- 让人想起，如果有太多的文本无法作为上下文包含，检索增强生成（RAG）系统如何提供启发式方法，以选择要包含的文本子集

<!--section: 4.2.2-->
- “[Gorilla: Large Language Model Connected with Massive APIs](https://arxiv.org/abs/2305.15334?utm_campaign=The%20Batch&utm_source=hs_email&utm_medium=email&_hsenc=p2ANqtz--9ARMthd09q0ABUi-abo6BH62BLbcwPo13LrXs9hUezs-L050Ay7b_rHdWuRIqBVOD6k_S),” Patil et al. (2023)
- “[MM-REACT: Prompting ChatGPT for Multimodal Reasoning and Action](https://arxiv.org/abs/2303.11381?utm_campaign=The%20Batch&utm_source=hs_email&utm_medium=email&_hsenc=p2ANqtz--9ARMthd09q0ABUi-abo6BH62BLbcwPo13LrXs9hUezs-L050Ay7b_rHdWuRIqBVOD6k_S),” Yang et al. (2023)
- “[Efficient Tool Use with Chain-of-Abstraction Reasoning](https://arxiv.org/abs/2401.17464?utm_campaign=The%20Batch&utm_source=hs_email&utm_medium=email&_hsenc=p2ANqtz--9ARMthd09q0ABUi-abo6BH62BLbcwPo13LrXs9hUezs-L050Ay7b_rHdWuRIqBVOD6k_S),” Gao et al. (2024)

<!--section: 4.3-->

</div></div>


### Planning

<div class="transclusion internal-embed is-loaded"><div class="markdown-embed">



# Planning
[Planning](https://www.deeplearning.ai/the-batch/agentic-design-patterns-part-4-planning/?ref=dl-staging-website.ghost.io)
![](https://www.deeplearning.ai/_next/image/?url=https%3A%2F%2Fdl-staging-website.ghost.io%2Fcontent%2Fimages%2F2024%2F04%2Funnamed---2024-04-10T140722.194-1.png&w=1920&q=75)

<!--section: 4.3.1-->
- 许多代理工作流不需要规划
	- 比如：可以让代理以固定次数反映并改进其输出
		- 在这种情况下，代理采取的步骤顺序是固定的和确定的
- 但对于无法提前分解的复杂任务， Planning 允许代理动态决定要执行的步骤

<!--section: 4.3.2-->
关于 Planning 的一些问题：
-  Planning 是很强大的能力
- 但另一方面，其结果难以预测

Andrew Ng 的感受：
>  In my experience, while I can get the agentic design patterns of [Reflection](https://www.deeplearning.ai/the-batch/agentic-design-patterns-part-2-reflection?utm_campaign=The%20Batch&utm_source=hs_email&utm_medium=email&_hsenc=p2ANqtz-8Kh954rkXmE4vgpKvro3Klpjhn7IuT-Y_eXIYtgVIq9PTzwa5zFWX7FZZqv1tuDEEsTDuY) and [Tool Use](http://www.deeplearning.ai/the-batch/agentic-design-patterns-part-3-tool-use/?utm_campaign=The%20Batch&utm_source=hs_email&utm_medium=email&_hsenc=p2ANqtz-8Kh954rkXmE4vgpKvro3Klpjhn7IuT-Y_eXIYtgVIq9PTzwa5zFWX7FZZqv1tuDEEsTDuY) to work reliably and improve my applications’ performance, Planning is a less mature technology, and I find it hard to predict in advance what it will do.
也就是说，按他的经验，Reflection, Tool Use 的设计模式可以可以可靠地工作、提高应用性能，但 Planning 技术仍不太成熟，难以预测结果。不过他相信，随着该领域的快速发展，他相信规划能力会迅速提高

<!--section: 4.3.3-->
- “[Chain-of-Thought Prompting Elicits Reasoning in Large Language Models](https://arxiv.org/abs/2201.11903?utm_campaign=The%20Batch&utm_source=hs_email&utm_medium=email&_hsenc=p2ANqtz-8Kh954rkXmE4vgpKvro3Klpjhn7IuT-Y_eXIYtgVIq9PTzwa5zFWX7FZZqv1tuDEEsTDuY),” Wei et al. (2022)
- “[HuggingGPT: Solving AI Tasks with ChatGPT and its Friends in Hugging Face](https://arxiv.org/abs/2303.17580?utm_campaign=The%20Batch&utm_source=hs_email&utm_medium=email&_hsenc=p2ANqtz-8Kh954rkXmE4vgpKvro3Klpjhn7IuT-Y_eXIYtgVIq9PTzwa5zFWX7FZZqv1tuDEEsTDuY),” Shen et al. (2023)
- “[Understanding the planning of LLM agents: A survey](https://arxiv.org/pdf/2402.02716.pdf?utm_campaign=The%20Batch&utm_source=hs_email&utm_medium=email&_hsenc=p2ANqtz-8Kh954rkXmE4vgpKvro3Klpjhn7IuT-Y_eXIYtgVIq9PTzwa5zFWX7FZZqv1tuDEEsTDuY),” by Huang et al. (2024)

<!--section: 4.4-->

</div></div>


### Multi-agent collaboration

<div class="transclusion internal-embed is-loaded"><div class="markdown-embed">



# Multi-Agent Collaboration
[Multi-Agent Collaboration](https://www.deeplearning.ai/the-batch/agentic-design-patterns-part-5-multi-agent-collaboration/?ref=dl-staging-website.ghost.io)
![](https://www.deeplearning.ai/_next/image/?url=https%3A%2F%2Fdl-staging-website.ghost.io%2Fcontent%2Fimages%2F2024%2F04%2Funnamed---2024-04-17T155856.845-2.png&w=1920&q=75)

<!--section: 4.4.1-->
- 可以通过提示一个LLM（或者，如果您愿意，也可以使用多个LLMs）来执行不同的任务来构建不同的代理
- 这一点很神奇，尽管是在对同一个LLM进行多次调用，但却可以视为使用多个agent的编程抽象(programming abstraction)，Andrew 给出了几个原因分析
	- 有效！
	- 尽管当前一些LLM可以接收很长的输入，但真正理解冗长、复杂的输入的能力参差不齐
		- LLM一次做一件事的效果更好
	- multi-agent 提供了一个抽象，即将复杂任务分解成子任务的组合，这很有用

<!--section: 4.4.2-->
- “[Communicative Agents for Software Development](https://arxiv.org/abs/2307.07924?utm_campaign=The%20Batch&utm_source=hs_email&utm_medium=email&_hsenc=p2ANqtz-8TZzur2df1qdnGx09b-Fg94DTsc3-xXao4StKvKNU2HR51el3n8yOm0CPSw6GiAoLQNKua),” Qian et al. (2023) (the ChatDev paper)
- “[AutoGen: Enabling Next-Gen LLM Applications via Multi-Agent Conversation](https://arxiv.org/abs/2308.08155?utm_campaign=The%20Batch&utm_source=hs_email&utm_medium=email&_hsenc=p2ANqtz-8TZzur2df1qdnGx09b-Fg94DTsc3-xXao4StKvKNU2HR51el3n8yOm0CPSw6GiAoLQNKua),” Wu et al. (2023) 
- “[MetaGPT: Meta Programming for a Multi-Agent Collaborative Framework](https://arxiv.org/abs/2308.00352?utm_campaign=The%20Batch&utm_source=hs_email&utm_medium=email&_hsenc=p2ANqtz-8TZzur2df1qdnGx09b-Fg94DTsc3-xXao4StKvKNU2HR51el3n8yOm0CPSw6GiAoLQNKua),” Hong et al. (2023)

</div></div>

