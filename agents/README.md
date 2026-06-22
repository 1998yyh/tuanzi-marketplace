# agents/

放 Claude Code subagents。单文件：

```
agents/<agent-name>.md
```

frontmatter 模板：

```yaml
---
name: <agent-name>
description: <什么场景下应该被调度>
tools: [Read, Edit, Bash]   # 可选，限定可用工具
model: sonnet                # 可选: haiku / sonnet / opus
---
```
