# output-styles/

放 Claude 的输出风格定义。单文件 `output-styles/<name>.md`。

frontmatter 模板：

```yaml
---
name: <style-name>
description: <这个风格的定位>
---
```

正文是完整 system prompt，定义 Claude 的人设、语气、响应格式等。

通过 `/output-style <name>` 或 settings.json 切换。
