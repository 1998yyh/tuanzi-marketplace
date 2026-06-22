# hooks/

放 hook 脚本和配置。结构示例：

```
hooks/
├── hooks.json           # hook 注册配置
└── scripts/
    └── <script-name>.js
```

`hooks.json` 示例：

```json
{
  "PostToolUse": [
    {
      "matcher": "Edit",
      "hooks": [
        {
          "type": "command",
          "command": "node hooks/scripts/post-edit.js"
        }
      ]
    }
  ]
}
```

可用事件：`PreToolUse` / `PostToolUse` / `Stop` / `SubagentStop` / `UserPromptSubmit` 等。
