---
title: phidata 一个超强的构建Agent的大模型框架.md
author: 老章 mlpy
date: 2024-10-27 14:10:00 +0800
categories: [AIGC]
tags: [aigc]
render_with_liquid: false
---


大家好，我是章北海

向大家推荐一个超强的构建Agent的大模型框架——Phidata

Phidata是一个用于构建智能Agent系统的Python框架。

它让你可以方便地创建具有记忆力、知识、工具使用能力和推理能力的AI助手,并将其作为一个完整的软件应用运行(包括数据库、向量数据库、API等)。

同时phidata还提供了对Agent系统的监控、评估和优化功能。

使用phidata,你可以:

- 构建拥有记忆、知识、工具使用和推理能力的智能Agent。Phidata会管理Agent的状态、记忆和知识,存储在数据库中。  
- 将这些Agent作为一个完整的软件应用运行,包括数据库、向量数据库和API接口。Phidata会管理所需的基础设施,支持本地和云端(BYOC)。
- 监控、评估和优化你的Agent系统。Phidata会记录会话日志,监控关键指标,帮助你洞察和改进系统。

Phidata虽然支持所有语言模型,但官方示例主要使用OpenAI的模型。只要设置好OpenAI的API key,就可以直接使用。
![](https://r2blog.zhanglearning.com/2024/10/12ad505ceee4f5462b551fe8158d4d01.png)

下面是一些使用phidata构建Agent的示例:
![](https://r2blog.zhanglearning.com/2024/10/96d4b32e211a679cdbe58ab76f530a66.png)

### 网页搜索Agent

这个Agent可以在网上搜索信息来回答问题。核心代码如下:

```python
from phi.agent import Agent  
from phi.model.openai import OpenAIChat
from phi.tools.duckduckgo import DuckDuckGo

web_agent = Agent(
    name="Web Agent",  
    role="Search the web for information",
    model=OpenAIChat(id="gpt-4o"),
    tools=[DuckDuckGo()], 
    markdown=True,
    show_tool_calls=True,
)
web_agent.print_response("Whats happening in France?", stream=True)
```

通过组合OpenAI的语言模型和DuckDuckGo搜索引擎,就可以创建一个可以在网上查找信息的Agent。当询问它"法国最近发生了什么",它会通过搜索引擎查找相关新闻,再用自然语言回答。

### 金融数据Agent  

这个Agent专门用于查询金融数据,核心代码:

```python
from phi.agent import Agent
from phi.model.openai import OpenAIChat  
from phi.tools.yfinance import YFinanceTools

finance_agent = Agent(
    name="Finance Agent",
    role="Get financial data", 
    model=OpenAIChat(id="gpt-4o"),
    tools=[YFinanceTools(stock_price=True, analyst_recommendations=True, company_info=True, company_news=True)],
    instructions=["Always use tables to display data"],
    markdown=True, 
    show_tool_calls=True,
)
finance_agent.print_response("Share analyst recommendations for NVDA", stream=True)
```

它使用yfinance库获取金融数据,当询问"分享NVDA股票的分析师评级"时,它会查询相关数据,并以表格的形式展示分析师的评级信息。

### Agent协作

Phidata还支持多个Agent协同工作,解决更复杂的问题。比如我们可以让上面的网页搜索Agent和金融数据Agent组成一个团队:

```python
agent_team = Agent(
    team=[web_agent, finance_agent], 
    show_tool_calls=True,
    markdown=True,
)
agent_team.print_response("Research the web for NVDA and share analyst recommendations", stream=True)  
```

当询问"在网上搜索NVDA公司的信息,并分享分析师的评级",这个Agent团队会先用网页搜索Agent查找NVDA公司的背景信息,再用金融数据Agent获取分析师评级,最后整合成完整的回答。

### 基于知识库的Agent

普通的Agent每次都需要将所有的背景知识放入prompt中,但这样会占用大量token。phidata的RAG(Retrieval Augmented Generation)Agent可以将背景知识存入向量数据库,每次只检索最相关的少量知识,大大节省token用量,还能提高回答质量。

下面的例子展示了如何从一个菜谱PDF文件创建知识库,构建一个美食问答Agent:

```python
from phi.agent import Agent
from phi.model.openai import OpenAIChat
from phi.knowledge.pdf import PDFUrlKnowledgeBase  
from phi.vectordb.lancedb import LanceDb, SearchType

db_uri = "tmp/lancedb"
# Create a knowledge base from a PDF
knowledge_base = PDFUrlKnowledgeBase(
    urls=["https://phi-public.s3.amazonaws.com/recipes/ThaiRecipes.pdf"], 
    # Use LanceDB as the vector database
    vector_db=LanceDb(table_name="recipes", uri=db_uri, search_type=SearchType.vector),  
)
# Load the knowledge base: Comment out after first run
knowledge_base.load(upsert=True)

agent = Agent(
    model=OpenAIChat(id="gpt-4o"),
    # Add the knowledge base to the agent  
    knowledge=knowledge_base,
    show_tool_calls=True,
    markdown=True,
)
agent.print_response("How do I make chicken and galangal in coconut milk soup")
```

当询问"如何制作椰汁鸡肉汤",Agent会从知识库中检索鸡肉汤的菜谱,再根据菜谱步骤回答问题。这样不仅节省token,回答的质量也更高。

### 其他功能

除了上述核心功能,phidata还提供了:

- 本地和云端的基础设施管理
- 会话日志记录和指标监控 
- 本地调试模式
- 结构化输出支持,可以强制Agent以特定格式(比如表格、JSON等)输出
- 内置的playground应用,可以方便地与Agent聊天互动

Phidata目前仍在快速迭代中,欢迎大家在GitHub上贡献代码,或在Discord社区中交流讨论。

总之,phidata是一个功能强大,涵盖全流程的智能Agent开发框架。对于想要快速构建和部署聊天机器人、智能助手、问答系统等AI应用的开发者非常友好,值得尝试!