# Agent Workflow Design

帮助 Agent 围绕实际任务获取信息、形成有依据的判断，并在需要时继续补查。

## 核心内容

- 获取足够的信息：按问题选择方法，支持补读、分页和聚合。
- 交接后继续工作：保留对象、口径、条件与来源，完整依据可继续读取。
- 形成有依据的判断：区分事实、发现、解释和方案，检查推导是否成立。
- 验证实际改善：检查结果质量，并通过行为对照检验规则修改。

完整指令见 [SKILL.md](SKILL.md)。

## 安装

将本仓库克隆到用户技能目录：

Windows PowerShell：

```powershell
$skillRoot = if ($env:CODEX_HOME) { Join-Path $env:CODEX_HOME 'skills' } else { Join-Path $HOME '.codex/skills' }
git clone https://github.com/qkdawn/agent-workflow-design.git (Join-Path $skillRoot 'agent-workflow-design')
```

macOS / Linux：

```bash
git clone https://github.com/qkdawn/agent-workflow-design.git "${CODEX_HOME:-$HOME/.codex}/skills/agent-workflow-design"
```

目标目录已有同名技能时，先保留本地修改再更新。

本技能沿用 Karpathy Guidelines 的通用工作原则。请同时安装 `karpathy-guidelines`，置于同级技能目录；本仓库不复制它的内容。

## 使用

```text
使用 $agent-workflow-design，检查这个 Agent 为什么遗漏关键依据、
交接后重复调查或从事实直接跳到方案。结合实际输入和输出提出修改，
并说明如何用同一任务验证改善。
```

本仓库提供设计指导，不包含 Agent 运行时或调度服务。
