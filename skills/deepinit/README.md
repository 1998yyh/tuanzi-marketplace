# deepinit Skill

替代 Claude Code 内置 `/init` 命令的深度项目上下文初始化 skill。

## 与内置 /init 的核心差异

| 维度 | 内置 /init | deepinit |
|------|-----------|---------------|
| 输出深度 | 浅层文件结构 + 通用描述 | 架构+环境+约束+测试+病例库 |
| 环境感知 | 无 | NFS/Docker/多机/时区 |
| 约束模型 | 无 | 三层边界（必须/确认/禁止）|
| 测试策略 | 通用提及 | 具体框架+命令+覆盖率 |
| 增量更新 | 覆盖重写 | 差异更新+版本追踪 |
| 反模式过滤 | 会写通用废话 | 严格排除非项目特定内容 |

## 安装

### 方式一：项目级安装（推荐）

复制到项目的 `.claude/skills/` 目录：

```bash
cp -r skills/deepinit /path/to/your/project/.claude/skills/
```

### 方式二：全局安装

需要 sudo（因为全局 skills 目录是 root 权限）：

```bash
sudo cp -r skills/deepinit ~/.claude/skills/
# 或者创建符号链接
sudo ln -s $(pwd)/skills/deepinit ~/.claude/skills/deepinit
```

### 方式三：作为 command 安装

如果更喜欢用 `/deepinit` 命令格式：

```bash
# 项目级
mkdir -p .claude/commands
cp skills/deepinit/SKILL.md .claude/commands/deepinit.md
```

## 使用

在 Claude Code 中直接说：
- "初始化项目"
- "生成 CLAUDE.md"
- "init"

或者直接调用：`/deepinit`

## 目录结构

```
deepinit/
├── SKILL.md                          # 主 skill 文件
├── README.md                         # 本文件
└── references/
    ├── environment-patterns.md       # 环境规范模式库
    ├── boundary-model-guide.md       # 三层边界模型编写指南
    ├── anti-patterns.md              # 反模式（不要写的内容）
    └── problem-library-setup.md      # 病例库系统设置指南
```
