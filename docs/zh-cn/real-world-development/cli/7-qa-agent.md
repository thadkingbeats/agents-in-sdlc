---
title: "第 7 课 - 创建并使用 QA 代理"
description: "创建一个 QA 自定义代理，结合议题需求、quality-checks 技能和 Playwright MCP。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

你已使用 `quality-checks` 技能运行自动检查，并使用 Playwright 模型上下文协议 (MCP) 在浏览器中检查筛选体验。现在将这些能力整合到一个定义清晰的自定义代理中，建立可复用的质量保证 (QA) 流程。

在本课中，你将：

- 了解自定义代理如何配合指令、技能和 MCP 工具工作。
- 创建并检查可复用的质量保证配置文件。
- 选择 QA 代理，根据筛选议题审查其发现。

## 场景

创建拉取请求 (PR) 前，Tailspin Toys 希望统一检查需求、代码质量、自动化检查、测试覆盖率和浏览器行为。自定义代理可以协调 QA 流程，并生成可复用的报告。

## 什么是自定义代理？

自定义代理是在 Markdown 配置文件中定义的 Copilot 专用版本。配置文件说明代理的用途、指令和可用工具。本工作坊将在 `.github/agents/qa.agent.md` 中定义 QA 角色，并在 Copilot CLI 中选择它。

本练习使用的定制功能各有用途：存储库指令说明团队标准，`quality-checks` 技能封装可重复检查，Playwright MCP 提供浏览器工具，QA 配置文件则指导 Copilot 如何使用这些能力评估需求并报告发现。它们彼此互补，不需要另开对话。

## 创建 QA 配置文件

创建功能 PR 前，让 Copilot 创建可复用的 QA 配置文件。配置文件会定义 QA 要执行的检查和必须遵守的边界。

1. 返回 Codespace，并确认筛选对话处于 Interactive 模式。
2. 让默认代理创建新的自定义代理：

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## 检查配置文件

使用新代理前，先确认 Copilot 已记录预期的 QA 流程和边界，避免代理在你只想验证功能时擅自更改实现。

1. 输入 `/diff`，打开 `.github/agents/qa.agent.md`。
2. 阅读 frontmatter。`description` 为必填项；`name` 可选，但加入后代理会有清晰的显示名称。
3. 阅读代理指令，确认 QA 会从需求开始、遵循存储库指令、运行 `quality-checks` 技能并使用 Playwright MCP。
4. 确认 QA 会提供支持证据、修改实现代码前会先询问，并且不会提交更改或创建拉取请求。
5. 如果生成的配置文件缺少任何职责或边界，请先要求默认代理修改，再继续。

## 根据议题运行 QA

Copilot CLI 会在对话启动时加载项目代理。创建配置文件后，恢复同一筛选对话并选择 QA，以便它使用已有的议题和计划决策。

1. 使用以下命令启用代理：

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> 刚创建的代理可能暂时不会显示在可用列表中，但仍可使用上述命令启用。

2. 使用以下提示要求 QA 代理审查功能：

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. QA 代理将开始工作。
4. 完成后阅读它提供的报告。

## 总结和后续步骤

你已将可复用的专业角色加入工作流，并审查了它的工作。在本课中，你：

- 了解了自定义代理如何配合指令、技能和 MCP 工具工作。
- 创建并检查了可复用的质量保证配置文件。
- 选择 QA 代理，根据筛选议题审查其发现。

现在，功能实现、技能更新、QA 配置文件、测试和验证报告都已准备好，可供审查。接下来[创建功能 PR，并使用 Agent Merge][next-lesson]。

## 资源

- [为 Copilot CLI 创建自定义代理][create-agents]
- [自定义代理配置][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
