# commands/

放 slash commands。单文件 `commands/<name>.md`，通过 `/<name>` 触发。

frontmatter 模板（可选）：

```yaml
---
description: <这个命令做啥>
argument-hint: <参数提示>
---
```

正文是命令被触发时塞给 Claude 的 prompt。
