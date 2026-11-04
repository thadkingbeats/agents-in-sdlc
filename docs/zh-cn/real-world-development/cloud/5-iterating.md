---
title: "练习 5：迭代改进 GitHub Copilot 的工作"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 上一课：管理代理][previous-lesson] |
|:--|

## 审查工作

在本实验中，你与 GitHub Copilot 合作完成了多项改善用户体验和添加功能的任务：为代码添加文档、构建供设计团队迭代的相关游戏功能，以及实现高对比度和浅色模式切换等无障碍功能。接下来检查代码更改，并在必要时向 Copilot 提供反馈，改进它的工作。

### 场景

加入生成式 AI 并不会改变软件设计和 DevOps 的基本原则。仍然需要审查生成的代码，并遵循常规 DevOps 流程。因此，在让团队其他成员参与审查前，先查看 GitHub Copilot 对文档、相关游戏功能和无障碍功能的建议。

## GitHub Copilot 云代理与安全

GitHub Copilot 云代理会在没有监督的情况下异步执行任务，因此设有安全约束：

- Copilot 只能读取存储库，并且只能写入它用于提交代码的分支。
- 云代理在 GitHub Actions 中运行，并创建独立、临时的工作环境。
- 任何 GitHub Actions 工作流都必须经过人工批准后才能运行。
- [默认情况下，外部资源访问受限](https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall)，模型上下文协议 (MCP) 服务器也包括在内。

## 审查生成的文档

先查看 GitHub Copilot 云代理创建的第一个拉取请求 (PR)，其中包含代码文档。通过 GitHub.com 上的标准 PR 界面完成审查。

> [!NOTE]
> 查看 PR 时，可能会看到 GitHub Copilot 被防火墙阻止的警告。这是**预期行为**，因为 Copilot 默认只能有限地访问外部资源，包括外部 MCP 服务器。如有需要，可以[自定义或禁用 Copilot 云代理的防火墙][agent-firewall]。

1. 在新的浏览器选项卡中打开 GitHub 上的存储库。
2. 选择 **Pull Requests**，打开 PR 列表。
3. 打开标题类似 **Add missing documentation** 的拉取请求。

> [!NOTE]
> 如果 Copilot 仍在处理任务，拉取请求中会包含 **[WIP]** 标记。请等待 Copilot 完成工作，这可能需要几分钟。

4. PR 准备就绪后，选择 **Files changed** 选项卡并审查更改。

    ![Files changed 选项卡](../../../_images/shared-pr-files-changed.png)

5. 查看新增的 TSDoc 文档注释和其他文档。具体更改可能有所不同。检查 TSDoc 文档注释、TypeScript 规范和文件注释头；这些要求来自练习 2 开始时查看的自定义指令文件。
6. 确认更新正确后，返回 **Conversation** 选项卡并向下滚动。
7. 查看是否有等待批准的工作流。
8. 如果有等待批准的工作流，选择 **Approve and run workflows**。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. 工作流会出现在 PR 的检查区域中。如果一切正常，单个 Astro 应用的项目检查将通过。此过程可能需要几分钟。

## 请求 GitHub Copilot 修改

与 Copilot 协作并非单向过程。你可以像提及团队其他成员一样，在 PR 评论或代码行内评论中提及 Copilot。Copilot 会读取评论，并启动新会话处理修改。由于结果具有非确定性，无法规定唯一的提示内容。可以要求 Copilot：

- 在每个代码文件开头添加简短说明文件用途的注释。
- 为 TypeScript 和 Astro 文件添加 TSDoc 文档注释。
- 创建 README，介绍 Astro 应用结构。

1. 添加评论，像提及其他用户一样提及 **@copilot**，并要求修改生成的文档。可以使用上面的建议，也可以提出其他文档改进要求。
2. 选择 **View Session**，观察 Copilot 如何开始新会话并执行更新。
3. 选择 **Back to pull request** 返回拉取请求。

    ![Back to pull request](../../../_images/ex7-back-to-pr.png)

4. Copilot 完成修改后，PR 中会出现新的提交。
5. 选择 **Files changed** 选项卡，审查修改。

可以继续迭代，直到满意为止。完成后，可以将 PR 从草稿状态改为准备审查，然后合并到 main 分支。

![Convert PR to ready](../../../_images/ex7-ready-for-review.png)

## 审查相关游戏功能

接下来返回 Copilot 为“在游戏详情页显示相关游戏”议题创建的 PR。

1. 在 GitHub.com 上打开存储库。
2. 选择 **Pull Requests** 选项卡。
3. 选择标题类似 **Show related games on the game details page** 的 PR。
4. 选择 **Files changed** 选项卡，审查生成的代码。
5. 确认更新正确后，返回 **Conversation** 选项卡并向下滚动。
6. 查看是否有等待批准的工作流。
7. 如果有等待批准的工作流，选择 **Approve and run workflows**。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

8. 工作流会出现在 PR 的检查区域中。如果一切正常，单个 Astro 应用的项目检查将通过。此过程可能需要几分钟。
9. **可选：** 可以在 Codespace 中切换到该分支，手动测试相关游戏功能。打开 Codespace 终端，并运行以下命令（将 `<branch-name>` 替换为 Copilot 创建的分支名，例如 **copilot/fix-8**）：

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

Copilot 已构建相关游戏功能！与之前一样，可以通过云代理迭代并请求更新。例如，可以调整显示的相关游戏数量，或要求添加文件注释头和 TSDoc 文档注释（注意：分配该任务时，你还没有更新自定义指令）。与之前一样，可以在 **Conversation** 选项卡中添加评论，Copilot 会据此启动新会话。

## 审查无障碍功能

最后，审查使用无障碍自定义代理实现的功能。此 PR 应同时包含练习 3 中要求的高对比度模式，以及练习 4 在任务控制中心追加要求的浅色模式。

1. 在 GitHub.com 上打开存储库。
2. 选择 **Pull Requests** 选项卡。
3. 选择标题类似 **Add high contrast mode to website** 的 PR。

> [!NOTE]
> 如果 Copilot 仍在处理任务，拉取请求中会包含 **[WIP]** 标记。请等待 Copilot 完成，这可能需要几分钟。

4. 选择 **Files changed** 选项卡，审查生成的代码。
5. 查看实现，重点关注：
   - 用于切换模式的用户界面 (UI) 组件。
   - 用本地存储保存用户偏好的方式。
   - 高对比度和浅色模式的 CSS 或样式更改。
   - 无障碍属性（无障碍富互联网应用 (ARIA) 标签、键盘导航等）。
   - 管理模式切换的 JavaScript/TypeScript 代码。
6. 确认更新正确后，返回 **Conversation** 选项卡并向下滚动。
7. 查看是否有等待批准的工作流。
8. 如果有等待批准的工作流，选择 **Approve and run workflows**。

   ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. 工作流会出现在 PR 的检查区域中。如果一切正常，单个 Astro 应用的项目检查将通过。此过程可能需要几分钟。
10. **可选：** 可以在 Codespace 中切换到该分支，手动测试无障碍功能。打开终端并运行以下命令（将 `<branch-name>` 替换为 Copilot 创建的分支名）：

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    随后启动应用，在浏览器中测试高对比度和浅色模式切换，确认功能正常，且页面重新加载后仍保留设置。

无障碍自定义代理帮助 Copilot 按照无障碍最佳实践实现这些功能。如果发现无障碍问题或改进点，可以像处理之前的 PR 一样，在评论中提及 **@copilot** 并要求更新。

## 可选练习 — 继续委派工作

云代理适合处理真实的待办事项，让你能将注意力转向其他工作。可以在自己的存储库中创建更多议题并分配给 Copilot，例如：

- 在游戏详情页创建支持者意向表单。
- 在游戏列表页实现分页。
- 为数据访问辅助函数添加输入验证和错误处理。

## 总结

你已完成云代理工作环境的练习。在这些课程中，你：

- **检查了存储库提供的自定义指令文件**，了解它们如何影响云代理的输出。
- **将议题分配给 GitHub Copilot 云代理**，观察它设置环境、制定计划并异步执行任务。
- **创建并使用自定义代理**处理无障碍工作，添加高对比度和浅色模式切换。
- **使用 Copilot 代理页面作为任务控制中心**，监控并引导正在进行的无障碍会话。
- **审查并迭代改进云代理的拉取请求**，提及 `@copilot` 请求修改并批准工作流。

## 回顾和后续步骤

云代理工作环境的练习已完成。其他工作环境可通过不同界面补充本次实践：

- 🖥️ **[VS Code 工作环境](../../vscode/)** — 在集成开发环境 (IDE) 中直接体验 Copilot Chat 代理模式和 MCP 集成。
- 💻 **[CLI 工作环境](../../cli/)** — 在终端中使用 Plan 和 Autopilot 模式、代理技能、自定义质量保证 (QA) 代理、Playwright MCP、Agent Merge，以及可选的 `/delegate` 云代理桥接，交付两项经过审查的更改。

还可以在自己的存储库中尝试以下后续任务：

- 将重构或测试覆盖率议题分配给云代理。
- 为其他领域创建自定义代理。
- 为不同技术栈配置 `copilot-setup-steps.yml`。

## 资源

- [GitHub Copilot][github-copilot]
- [关于 Copilot 代理][copilot-agents]
- [将 GitHub 议题分配给 Copilot][assign-issue]
- [Copilot 云代理设置工作流最佳实践][cloud-agent-best-practices]
- [配置 Copilot 云代理防火墙][agent-firewall]

---

| [← 上一课：管理代理][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
