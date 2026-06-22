# CLAUDE.md — 团子 (tuanzi)

> 给 Claude Code 看的项目说明。本项目是一个 Claude Code marketplace plugin。

## 项目性质

这不是一个应用程序，也不是一个库。这是一个 **Claude Code marketplace**，专门用来打包 hao.yang 自用的 skills / agents / commands / output-styles。

任何代码改动的目的都是**让 Claude Code 在加载这个插件后表现更好**，不是让某个最终用户运行业务功能。

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

### 4. Output Styles 规范

- 单文件：`output-styles/<name>.md`
- frontmatter：`name`, `description`
- 正文是完整的 system prompt，定义 Claude 的人设/语气/响应模式

### 5. 元信息同步

- 新增/删除任何 skill/agent/command 后，更新 `README.md` 的内容清单表格
- 大版本变化时同步 `.claude-plugin/plugin.json` 和 `marketplace.json` 的 `version`

## 禁止做的事

- ❌ 不要在仓库里写业务代码（这是工具集合，不是应用）
- ❌ 不要随便重命名已经迁进来的 skill/agent —— 用户可能在其他项目通过名字引用它
- ❌ 不要往 `node_modules`、`dist` 这类目录提交内容 —— 这是配置仓库，没有构建产物
- ❌ 不要把敏感凭据（API key、token）写进任何 .md / .json 文件

## 添加新东西的流程

1. 确定类型（skill / agent / command / output-style）
2. 按上面对应规范创建文件
3. 更新 `README.md` 内容清单
4. （可选）测试：本地通过 `/plugin marketplace add <path>` 安装验证

## 风格偏好（hao.yang 的）

- 文档默认中文
- skill 描述要带触发词
- 简洁优先，不写废话
