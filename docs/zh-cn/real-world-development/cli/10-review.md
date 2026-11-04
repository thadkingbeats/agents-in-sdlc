---
title: "第 10 课 - 总结与后续步骤"
description: "回顾 Copilot CLI 工作流、两个拉取请求、可复用定制项和更多资源。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

你通过 GitHub Copilot CLI 完成了一套连续的 Tailspin Toys 工作流。你：

- 准备了 Codespace、安装 Copilot CLI、探索项目并找到预先创建的筛选议题。
- 添加星级评分，在转发的浏览器中检查结果，并手动合并第一个拉取请求 (PR)。
- 从筛选议题开始，在 Plan 模式中确定方案、在 Autopilot 模式中构建，并在 Interactive 模式中审查。
- 使用自定义指令引导代理，自定义现有 `quality-checks` 技能，并使用它运行单元测试、lint 和类型检查。
- 添加 Playwright 模型上下文协议 (MCP) 服务器，并用它在真实浏览器中探索筛选功能。
- 创建并选择质量保证 (QA) 自定义代理，评估需求、覆盖范围、技能结果和浏览器证据。
- 审查完整的筛选更改，并授权 Agent Merge 合并筛选 PR。
- 探索用于管理上下文、模型、共享和可选云端委派的斜杠命令。

## 你交付的内容

本工作坊包含两个 PR 阶段，每个阶段都基于更新后的 `main` 创建独立分支：

1. **星级评分：** 在游戏卡片上显示现有的 `starRating`，并明确显示尚未评分的状态。
2. **筛选和质量工作流：** 实现筛选、更新指令并将其应用于功能、自定义 `quality-checks` 报告、创建 QA 配置文件并添加相关测试。

从规划筛选功能到创建其 PR，你一直使用同一对话和分支。为了简化工作坊，这些工作合并到一个 PR 中。

## 不同类型的验证

你通过多种方式检查代码：自动化测试、亲自在浏览器中检查，以及使用 MCP 让 Copilot 在浏览器中探索。`quality-checks` 技能运行单元测试、lint 和类型检查，并按新格式报告结果。QA 汇总这些结果，并在创建 PR 前审查需求和测试覆盖范围。

新增测试应解决实际覆盖缺口；QA 运行后无需添加测试也可能是正确结果。授权合并前请审查代码和证据；代码更改后应重新生成受影响的证据。

## 最佳实践

提供给 Copilot 的上下文和工具会影响它的工作。在本工作坊中，你更新了指令、自定义了技能、创建了 QA 配置文件并配置 MCP 服务器。可以在多个对话中复用这些定制项，并根据团队需要进行调整。指令定义标准，技能描述可重复任务，自定义代理定义专业角色，MCP 服务器连接外部工具。请审查实际更改和工具结果，而不只是代理摘要。

根据任务选择**模式和模型**。先用 **Plan** 规划方案，再用 **Interactive** 协作完成范围明确的更改，并在任务定义清楚时使用 **Autopilot**。常规编辑可选择更快的模型；复杂工作则可选择能力更强的模型。

上下文与基础设施同样重要。清楚说明希望构建**什么**、**为什么**以及**如何**构建，会显著影响生成结果。

## 继续探索

已完成核心工作流。还可以了解以下 CLI 功能：

- 使用 `/review` 让代码审查代理分析更改。
- 使用 `/rubber-duck` 讨论问题并获取另一种观点。
- 使用 `/fleet` 并行协调独立子任务。
- 使用 `/worktree` 隔离单独任务。
- 使用 `/delegate` 将任务发送给 GitHub Copilot 云代理。

## 后续步骤

提升工具使用能力的最佳方式是持续实践。将 Copilot 用于生产代码、兴趣项目，或一直想开发却尚未着手的小应用。与团队分享经验，也向团队成员学习。并一如既往地查阅文档。

如果想从终端扩展 Tailspin Toys，可以继续学习可选的 [Foundry Backer Concierge 系列][foundry]。若想比较其他工作环境，可探索 [VS Code 工作坊][vscode]、[GitHub Copilot app 工作坊][app]或 [Copilot 云代理工作坊][cloud]。

## 资源

- [关于 GitHub Copilot CLI][about-cli]
- [Copilot CLI 命令参考][cli-reference]
- [自定义 Copilot CLI][customize-cli]
- [使用 Copilot CLI 管理拉取请求][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
