# skills/

放 Claude Code skills。每个 skill 一个子目录：

```
skills/
└── <skill-name>/
    ├── SKILL.md         # 必需，含 frontmatter (name, description)
    └── references/      # 可选，存大段引用资料
```

frontmatter 模板：

```yaml
---
name: <skill-name>
description: <一句话说清用途和触发关键词>
---
```
