# Interview Qbank Builder

> 通用、多人复用的求职面试题库与口语化自我介绍构建器（Codex Skill）。

本 Skill 面向不同候选人与岗位，生成事实受控、谦逊口语化、能够直接练习的面试材料。它会在构建题库前强制确认候选人背景、目标岗位 JD 和知识库链接，并使用 agent-reach 调用小红书检索对应岗位的公开面经与高频题目。

## 核心能力

- 三要素前置门禁：候选人背景、目标岗位 JD、知识库或事实材料链接（或明确无知识库）。
- 小红书岗位面经检索：根据公司、岗位和行业生成检索词，提取高频题型、追问主题和面试风格信号。
- 登录失败即暂停：若小红书登录态过期、缺少 a1 Cookie、Session expired 或搜索渠道不可用，Skill 不会继续生成题库，而是先等待用户完成登录。
- 事实受控：小红书内容只用于决定“问什么”，不用于证明候选人“做过什么”。
- 口语化三段论：结论先行 -> 真实案例或量化 -> 落到岗位。
- 完整交付：一分钟自我介绍、20~30 道题库、可能追问、避坑提示、反问清单和临场速记卡。

## 标准工作流

1. 确认候选人背景、目标岗位 JD 和知识库链接。
2. 调用 agent-reach 执行 xhs status 和 xhs whoami。
3. 如果认证失败，暂停并等待用户完成小红书登录。
4. 认证通过后，用 xhs search 搜索岗位面经与高频题，必要时用搜索结果 URL 调用 xhs read 或 xhs comments。
5. 整理外部样本信号，保留来源与覆盖限制。
6. 基于候选人事实、JD 和面经信号生成题库。

## 小红书检索规则

1. 至少覆盖公司+岗位面试、岗位面试题、公司面经、行业或技术方向高频题等查询变体。
2. 需要读详情时使用搜索结果 URL 或带上下文的 ID，不能使用裸 note_id。
3. 保持低频请求，通常每次间隔 2~3 秒；遇到验证码或风控时停止批量抓取。
4. 不复制整篇笔记，不保存 Cookie、Token 或完整 JSON。
5. 多条内容重复出现的主题才标记为高频；单条内容标记为单样本线索。
6. 小红书公开经验与候选人真实背景必须分开呈现。

## 登录失败时的用户交互

当认证检查失败时，Skill 应明确回复：

> 小红书登录态未通过，题库生成已暂停。请先在浏览器中完成小红书扫码或登录，完成后回复“已登录”。我会重新检查 xhs status 和 xhs whoami，通过后再继续检索和生成题库。

不要要求用户粘贴 Cookie、Token 或浏览器存储内容。用户确认后，从认证检查重新开始，不要假设之前的登录已经生效。

## 题库中的面经摘要

题库正文前增加“小红书检索摘要”，至少包含：

- 使用过的查询词；
- 代表性笔记标题和 URL（如工具返回）；
- 多条样本重复出现的高频题型；
- 仅单条内容出现的线索；
- 面试轮次、追问方式和技术深度信号；
- 登录状态、搜索覆盖范围和失败限制。

小红书内容属于外部公开样本，不能覆盖候选人简历、工作日志或知识库中的事实。

## 目录结构

interview-qbank-builder/
├── SKILL.md
├── README.md
├── agents/
│   └── openai.yaml
└── references/
    ├── templates.md
    └── xhs-search.md

## 本地软连接安装

按工作区约定，源码应位于 E:\GitHubWorkspace，运行入口使用 Junction 指向原件目录：

    git clone https://github.com/anklecrusher/interview-qbank-builder.git E:\GitHubWorkspace\own\opensource\interview-qbank-builder
    cmd /c mklink /J "C:\Users\<用户名>\.codex\skills\interview-qbank-builder" "E:\GitHubWorkspace\own\opensource\interview-qbank-builder"

验证：

    Get-Item "C:\Users\<用户名>\.codex\skills\interview-qbank-builder" | Select-Object Name, LinkType, Target

应看到 LinkType 为 Junction，且目标指向 E 盘原件仓库。不要在 .codex\skills 中复制一份实体 Skill 内容。

## 开源协议

MIT License
