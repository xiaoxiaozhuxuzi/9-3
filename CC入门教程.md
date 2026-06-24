# Claude Code 入门教程

> 从零开始，掌握 AI 编程助手 Claude Code

---

## 目录

1. [什么是 Claude Code](#1-什么是-claude-code)
2. [安装与配置](#2-安装与配置)
3. [基本使用](#3-基本使用)
4. [核心功能](#4-核心功能)
5. [Slash 命令](#5-slash-命令)
6. [Skills 技能系统](#6-skills-技能系统)
7. [实用技巧](#7-实用技巧)
8. [常见问题](#8-常见问题)

---

## 1. 什么是 Claude Code

Claude Code 是 Anthropic 推出的**终端 AI 编程助手**。它能：

- 读懂你的整个代码库，帮你写代码、改 bug、重构
- 直接操作文件系统、执行命令、管理 Git
- 通过 **Skills（技能）** 系统扩展专业能力
- 在终端中交互，也可以作为 IDE 插件使用（VS Code、JetBrains）

**核心理念**：你描述需求，Claude 帮你实现。

---

## 2. 安装与配置

### 2.1 安装 Claude Code

```bash
# npm 全局安装
npm install -g @anthropic-ai/claude-code

# 或使用 Homebrew (macOS/Linux)
brew install claude-code

# 或直接下载 .deb 包 (Linux)
# 从 https://claude.ai/code 下载
```

### 2.2 获取 API Key

Claude Code 需要 Anthropic API Key 或其他兼容的 API：

1. 访问 [console.anthropic.com](https://console.anthropic.com) 注册并获取 Key
2. 或使用第三方兼容 API（如 DeepSeek 等）

### 2.3 配置

```bash
# 首次运行会自动引导配置
claude

# 或手动编辑配置文件
~/.claude/settings.json
```

配置示例：
```json
{
  "env": {
    "ANTHROPIC_AUTH_TOKEN": "sk-your-api-key",
    "ANTHROPIC_BASE_URL": "https://api.anthropic.com"
  },
  "theme": "dark"
}
```

### 2.4 验证安装

```bash
claude --version   # 查看版本
claude             # 启动交互会话
```

---

## 3. 基本使用

### 3.1 启动会话

```bash
# 在项目目录中启动
cd my-project
claude

# 指定工作目录
claude --dir /path/to/project
```

### 3.2 对话交互

进入 Claude Code 后，直接用自然语言提需求：

```
帮我创建一个 React 登录组件，包含邮箱和密码字段

这段代码有什么问题？如何优化？

为这个函数写单元测试
```

### 3.3 文件操作

Claude 可以直接：
- **读取**文件 — 理解你的代码
- **编辑**文件 — 精确修改
- **创建**文件 — 生成新代码
- **删除**文件 — 清理不需要的内容

所有操作都会先征求你的许可。

### 3.4 命令执行

Claude 可以执行终端命令：

```
npm install lodash        # 安装依赖
git diff                  # 查看改动
npm test                  # 运行测试
```

> 提示：在终端中输入 `! 命令` 可以直接执行，例如 `! npm run build`

---

## 4. 核心功能

### 4.1 代码生成

```
用 TypeScript 写一个防抖函数

帮我写一个 Express API 接口，返回用户列表
```

### 4.2 Debug 与修复

```
这个函数报 "Cannot read property 'map' of undefined"，帮我修

为什么这段代码运行很慢？帮我优化
```

### 4.3 代码审查

```
/ review    # 审查当前 PR
/ code-review   # 审查当前改动
```

Claude 会检查：
- 逻辑错误
- 安全隐患
- 性能问题
- 代码风格

### 4.4 Git 操作

```
帮我写一个清晰的 commit message

创建一个 PR 描述

git rebase 到 main 分支
```

### 4.5 重构

```
把这个类组件改成函数组件 + hooks

把 CSS 提取成独立文件，用 CSS Modules
```

---

## 5. Slash 命令

在 Claude Code 中，以 `/` 开头可以调用特殊命令：

| 命令 | 功能 |
|------|------|
| `/help` | 显示帮助 |
| `/clear` | 清空对话 |
| `/doctor` | 诊断环境问题 |
| `/init` | 初始化 CLAUDE.md |
| `/compact` | 压缩上下文 |
| `/review` | 审查 PR |
| `/simplify` | 代码简化优化 |
| `/code-review` | 代码审查 |
| `/memory` | 管理持久记忆 |
| `/config` | 打开配置 |
| `/plugin` | 管理插件 |
| `/loop` | 定时重复执行 |
| `/workflows` | 查看后台任务 |

---

## 6. Skills 技能系统

### 6.1 什么是 Skills

Skills 是 Claude Code 的**专业能力扩展包**。每个 skill 都是一个包含专业指令的目录，让 Claude 在特定领域表现更出色。

### 6.2 安装 Skills

```bash
# 从 GitHub 安装（官方方式）
npx skills add <owner/repo>@<skill-name>

# 或手动放置到
~/.claude/skills/<skill-name>/SKILL.md
```

### 6.3 常用 Skills

| Skill | 用途 |
|-------|------|
| `skill-creator` | 创建新的 skill |
| `find-skills` | 搜索在线 skill 库 |
| `frontend-design` | 前端设计指南 |
| `mcp-builder` | 构建 MCP 服务器 |
| `web-artifacts-builder` | 构建 Web 应用 |
| `xlsx` / `docx` / `pdf` / `pptx` | 办公文档处理 |

### 6.4 创建自己的 Skill

```bash
# 使用 skill-creator
# 在 Claude Code 中说: "帮我创建一个 xxx 的 skill"
```

---

## 7. 实用技巧

### 7.1 CLAUDE.md

在项目根目录创建 `CLAUDE.md`，写入项目关键信息，Claude Code 每次启动都会自动读取：

```markdown
# CLAUDE.md
## 项目简介
一个 React + TypeScript 的电商项目

## 常用命令
- `npm run dev` 启动开发服务器
- `npm test` 运行测试

## 技术栈
React 18, TypeScript, Tailwind CSS, Zustand
```

### 7.2 使用记忆功能

```
/memory    # 让 Claude 记住你的偏好、项目约定等
```

### 7.3 多任务并行

Claude Code 可以同时处理多个独立任务 — 例如同时审查代码和修复 bug：

```
帮我在后台审查 PR #42，同时修一下登录页的样式问题
```

### 7.4 工作树隔离

对于破坏性大的改动，使用工作树：

```
在隔离环境中尝试重构数据库层
```

### 7.5 状态栏配置

在 `~/.claude/settings.json` 中配置状态栏：

```json
{
  "statusLine": {
    "type": "command",
    "command": "..."
  }
}
```

### 7.6 快捷键

| 键 | 功能 |
|----|------|
| `↑` / `↓` | 切换历史命令 |
| `Tab` | 自动补全文件路径 |
| `Ctrl+C` | 取消当前操作 |
| `Ctrl+O` | 查看完整历史 |

---

## 8. 常见问题

### Q: 提示 "Auto-update failed" 怎么办？

运行 `/doctor` 诊断，或手动更新：
```bash
npm update -g @anthropic-ai/claude-code
```

### Q: API 调用失败？

检查 `~/.claude/settings.json` 中的 `ANTHROPIC_AUTH_TOKEN` 和 `ANTHROPIC_BASE_URL` 是否正确。

### Q: 上下文不够用？

- 使用 `/compact` 压缩对话历史
- 将大型文档放到 `CLAUDE.md` 中
- 大文件操作时分段处理

### Q: 如何控制权限？

在 `~/.claude/settings.json` 中配置 `permissions` 字段，可以允许/禁止特定操作。

### Q: 支持哪些模型？

Claude Code 支持 Anthropic 全系列模型及其他兼容 API：
- Claude Opus（最强推理）
- Claude Sonnet（速度与质量平衡）
- Claude Haiku（最快最经济）
- 第三方兼容模型

---

## 附录：学习资源

- 官方文档：[docs.anthropic.com/claude-code](https://docs.anthropic.com/claude-code)
- Skills 市场：[skills.sh](https://skills.sh)
- GitHub：[github.com/anthropics/claude-code](https://github.com/anthropics/claude-code)

---

> 🍅 本文档由 Claude Code 生成 | 更新于 2026.06.24
