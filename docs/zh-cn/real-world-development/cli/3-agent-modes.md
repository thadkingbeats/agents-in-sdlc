---
title: "第 3 课 - 代理模式：Plan 和 Autopilot"
description: "使用 Plan 确定实施方案，使用 Autopilot 根据议题构建筛选功能，再通过 Interactive 模式审查结果。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

我们先为项目添加了一项小功能。更大的更改需要更完善的流程。GitHub Copilot CLI 可以融入组织现有的开发流程，帮助团队以正确方式构建正确功能。本课将开始一系列代理驱动开发练习：从议题着手实现功能、验证代码和行为，最后成功合并。

> [!NOTE]
> 后续功能工作将沿用同一对话和分支。实际项目中通常会为不同文件类型使用多个分支或 PR；本研讨会为了聚焦核心概念而简化了流程。

在本课中，你将：

- 根据 GitHub 议题开始新的 Copilot 对话。
- 在 Plan 模式中确定需求。
- 使用 Autopilot 模式实现新功能。
- 审查代码。
- 在转发的浏览器中手动验证功能。

继续实现此功能时，还将更新存储库指令、自定义现有 `quality-checks` 技能、添加 MCP 验证、创建 QA 代理并创建功能 PR。

## 场景

Tailspin Toys 的游戏目录不断增长，访问者需要按类别和 publisher 筛选游戏。待办事项中的议题描述了该功能，但组合类别等细节需要在编写代码前确定。你将使用 Plan 模式确认这些决定，然后授权 Autopilot 按范围实现功能。

## 背景

在开发流程中引入人工智能 (AI) 编码代理并不会改变基本原则。大多数开发者的流程包括：

1. 从说明需求的已创建议题开始。
2. 制定实现计划。
3. 编写并审查代码。
4. 运行测试验证代码。
5. 手动验证新功能。
6. 创建拉取请求 (PR)。
7. 代码经过审查且持续集成流程成功后，合并代码。

> [!NOTE]
> 具体流程会因团队和组织而异，但大多数流程都与上述方式类似。

坚持标准流程，可以确保 AI 生成的代码满足需求，并经过与手动编写代码相同的审查。

## 对话模式

**对话模式**控制代理的自主程度。按 <kbd>Shift</kbd>+<kbd>Tab</kbd> 可在模式之间切换：

- **Interactive**：你与代理协作。代理提出更改建议，并等待你的输入后再继续。
- **Plan**：代理先制定计划，但不能编辑项目文件。
- **Autopilot**：代理自主编写代码、运行测试并不断迭代，直至任务完成。

先使用 Plan 模式并审查计划，再使用 Autopilot 实现。

## 从议题开始

开始筛选工作前，先返回 Codespace，确认存储库和终端已准备就绪。

1. 返回 Codespace。如果已停止，请重新启动。
2. 确认星级评分 PR 已合并。
3. 如果终端尚未打开，按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）。
4. 更新 `main`，并为筛选工作创建分支：

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. 启动 Copilot CLI：

   ```bash
   copilot --yolo
   ```

6. 按两次 <kbd>Tab</kbd> 打开 **Issues** 选项卡。
7. 按 <kbd>A</kbd> 显示所有议题。
8. 使用箭头键突出显示标题为 **Allow users to filter games by category and publisher** 的议题。
9. 按 <kbd>C</kbd> 将议题加入提示，并返回 **Session** 选项卡。

现在提示中会出现 `#7` 或类似编号。使用 `#` 可将 GitHub 议题或拉取请求 (PR) 添加到上下文中。

## 规划筛选功能

规划可以在交给 Copilot 实施前确定功能或任务的处理方式。对于复杂任务，建议花时间制定计划。现在切换到计划模式，让 Copilot 创建计划。

1. 按 <kbd>Shift</kbd>+<kbd>Tab</kbd> 切换到 Plan 模式，并确认提示下方显示 **Plan**。
2. 在上一步添加的议题引用后输入以下提示：

   ```plaintext
   Create a plan for implementing this feature.
   ```

Copilot 会先探索项目，再确定合适的实现方式。

3. Copilot 可能会询问筛选行为的细节。根据偏好回答；不存在唯一正确答案。
4. 计划完成后，按 <kbd>Control</kbd>+<kbd>E</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>E</kbd>（Windows/Linux）展开计划。
5. 滚动查看计划。
6. 如果计划与已决定的要求不符，请让 Copilot 修改。

## 批准 Autopilot

计划完成并审查后，就可以开始实现。使用 Autopilot 让 Copilot 处理工作，并不断迭代，直到认为任务完成。

1. 选择 **Accept plan and build on autopilot (recommended)**，或当前版本中含义相同的选项。
2. 确认提示下方显示 **Autopilot** 模式。
3. 观察 Copilot 如何根据计划编写代码并运行测试。

> [!NOTE]
> 批准后可能会立即开始实现，因此请先审查计划。如果 Copilot 报告缺少依赖项或端口冲突，请先解决环境问题，再判断检查是否完成。

## 审查并验证实现

代码生成后，与其他代码一样，合并前需要审查。现在检查代码并运行网站。

1. 按 <kbd>Shift</kbd>+<kbd>Tab</kbd> 进入 Interactive 模式，确认提示下方不再显示 **Plan** 或 **Autopilot**。
2. 输入 `/diff`，检查筛选实现和测试。
3. 将结果与议题和计划阶段确定的决策进行比较。
4. 审查代码后，按 <kbd>Esc</kbd> 退出差异视图。
5. 查看项目检查结果；如有失败，请让 Copilot 修复。

## 探索新功能

代码看起来不错，但还需要确认能否运行。像之前一样启动应用，通过 Codespaces 转发端口打开网站。

1. 让 Copilot 启动应用：

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. Codespaces 报告端口 `4321` 可用时，选择 **Open in Browser**。
3. 尝试按类别筛选、按 publisher 筛选，以及计划中确定的组合筛选。
4. 确认重置和无结果状态符合议题和你的决策。
5. 返回 Codespace，要求 Copilot 停止它启动的开发服务器。

## 总结和后续步骤

本课使用不同的对话模式构建并审查功能。你：

- 根据 GitHub 议题开始新的 Copilot 对话。
- 在 Plan 模式中确定需求。
- 使用 Autopilot 模式实现新功能。
- 审查了代码。
- 在转发的浏览器中手动验证了功能。

接下来[使用自定义指令][next-lesson]，深入了解如何让生成的代码遵循书面规范。

## 资源

- [GitHub Copilot CLI 中的 Autopilot][autopilot]
- [Copilot CLI 命令参考][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
