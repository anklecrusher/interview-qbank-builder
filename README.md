# Interview Qbank Builder

> 通用、多人复用的求职面试题库与口语化自我介绍构建器（Codex Skill）。

在求职面试场景下，通用 AI 往往容易出现**“凭空虚构未做过的项目”、“过度夸大非主导职责”、“生成过于书面化的生硬文字无法口述”**等痛点。本 Skill 专为解决这些问题而设计，通过**事实受控（Fact-Bounded）**机制与**口语化三段论（结论 -> 实例/量化 -> 落到岗位）**，为求职者生成既具备高度现场感、又经得起技术深挖的实战面试资料。

---

## 核心特性

1. **强制前置三要素问询（Pre-Check Gate）**：
   - 绝不预设或假定背景！在生成前，交互式问清：**候选人真实背景**、**目标岗位 JD** 与 **知识库链接（或明确无知识库）**。
2. **严守事实受控红线（Zero-Hallucination）**：
   - 严格区分“独立主导”、“核心攻坚”与“协助协同”，划定面试表达红线，防止面试现场被深挖翻车。
3. **沉稳谦逊的 1 分钟自我介绍**：
   - 控制在 220~280 字（正常语速 60~75 秒内口述完毕），拒绝假大空，聚焦与岗位最契合的经历与业务收益。
4. **20~30 题口语化面试题库**：
   - 覆盖项目技术实战深挖、岗位工作流理解、跨部门抗压协同、求职意向规划 4 大核心维度。
   - 每题均按【考察重点】、【口语化回答（三段论）】与【避坑提示】输出。
5. **高价值反问清单与临场速记卡**：
   - 提炼 3~5 个向面试官提问的高质量业务问题，以及 3 个核心标签与红线提示的临场 Cheat Sheet。

---

## 协作工作流程

```text
[用户发起需求]
      │
      ▼
【第一步：门禁拦截】─────────► 是否齐全（候选人背景 / 目标岗位 JD / 知识库链接）？
      │                       │ 否：先提问补齐三要素（严禁推测）
      │ 是                    ▼
      ▼
【第二步：事实分析】─────────► 梳理事实清单、技能对齐度、划定红线（协助 vs 主导）
      │
      ▼
【第三步：自我介绍】─────────► 沉稳谦逊的一分钟口语化自我介绍（220-280字）
      │
      ▼
【第四步：定制题库】─────────► 20~30 题覆盖实战深挖、业务协同、意愿规划（结构化口语输出）
      │
      ▼
【第五步：反问与速记卡】─────► 高价值业务反问清单 + 临场速记卡（Cheat Sheet）
```

---

## 本地安装（符合约定）

### 推荐方式：Windows 软连接（Junction）

根据工作区规范，请克隆仓库至本地并建立软连接至 Codex Skills 目录：

```powershell
# 1. 克隆项目至指定工作目录（示例）
git clone https://github.com/anklecrusher/interview-qbank-builder.git E:\GitHubWorkspace\own\opensource\interview-qbank-builder

# 2. 在 Codex Skills 目录下建立 Junction 软连接（管理员或开发者模式）
cmd /c mklink /J "C:\Users\<用户名>\.codex\skills\interview-qbank-builder" "E:\GitHubWorkspace\own\opensource\interview-qbank-builder"
```

验证软连接：
```powershell
Get-Item "C:\Users\<用户名>\.codex\skills\interview-qbank-builder" | Select-Object Name, LinkType, Target
```

---

## 目录结构

```text
interview-qbank-builder/
├── SKILL.md                 # 核心 Skill 规则与工作流说明
├── README.md                # 中文使用与部署文档
├── agents/
│   └── openai.yaml          # Codex 技能元数据与界面声明
└── references/
    └── templates.md         # 信息问询话术、事实边界表与三段论标准回答模版
```

---

## 开源协议

MIT License
