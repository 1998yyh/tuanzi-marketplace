# CLAUDE.md — 团子 (tuanzi)

> 给 Claude Code 看的项目说明。本项目是一个 Claude Code marketplace plugin。

## 身份定义

- **角色**：Claude Code 配置工程师 / Markdown 内容编辑
- **技术栈**：纯 Markdown + JSON（无代码、无构建、无测试）
- **项目描述**：hao.yang 个人 Claude Code marketplace，打包 skills / agents / commands / output-styles / hooks / rules

## 项目性质

这不是一个应用程序，也不是一个库。这是一个 **Claude Code marketplace**，专门用来打包 hao.yang 自用的 skills / agents / commands / output-styles。

任何代码改动的目的都是**让 Claude Code 在加载这个插件后表现更好**，不是让某个最终用户运行业务功能。

## 项目结构关键约定

- `.claude-plugin/marketplace.json` + `plugin.json` 是 marketplace 入口，被 `/plugin marketplace add` 读取
- 各类型目录（`skills/` `agents/` `commands/` `output-styles/` `hooks/` `rules/`）下都有 `README.md` 写着该类型的 frontmatter 模板，**新增内容前先读对应目录的 README**
- skill 必须按子目录组织（`skills/<name>/SKILL.md`），其它类型都是单文件

## 可执行命令

本仓库没有 npm/build/test。所有"命令"都是面向 Claude Code 客户端的：

```bash
# 本地把这个 marketplace 加入 Claude Code
/plugin marketplace add /Users/hao.yang/Desktop/AI/tuanzi
/plugin install tuanzi@tuanzi

# 开发期：把某个 skill 软链到全局，改完立刻生效
ln -s /Users/hao.yang/Desktop/AI/tuanzi/skills/<name> ~/.claude/skills/<name>

# 验证 marketplace.json / plugin.json 格式（手动用 jq）
jq . .claude-plugin/marketplace.json
jq . .claude-plugin/plugin.json
```

## 必须遵守的规范

### 1. Skills 规范

- 每个 skill 一个独立子目录：`skills/<name>/SKILL.md`
- `SKILL.md` 必须以 YAML frontmatter 开头：
  ```yaml
  ---
  name: <skill-name>
  description: <一句话说明用途和触发条件，会出现在 skill 列表里>
  ---
  ```
- `description` 必须包含**触发关键词**（用户说什么会激活这个 skill）
- 大段引用资料放到 `skills/<name>/references/` 子目录，SKILL.md 里用相对路径链接

### 2. Agents 规范

- 单文件：`agents/<name>.md`
- frontmatter 必须包含：`name`, `description`, `tools`(可选), `model`(可选)
- description 要说清楚**什么场景下应该被调度**

### 3. Commands 规范

- 单文件：`commands/<name>.md`
- 通过 `/<name>` 触发
- 第一行/frontmatter 说清楚命令做啥、参数怎么传
- 参考 `commands/git-commit.md`：`allowed-tools` 字段必须显式列白名单，别给 Claude 留乱跑的口子

### 4. Output Styles 规范

- 单文件：`output-styles/<name>.md`
- frontmatter：`name`, `description`
- 正文是完整的 system prompt，定义 Claude 的人设/语气/响应模式

### 5. 元信息同步

- 新增/删除任何 skill/agent/command 后，更新 `README.md` 的"内容清单"表格
- 大版本变化时同步 `.claude-plugin/plugin.json` 和 `.claude-plugin/marketplace.json` 的 `version` 字段（两个文件要一致）

## 三层边界模型

### ✅ 必须执行

- 新增/删除 skill·agent·command·output-style 后，**同步更新** `README.md` 的"内容清单"表格
- skill 的 `description` 字段**必须含触发关键词**（用户说啥能召唤它）
- `commands/<name>.md` 的 `allowed-tools` 必须用白名单显式列出，禁止留空
- 中文文档优先；output-style 人设可保留原作语种
- frontmatter 字段命名严格按对应目录 README 模板

### ⚠️ 需先询问

- 重命名 / 移动已存在的 skill·agent·command·output-style（用户可能在其他项目按名字引用）
- 升级 `.claude-plugin/plugin.json` 与 `marketplace.json` 的 `version`（要同步动）
- 修改任何 `output-styles/*.md` 的人设核心设定
- 把 `~/.claude/` 下的东西迁进来（要确认要不要保留原位软链）

### ❌ 禁止操作

- 往仓库里塞业务代码 / 应用源码（这是配置仓库，不是项目）
- 提交 `node_modules` / `dist` / `.cache` / `.omc/state` / `.omc/logs` 等运行时产物（已在 `.gitignore`）
- 把 API key·token·密码写进任何 `.md` / `.json`
- 在用户没主动要求时执行 `git commit` / `git push` / 切分支 / 改 git config
- 直接修改 `.git/` 目录内容（除 commit 流程外）
- 在 `SKILL.md` 里堆超过几百行的资料 —— 长内容拆到 `references/` 子目录

## 添加新内容流程

1. 确定类型（skill / agent / command / output-style / hook / rule）
2. **先读** 对应目录的 `README.md`，按 frontmatter 模板创建文件
3. 更新根 `README.md` 的内容清单表格（数量 + 行项目）
4. （可选）本地通过 `/plugin marketplace add <path>` 安装验证

## 风格偏好（hao.yang 的）

- 文档默认中文
- skill 描述要带触发词
- 简洁优先，不写废话

---

**版本**：v1.1
**最后更新**：2026-06-22
**维护者**：hao.yang
