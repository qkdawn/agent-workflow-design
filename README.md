# Agent Workflow Design

A skill for designing reliable domain-agent workflows with evidence-driven reasoning, clear tool contracts, and durable handoffs.

面向领域 Agent 的工作流设计技能，围绕证据推理、工具契约与持久化成果交接，支持工作流设计、审查和重构。

## 解决什么问题

当 Agent 过早下结论、工具返回混入建议、上下文被上游长文污染，或多阶段协作无法稳定交接成果时，本技能帮助定位问题所在的层次，并设计对应的改进方式。

从三个问题开始：

1. Agent 替谁解决什么决策问题？
2. 回答问题需要哪些事实、对象和比较关系？
3. 最终交付什么稳定的领域成果，谁会继续使用？

## 核心原则

- **明确职责**：区分领域 Agent、确定性工具、成果库、Harness 与业务编排器。
- **工具返回数据**：保留对象、参数、范围、时间、单位、来源与结果引用；失败不应被改写成业务结论。
- **调查与写作循环**：写作发现证据不足时可以重新调查，新结果回到持久化成果入口。
- **先比较，再判断**：区分事实、比较发现、机制解释与判断，避免围绕先验方向收集支持。
- **按需交接成果**：通过持久化领域结果与按需读取衔接阶段。
- **评价实际质量**：关注事实正确性、证据支持、问题回答、关系发现及运行稳定性。

完整规则与审查清单见 [SKILL.md](SKILL.md)。

## 安装到 Codex

需要 Git。将仓库克隆到 Codex 的用户技能目录；如果设置了 `CODEX_HOME`，请使用该目录下的 `skills`。

### Windows PowerShell

```powershell
$codexRoot = if ($env:CODEX_HOME) { $env:CODEX_HOME } else { Join-Path $HOME '.codex' }
$skillsDir = Join-Path $codexRoot 'skills'
New-Item -ItemType Directory -Path $skillsDir -Force | Out-Null
git clone https://github.com/qkdawn/agent-workflow-design.git (Join-Path $skillsDir 'agent-workflow-design')
```

### macOS / Linux

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
git clone https://github.com/qkdawn/agent-workflow-design.git "${CODEX_HOME:-$HOME/.codex}/skills/agent-workflow-design"
```

如果目标目录中已经安装了同名技能，请先保留已有修改，再决定如何更新；不要直接覆盖。安装后重新启动 Codex，使其加载技能。

其他支持 `SKILL.md` 的 Agent 工具，可按各自的技能目录规范安装；本仓库附带 Codex 界面配置。

## 使用示例

在 Codex 中使用 `$agent-workflow-design` 引用技能，并提供具体的领域问题、现有流程或工具返回样例。

**设计新工作流**

```text
使用 $agent-workflow-design，为产业园选址分析设计 Agent 工作流。
决策对象是候选园区，输入包括项目需求、交通与产业数据，
交付需要包含候选比较、证据引用和推荐理由。请明确各层职责、
工具契约、成果保存方式，以及证据不足时如何回到调查。
```

**审查现有流程**

```text
使用 $agent-workflow-design，审查当前 Agent 的任务提示、工具返回
和阶段交接。重点检查它为什么过早确定方向，以及哪些信息
第一次把无关的限制说明带入了上下文。结合现有代码提出修改建议。
```

**重构成果交接**

```text
使用 $agent-workflow-design，把上游整段报告传给下游的流程
改为持久化成果与按需读取。说明成果标识、查询入口、
来源引用，以及写作补充调查后如何更新成果。
```

## 仓库结构

```text
agent-workflow-design/
├── SKILL.md             # 完整技能指令
├── agents/
│   └── openai.yaml      # Codex 显示名称与默认提示
└── README.md            # 安装与使用说明
```

## 适用范围

本仓库提供设计与审查方法，不包含可独立运行的 Agent 服务、模型运行时或调度系统。使用时应结合实际领域、现有工具和数据来源；已有基座提供的上下文管理、通讯、重试与调度能力应优先复用。
