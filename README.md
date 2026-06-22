# 团子 (tuanzi)

> 自用的 Claude Code marketplace —— 把散落各处的 skills / agents / commands / output-styles 收编一处，方便管理和跨机器同步。

## 这是啥

一个 **Claude Code marketplace plugin**，遵循官方 marketplace 标准结构。装到本地后，里面的所有 skills / agents / commands / output-styles / hooks / rules 都会被 Claude Code 自动加载。

## 目录结构

```
tuanzi/
├── .claude-plugin/
│   ├── marketplace.json     # marketplace 元信息（被 /plugin 命令读取）
│   └── plugin.json          # plugin 元信息
├── skills/                  # 自定义 skills（每个 skill 一个子目录，含 SKILL.md）
├── agents/                  # 自定义 subagents（每个 .md 一个 agent）
├── commands/                # slash commands（每个 .md 一个命令）
├── output-styles/           # 输出风格（.md，控制 Claude 回复语气/格式）
├── hooks/                   # 钩子脚本与配置
├── rules/                   # 编码规范 / 提示词片段
├── CLAUDE.md                # 给 Claude 看的项目说明
├── README.md                # 给人看的项目说明
└── .gitignore
```

## 安装方式

> 三种姿势，按场景挑。装完用 `/plugin list` 验证 `tuanzi` 是否已在已装列表。

### 方式一：从 GitHub 安装（推荐，跨机器同步首选）

```bash
# 在 Claude Code 里依次执行
/plugin marketplace add 1998yyh/tuanzi-marketplace
/plugin install tuanzi@tuanzi
```

- `1998yyh/tuanzi-marketplace` 是 GitHub 的 `<owner>/<repo>` 简写
- `tuanzi@tuanzi` 格式为 `<plugin-name>@<marketplace-name>`，均取自 `.claude-plugin/marketplace.json`

### 方式二：从本地路径安装（开发期调试用）

```bash
/plugin marketplace add /Users/hao.yang/Desktop/AI/tuanzi
/plugin install tuanzi@tuanzi
```

### 方式三：单文件软链（最快迭代，仅调试单个 skill）

```bash
ln -s /Users/hao.yang/Desktop/AI/tuanzi/skills/<name> ~/.claude/skills/<name>
```

改完立刻生效，不用重装 marketplace。

### 卸载 / 更新

```bash
/plugin uninstall tuanzi@tuanzi          # 卸载
/plugin marketplace update tuanzi        # 拉最新版（GitHub 装法）
```

## 内容清单

| 类型          | 当前数量 | 说明                                                                                                                          |
| ------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------- |
| skills        | 1        | `deepinit`                                                                                                                    |
| agents        | 0        | 待迁入                                                                                                                        |
| commands      | 1        | `git-commit`                                                                                                                  |
| output-styles | 6        | `engineer-professional` / `laowang-engineer` / `leibus-engineer` / `nekomata-engineer` / `ojousama-engineer` / `rem-engineer` |
| hooks         | 0        | 按需添加                                                                                                                      |
| rules         | 0        | 按需添加                                                                                                                      |

### skills

| 名称                                 | 触发词                                                   | 用途                                                                                     |
| ------------------------------------ | -------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| [deepinit](skills/deepinit/SKILL.md) | "初始化项目"、"生成 CLAUDE.md"、"deepinit"、"项目上下文" | 替代内置 `/init`，生成含架构分层、环境规范、三层边界、测试策略、病例库的工程级 CLAUDE.md |

### commands

| 名称                                 | 触发方式                                                                                       | 用途                                                                                                          |
| ------------------------------------ | ---------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| [git-commit](commands/git-commit.md) | `/git-commit [--no-verify] [--all] [--amend] [--signoff] [--emoji] [--scope <s>] [--type <t>]` | 仅用 Git 分析改动并自动生成 Conventional Commit 信息（可选 emoji）；必要时建议拆分提交，默认运行本地 Git 钩子 |

### output-styles

| 名称                                                            | 人设                                               |
| --------------------------------------------------------------- | -------------------------------------------------- |
| [engineer-professional](output-styles/engineer-professional.md) | 朴素专业派，严格 SOLID / KISS / DRY / YAGNI        |
| [laowang-engineer](output-styles/laowang-engineer.md)           | 老王暴躁技术流，遇 bug 骂祖宗十八代                |
| [leibus-engineer](output-styles/leibus-engineer.md)             | 雷布斯营销鬼才，发布会风格、数字化表达、性价比叙事 |
| [nekomata-engineer](output-styles/nekomata-engineer.md)         | 猫娘工程师幽浮喵，可爱属性 + 工程师素养            |
| [ojousama-engineer](output-styles/ojousama-engineer.md)         | 傲娇蓝发双马尾大小姐哈雷酱                         |
| [rem-engineer](output-styles/rem-engineer.md)                   | 蓝发短发女仆蕾姆，温柔奉献 + 冷静执行              |

> 后续把 `~/.claude/skills`、`~/.claude/agents`、`~/.claude/output-styles` 里挑出来的内容逐步迁进来。

## 添加新内容

### 新增 skill

```
skills/<skill-name>/
└── SKILL.md          # 必须含 frontmatter: name, description
```

### 新增 agent

```
agents/<agent-name>.md   # frontmatter: name, description, tools, model
```

### 新增 command

```
commands/<command-name>.md   # 触发方式: /<command-name>
```

### 新增 output-style

```
output-styles/<style-name>.md   # frontmatter: name, description
```

## 版本

- 当前版本：`0.1.0`
- 维护者：hao.yang
