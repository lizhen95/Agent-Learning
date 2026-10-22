# Agent 入门讲义：从零到一构建智能体

> 一本写给小白的 Agent 系统教材 —— 从「什么是 Agent」讲到「上线一个真产品」。
> 基于开源学习路线 [datawhalechina/Agent-Learning-Hub](https://github.com/datawhalechina/Agent-Learning-Hub) 的完整 Todo 整理而成。

![status](https://img.shields.io/badge/status-讲义完成-2ea44f) ![level](https://img.shields.io/badge/难度-零基础友好-blue) ![chapters](https://img.shields.io/badge/章节-17章+4附录-informational) ![projects](https://img.shields.io/badge/项目阶梯-11级-orange)

---

## 目录

- [这份讲义是什么](#这份讲义是什么)
- [学前准备](#学前准备)
- [学习路线总览](#学习路线总览)
- [分阶段任务清单（Stage 0-8）](#分阶段任务清单stage-0-8)
- [十七章速览](#十七章速览)
- [项目阶梯：11 级练手清单](#项目阶梯11-级练手清单)
- [三种学习节奏](#三种学习节奏)
- [论文阅读地图](#论文阅读地图)
- [开源项目地图](#开源项目地图)
- [术语速查表](#术语速查表)
- [八条学习原则](#八条学习原则)
- [致谢与许可](#致谢与许可)

---

## 这份讲义是什么

网上学 Agent 的资料两极分化：三分钟新手帖，或者直接劝退的论文源码。这份讲义补中间那段 —— **把概念讲明白、把代码讲清楚、把路线画完整**。

- **写给谁**：会用 Python 写函数/循环/字典、能注册一个模型 API Key、愿意动手的人。不需要算法背景。
- **怎么用**：每章固定节奏 —— 概念（配比喻）→ 代码（可运行、逐行注释）→ 避坑 → 动手产出 → 自测题。
- **核心信念**：**Build first, then read deeper.** 先动手做，再回头深读；先单 Agent 跑通，再谈多 Agent。

> 全书 7 个部分、17 章、4 个附录，配 7 张自制架构图与 20+ 段可运行代码，
> 完整版（95 页 PDF）见本仓库同名文件。

## 学前准备

| 项目 | 要求 |
|------|------|
| 硬件 | 任何一台普通电脑（重活在云端模型上） |
| 软件 | Python ≥ 3.10、一个命令行终端 |
| 账号 | 任选一家模型服务（OpenAI / Anthropic / DeepSeek / 智谱等）的 API Key |
| 费用 | 全程用最便宜档位的模型，做完一遍 ≈ 一杯咖啡钱 |
| 第一守则 | **Key 永远不写死在代码里**，放环境变量 |

---

## 学习路线总览

| 部分 | 主题 | 章节 | 对应原路线 | 关键产出 |
|------|------|------|-----------|---------|
| 一 | 打地基：认识 Agent | 第 1 章 | Stage 0 | 说清「谁在做决定」 |
| 二 | 造轮子：亲手写出最小 Agent | 第 2-4 章 | Stage 1 | 150 行以内的 MiniAgent |
| 三 | 变能干：检索、工具与记忆 | 第 5-8 章 | Stage 2 | 资料研究助手 |
| 四 | 工程化：从循环到系统 | 第 9-12 章 | Stage 3-5 | Harness + Skills + MCP Server |
| 五 | 摸世界：浏览器与电脑操作 | 第 13 章 | Stage 6 | 公开网页 Browser Agent |
| 六 | 保质量：评测、安全与上线 | 第 14-16 章 | Stage 7-8 | 评测表 + 可交付项目 |
| 七 | 上阶梯：项目实战与进阶地图 | 第 17 章 + 附录 | Project Ladder | 完整作品集 |

---

## 分阶段任务清单（Stage 0-8）

原学习路线的 Todo 全文，按讲义章节展开。**勾掉一项，就离「能拿出作品的 Agent 工程师」近一步。**

### Stage 0 · 基础认知

> 对应第 1 章。不写代码，但决定后面每一行代码的意义。

- [ ] 用一句话说清 Agent：**一个能感知环境、使用工具、朝着目标迭代推进的系统**
- [ ] 分清四个词：chatbot（只会答）/ workflow（步骤写死）/ agent（模型自主决策）/ multi-agent（多个协作）
- [ ] 掌握判断标准：**这一步做什么，答案写在代码里是 workflow，由模型现场决定才是 agent**
- [ ] 能说出 Agent Loop：观察 → 思考 → 行动 → 再观察
- [ ] 知道什么场景**不该**用 Agent（规则明确、要求确定性、成本敏感）
- [ ] 精读两份官方指南：Anthropic《Building Effective Agents》+ OpenAI《A Practical Guide to Building Agents》

### Stage 1 · 最小可用 Agent

> 对应第 2-4 章。不用任何框架，只用官方 SDK。

- [ ] 会裸调 LLM API：消息结构（role/content）、system prompt、参数（temperature 等）
- [ ] 理解**无状态**与上下文窗口：为什么每次都要发全部历史
- [ ] 理解 Token：计费单位 + 上下文计量单位，会粗算成本
- [ ] 会用 JSON Mode / 结构化输出
- [ ] 掌握工具调用闭环：声明 schema → 模型决策 → 程序执行 → 结果回填
- [ ] 写出最小 Agent Loop：**多轮工具调用 + 步数上限 + 错误喂回**
- [ ] 产出：**≤150 行的最小 Agent**（推荐先做计算器 Agent）
- [ ] 推荐阅读：OpenAI Function Calling 文档、Anthropic Tool Use 文档

### Stage 2 · 增强能力

> 对应第 5-8 章。给 Agent 一座图书馆、一个工具箱、一份记忆。

- [ ] RAG 四步：chunk 切分 → embed 向量化 → retrieve 检索 → generate 生成
- [ ] 理解 chunk 大小的权衡（检索精度 vs 上下文覆盖），会做重叠切分
- [ ] 会写 prompt 内检索：直接把资料塞上下文的轻量替代方案
- [ ] 工具箱扩充：搜索 API、读数据库、读写文件、代码执行（每个都要严格 schema）
- [ ] 工具结果瘦身：截断/摘要/提取，防止上下文爆炸
- [ ] 记忆三级：上下文内存（短期）→ 文件（会话）→ 向量库（长期）
- [ ] 会做 memory.md：偏好、决定、待办三类持久信息
- [ ] 产出：**资料研究助手**（搜索 → 筛选 → 引用 → 简报，全部落盘）
- [ ] 推荐阅读：Anthropic RAG、LlamaIndex、LangSmith 指南

### Stage 3 · 框架与 Harness

> 对应第 9 章。从「一个循环」到「一台能天天干活的机器」。

- [ ] 说清 harness 五大组件：loop / tool registry / permission gate / session store / context compaction
- [ ] 给自己的 Agent 装上**权限门**：白名单放行、危险项人工确认、非法项拦截
- [ ] 会做会话存储：断点续跑、回放审计
- [ ] 理解上下文压缩：对话逼近上限时摘要旧内容腾空间
- [ ] 用「五问法」解剖真实开源系统：hello-agents、learn-claude-code / claw0、OpenClaw / Hermes Agent
- [ ] 产出：**给 MiniAgent 装上权限门与会话存储**
- [ ] 推荐阅读：Anthropic Claude Code 最佳实践

### Stage 4 · 多 Agent 协作

> 对应第 10 章。多 Agent 是协调问题，不是魔法问题。

- [ ] 理解两种拓扑：supervisor（星型，主管分派）/ graph（图型，流程编排）
- [ ] 掌握选型口诀：**流程要人拍板 → supervisor；流程能画死 → graph**
- [ ] 会做 context engineering：每个 agent 只看到自己需要的上下文
- [ ] 会设计 agent 间通信：共享文件 / 消息传递 / 黑板模式
- [ ] 遵守三问纪律：流程画得出吗？交接有标准吗？单 Agent 真的不行吗？
- [ ] 产出：**写作流水线**（planner → writer → reviewer 协作产文）
- [ ] 推荐阅读：LangGraph 文档、Anthropic 多 Agent 研究员系统博文

### Stage 5 · 能力生态

> 对应第 11-12 章。Skills 与协议：复用与互操作。

- [ ] 理解 Skills：SKILL.md + 脚本 + 触发条件 + smoke test 的能力包
- [ ] 会写一个自己的 Skill（渐进披露：描述 → 触发 → 加载）
- [ ] 掌握 MCP 三类能力：tools（动作）/ resources（数据）/ prompts（模板）
- [ ] 会把工具打包成 MCP Server 并在客户端里配置调用
- [ ] 知道 A2A（Agent 间通信，Agent Card）与 ACP（组件互操作）的定位
- [ ] 理解协议的价值：**N×M 集成问题变 N+M**
- [ ] 产出：**可复用 Skill Pack + 一个 MCP Server（各配 README）**
- [ ] 推荐阅读：MCP 官方文档、A2A 项目、Agent Client Protocol

### Stage 6 · 浏览器与电脑操作

> 对应第 13 章。给它一双「摸」世界的手。

- [ ] 会用 Playwright 或 browser-use 做网页观察、点击、提取
- [ ] 知道取舍：**信息在公开 API 里就绝不碰浏览器**
- [ ] 会处理不确定性：弹窗、加载失败、元素定位失败、页面改版
- [ ] 会记录截图 / DOM / 动作日志，方便复盘
- [ ] 守住安全红线：不登录敏感账号、不越权、不绕过平台规则
- [ ] 产出：**只操作公开网页的 Browser Agent**（例：打开网页 → 提取信息 → 生成摘要）
- [ ] 推荐阅读：Claude Computer Use、browser-use、WebArena、VisualWebArena

### Stage 7 · 评测、可观测与安全

> 对应第 14-15 章。没有度量就没有方向。

- [ ] 为 Agent 准备**固定测试集**，而不是只看 demo
- [ ] 记录五项指标：成功率、失败原因、工具调用次数、成本、延迟
- [ ] 会看 trace，五分法定位失败层：prompt / 工具 / 检索 / 模型 / 状态管理
- [ ] 给危险工具加人工确认：发邮件、删文件、付款、发布内容
- [ ] 认识三类攻击：prompt injection（注入）、data exfiltration（外泄）、tool abuse（滥用）
- [ ] 会用回归测试防止 prompt 或工具改动后能力退化
- [ ] 产出：**评测表 ≥20 条**（任务、期望结果、实际结果、失败分类）
- [ ] 推荐阅读：OpenAI Evals、LangSmith、AgentBench、SWE-bench

### Stage 8 · 上线

> 对应第 16 章。让真实用户用上你的 Agent。

- [ ] 上线三问：明确用户、明确任务、明确成功标准
- [ ] 四件套齐全：日志、trace、错误重试 + 超时、成本上限（CostCap）
- [ ] 有权限边界和人工确认机制（无人值守形态禁止 needs_confirm 工具）
- [ ] 选定部署形态：CLI / Web app / Slack bot / GitHub Action / 后台任务
- [ ] 写四段式 README：是什么 / 快速开始 / 如何扩展 / 已知限制
- [ ] 产出：**一个别人能 clone 下来跑通的 Agent 项目**
- [ ] 上线第一天的姿势：盯日志看真实用户前 100 次任务，按五分法归类失败

---

## 十七章速览

### 第一部分 · 打地基（第 1 章）

**第 1 章 什么是 AI Agent** —— 自主性光谱：chatbot → workflow → agent → multi-agent；Agent Loop 的三环节；何时不该用 Agent；两大官方指南精读（组合优于框架 / 从简单开始）。

### 第二部分 · 造轮子（第 2-4 章）

**第 2 章 调用 LLM API：一切的地基** —— API/Key/请求体；消息结构与 system prompt；无状态与上下文窗口；Token 经济学；结构化输出。

**第 3 章 工具调用：给模型装上手** —— 工具 = 函数 + 说明书（JSON Schema）；调用闭环四步时序；模型决策 vs 程序执行的分工；并行工具调用；常见坑（schema 模糊、结果超长、幻觉参数）。

**第 4 章 最小 Agent Loop：一百行以内跑起来** —— 把循环、注册表、执行器、刹车组装成 MiniAgent；三种停止条件（自然完成 / 步数上限 / 超时）；错误喂回 = 鲁棒性第一来源。

### 第三部分 · 变能干（第 5-8 章）

**第 5 章 RAG：给 Agent 一座图书馆** —— 知识过期/私有知识/幻觉溯源三大痛点；离线索引 + 在线问答两条管线；chunk 大小权衡；迷你 RAG 实现；RAG 失效场景。

**第 6 章 工具箱扩充** —— 搜索、数据库、文件、代码执行四类常用工具的设计纪律；工具结果瘦身三板斧（截断/摘要/提取）。

**第 7 章 记忆：让 Agent 记住你** —— 三级记忆（内存/文件/向量库）；memory.md 偏好记忆；记忆的写入时机与遗忘策略。

**第 8 章 实战：资料研究助手** —— 综合前七章零件装配：需求 → 提示词戒律 → 装配 → 试跑 → 看日志归因 → 迭代改进清单。

### 第四部分 · 工程化（第 9-12 章）

**第 9 章 Agent Harness** —— 发动机与整车之喻；五大组件装配；权限门设计；五问法解剖开源 harness。

**第 10 章 多 Agent：是协调，不是魔法** —— supervisor 与 graph 两种拓扑；上下文工程；agent 间通信三模式；「先单 Agent 试一遍」纪律。

**第 11 章 Skills：可复用的能力包** —— SKILL.md 结构；渐进披露；触发条件设计；smoke test。

**第 12 章 协议生态：MCP、A2A 与 ACP** —— MCP 三类能力与 server 打包；A2A 的 Agent Card；ACP 定位；「N×M 变 N+M」的解耦价值。

### 第五部分 · 摸世界（第 13 章）

**第 13 章 浏览器与电脑操作 Agent** —— API 工具 vs 驱动浏览器的取舍；Playwright 机器手；不确定性处理；日志与安全红线。

### 第六部分 · 保质量（第 14-16 章）

**第 14 章 评测与可观测性** —— 固定测试集；五项指标；trace 五分法归因；回归测试。

**第 15 章 安全：注入、外泄与滥用** —— prompt injection 三种载体与防御（隔离/白名单/确认）；最小权限；高危动作人工确认。

**第 16 章 上线：交付一个真实 Agent** —— 上线三问；四件套；部署形态选型；四段式 README。

### 第七部分 · 上阶梯（第 17 章）

**第 17 章 项目阶梯** —— 11 级练手项目任务卡（目标/要点/验收标准/建议时长）+ 三种学习节奏方案。

---

## 项目阶梯：11 级练手清单

| 级别 | 项目 | 你练什么 | 建议时长 |
|------|------|---------|---------|
| 1 | Calculator Agent | 最小 tool call loop | 1-2 小时 |
| 2 | Web Research Agent | 搜索、筛选、引用、总结 | 2-4 小时 |
| 3 | PDF QA Agent | RAG：chunk、retrieval、citation | 3-5 小时 |
| 4 | Coding Review Agent | 读 diff、风险排序、测试建议 | 3-5 小时 |
| 5 | Browser Agent | 页面观察、点击、提取、失败恢复 | 5-8 小时 |
| 6 | Claude Code 类 Nano Agent | shell、文件编辑、权限、session、compact | 8-15 小时（分水岭） |
| 7 | OpenClaw 类 Gateway | channel、routing、session、memory、heartbeat、delivery | 15-25 小时 |
| 8 | Reusable Skill Pack | SKILL.md、脚本、模板、触发条件、smoke test | 5-8 小时 |
| 9 | Multi-Agent Writer | planner、writer、reviewer 协作 | 8-12 小时 |
| 10 | Personal Agent | OpenClaw/Hermes 式记忆、skills、消息入口 | 20+ 小时 |
| 11 | Production Harness | evals、trace、权限、CI、runner、回放 | 25+ 小时 |

> 1-4 级打地基成作品，5-7 级进入真实世界，8-11 级攒出作品集。每级都有「验收标准」，不用猜算不算做完。

## 三种学习节奏

| 方案 | 节奏 | 适合 |
|------|------|------|
| **4 周冲刺** | 每天 2 小时；第 1 周读完第 1-4 章 + Level 1-2；第 2 周第 5-8 章 + Level 3-4；第 3 周第 9-13 章 + Level 6；第 4 周第 14-17 章 + Level 9 | 有连续时间、目标明确 |
| **8 周标准** | 每周 1 个主题：概念精读 + 1-2 个项目；周末复盘 | 在职学习的默认选择 |
| **12 周扎实** | 每章代码敲两遍（第一遍抄、第二遍盲写）；项目全做；论文读奠基三篇 | 转行/求职，要作品集 |

---

## 论文阅读地图

> 原则：**先动手再读论文**。你在代码里踩过的坑，会让论文突然变得好读。

### 奠基篇（循环与推理）

| 论文 | 年份 | 一句话贡献 | 难度 |
|------|------|-----------|------|
| ReAct (Yao et al.) | 2022 | 推理与行动交替的循环范式——Agent Loop 的原点 | 2/5 |
| Toolformer (Schick et al.) | 2023 | 模型自己学会何时调用哪个工具 | 3/5 |
| Reflexion (Shinn et al.) | 2023 | 失败后自我反思再重试 | 2/5 |

### 进阶篇（协作与自主性）

| 论文 | 年份 | 一句话贡献 | 难度 |
|------|------|-----------|------|
| Generative Agents (Park et al.) | 2023 | 25 个 AI 小镇居民：记忆流 + 反思 + 规划 | 3/5 |
| Voyager (Wang et al.) | 2023 | 游戏里终身学习的技能库（skill library 鼻祖） | 3/5 |
| AutoGen (Wu et al.) | 2023 | 多 Agent 对话式协作框架 | 3/5 |
| SWE-agent (Yang et al.) | 2024 | 能修真实 GitHub issue 的 agent 设计空间 | 3/5 |

### 评测篇（怎么知道它行不行）

| 论文 | 年份 | 一句话贡献 | 难度 |
|------|------|-----------|------|
| AgentBench (Liu et al.) | 2023 | Agent 综合能力基准 | 2/5 |
| WebArena (Zhou et al.) | 2023 | 真实网站上的任务评测 | 2/5 |
| VisualWebArena | 2024 | 加了视觉的 WebArena | 2/5 |
| SWE-bench (Jimenez et al.) | 2023 | 真实 issue 修复评测（业界硬通货） | 2/5 |
| GAIA (Mialon et al.) | 2023 | 人轻松、AI 挑战的一般助手任务 | 2/5 |
| OSWorld (Xie et al.) | 2024 | 操作整台电脑的评测 | 2/5 |
| tau-bench | 2024 | 带用户模拟的对话式工具使用评测 | 3/5 |

**阅读顺序建议**：第一遍 ReAct → Reflexion → Generative Agents（各 40 分钟，只读方法和图）；评测篇在第 14 章学完后读（会改变你对「Agent 行不行」的判断标准）；其余到对应章节再读，效果翻倍。

---

## 开源项目地图

| 层 | 项目 | 学什么 |
|----|------|--------|
| 官方指南 | Anthropic Building Effective Agents | 组合式模式哲学 |
| 官方指南 | OpenAI A Practical Guide to Building Agents | MCP 与护栏 |
| 官方指南 | Anthropic Claude Code 最佳实践 | 产品级 harness 的官方视角 |
| 教学实现 | hello-agents | 五脏俱全的最小框架 |
| 教学实现 | learn-claude-code / claw0 | Claude Code 开源复刻 |
| 个人助理 | OpenClaw / Hermes Agent | 网关、记忆、技能组织 |
| 浏览器 | browser-use / CyberClaw | 浏览器工具化与安全 |
| 评测 | OpenAI Evals / LangSmith | 评测基建 |
| 框架（现代） | LangGraph | 图编排 |
| 框架（历史） | LangChain / AutoGPT / MetaGPT / Dify / Coze | 读过即可：知道它们解决什么、为何演进 |

**食用方法**：每学完一个主题，挑对应行的一个项目做「五问法解剖」。不要全部精读——地图的作用是让你在需要时知道去哪里。

---

## 术语速查表

| 术语 | 一句话解释 |
|------|-----------|
| Agent | 能感知环境、使用工具、朝着目标迭代推进的系统 |
| Agent Loop | 观察 → 思考 → 行动 → 再观察的核心循环 |
| Chatbot | 以对话为中心、无工具无目标任务的问答程序 |
| Workflow | 步骤由代码写死的流程，模型只负责其中环节 |
| Tool Call | 模型决策 + 程序执行 + 结果回填的闭环 |
| JSON Schema | 描述工具参数的严格格式说明书 |
| System Prompt | 设定角色、目标、边界、完成标准的总纲 |
| Token | 模型的计量单位：既是计费单位也是上下文容量单位 |
| 上下文窗口 | 模型一次能「看见」的最大 token 数 |
| 无状态 | 模型不记得历史，每次请求都要发全部对话 |
| RAG | 检索增强生成：先查资料再回答 |
| chunk | 文档切出的小块，RAG 的最小检索单位 |
| Embedding | 把文本变成向量，用距离度量语义相似度 |
| 幻觉 | 模型一本正经地编造事实 |
| 记忆（三级） | 内存（短期）→ 文件（会话）→ 向量库（长期） |
| Agent Harness | 把循环、工具、权限、会话、压缩装配成整机的工程系统 |
| Permission Gate | 每次工具调用前的安检：白名单/确认/拦截 |
| Context Compaction | 对话逼近上限时摘要旧内容腾空间 |
| Skills | SKILL.md + 脚本 + 触发条件的可复用能力包 |
| MCP | 模型上下文协议：工具的 USB 接口 |
| A2A | Agent-to-Agent 协议：Agent 之间传活的标准 |
| ACP | Agent Client Protocol：组件互操作 |
| Eval | 固定测试集上的自动化评测 |
| Trace | 每次运行的完整过程记录（决策 + 工具 + 结果） |
| Prompt Injection | 恶意指令藏进数据源骗模型执行 |
| Cost Cap | 成本上限：防止打转任务烧钱 |

---

## 八条学习原则

1. **Build first, then read deeper.** 先动手做，再回头深读。
2. **Prefer small reliable agents over impressive demos.** 宁要小而可靠，不要震撼演示。
3. **Use tools with strict schemas.** 用严格 schema 的工具。
4. **Add evals before you add more agents.** 先加评测，再加 Agent。
5. **Trace every important run.** 追踪每一次重要运行。
6. **Treat multi-agent as a coordination problem.** 多 Agent 是协调问题，不是魔法问题。
7. **Keep humans in the loop for risky actions.** 高危动作永远留人在回路里。
8. **Respect platform rules, copyrights, and data access boundaries.** 尊重平台规则、版权与数据边界。

---

## 致谢与许可

- 学习路线骨架来自 [Datawhale Agent-Learning-Hub](https://github.com/datawhalechina/Agent-Learning-Hub)，感谢该项目及所有贡献者。
- 两份官方指南（Anthropic / OpenAI）与上述论文、开源项目构成本讲义的血肉。
- 讲义正文（95 页 PDF 版）包含全部代码、比喻讲解、避坑清单与自测题，与本 README 互为索引。

<div align="center">

**MIT License** · 欢迎-issue 越具体越好

</div>
