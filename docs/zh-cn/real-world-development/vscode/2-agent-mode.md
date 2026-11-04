---
title: "练习 2 - 使用 Copilot 代理模式添加功能"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

即使是简单的应用更新，通常也需要修改多个文件并执行测试。开发者需要找到相关文件、进行修改、运行测试、调试、发现遗漏的文件并继续修改，工作环节往往很多。

Copilot 代理模式可以帮助处理这类工作。

代理模式能在 IDE 中更自主地工作。它会先探索项目结构，进行必要修改，运行测试等任务，并自动修复发现的问题。接下来使用代理模式为网站添加功能。

> [!NOTE]
> 代理模式和云代理名称相似，但适用于不同场景。代理模式在 IDE 中执行任务，便于快速反馈和交互。云代理则像团队成员一样异步工作，通过议题和拉取请求与你协作。

在本练习中，你将了解如何：

- 让 Copilot 代理模式探索项目、定位相关文件并协调多处更改。
- 使用代理模式跨 UI 和数据层实现新功能。
- 在合并到代码库之前审查 Copilot 生成的更改和测试。

## 场景

随着游戏列表增加，你希望用户能够按类别和 publisher 筛选。上一练习已添加 publisher 辅助函数，现在将使用 Copilot 代理模式完成剩余的数据层、UI 和测试工作。

## 运行 Tailspin Toys 网站

修改代码前，先查看网站当前功能。

该网站是一个开发者主题棋盘游戏众筹平台，可列出游戏并显示游戏详情。它是一个 Astro 应用，在构建时将页面渲染为静态 HTML。页面通过 frontmatter 使用 Drizzle ORM 直接查询本地 SQLite 数据库，不存在单独的后端 API 或客户端 UI 框架。可复用的数据访问辅助函数位于 `src/lib/`，交互功能使用少量范围明确的 Astro `<script>` 和标准 DOM API 实现。

### 启动网站

项目提供了 `npm run dev` 任务，用于启动单个 Astro 开发服务器。请在 GitHub Codespace 中按以下步骤运行：

1. 返回上一练习中使用的 codespace。当前分支应为 `main`。
2. 在 Codespace 中按 <kbd>Control</kbd>+<kbd>`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>`</kbd>（Windows/Linux）打开终端。
3. 为筛选工作创建并切换到新分支：

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 运行以下命令启动网站：

   ```bash
   npm run dev
   ```

   Astro 开发服务器就绪后，会显示包含 URL 的提示，类似于：

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> 如果弹出提示，询问是否要在浏览器窗口中打开 `http://localhost:4321`，选择 **x** 关闭。

5. 在终端中按住 <kbd>Command</kbd>（Mac）或 <kbd>Ctrl</kbd>（Windows/Linux），并选择 Astro 服务器地址 `http://localhost:4321`，打开网站。

> [!NOTE]
> 在 codespace 中选择终端里的 localhost 链接时，会自动重定向到 `https://<your-codespace-name>-4321.app.github.dev/`。这是连接到 codespace（当前正运行网站服务器）的私有隧道。

### 浏览网站

网站启动后，可以浏览它的主要功能：

- **主页**：显示棋盘游戏的列表，包括标题、图像和说明。
- **游戏详情页**：选择游戏后会打开详情页，其中包含标题、说明、publisher 和类别等信息。

## 使用 Copilot 探索待办事项

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 codespace，打开 Copilot Chat 面板并选择 **New Chat**，开始干净的对话。不同练习所用的模式和模型可能不同；相关步骤会在需要时说明。

网站当前版本可以运行，但还需要增加功能。项目模板已自动创建议题待办事项。先让 GitHub Copilot 列出这些事项。

1. 在 Chat 视图的代理下拉列表中选择 **Agent**。代理模式可以自主规划并跨文件实现更改、运行终端命令和调用工具。

   ![显示 Chat 视图中代理选择器的截图。](../../../_images/shared-chat-mode-selector.png)

2. 从可用模型列表中选择 **Claude Sonnet 4.5**。

> [!CAUTION]
> 本研讨会作者并未偏好某个模型。编写本研讨会时使用了 Claude Sonnet 4.5，因此示例采用该模型，希望由此获得相对一致的体验。但由于大型语言模型 (LLM) 具有概率性，收到的建议可能与示例不同，这是正常且预期的情况。

> [!NOTE]
> 由于 LLM 具有概率性，Copilot 可能会使用不同的 MCP 命令，但仍应能完成任务。

3. 向 Copilot 发送以下提示，询问存储库中的待办事项：

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. 选择 **Continue**，运行列出所有议题的命令。
5. 查看生成的议题列表。

Copilot 还会根据对用户的帮助程度为事项排序。

## 查看指令文件

让代理生成代码前，先查看用于提供工作上下文的指令文件。本练习将使用 [user interface (UI)](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md) 文件，其中包含为网站添加功能时应遵循的指南。

1. 在 codespace 中打开 `.github/instructions/ui.instructions.md`。
2. 查看其中关于添加功能的整体指引，包括：
   - 架构概览。
   - 组件设计、可测试性和无障碍原则。
   - 指向各类文件专用指令的链接，包括 Astro、Tailwind CSS 和 Drizzle。

> [!TIP]
> 指令文件可以引用其他指令文件和项目文件。路径相对于指令文件所在位置，因此可以复用指引、拆分复杂指令，并在生成代码时引用示例和模板。

## 实现筛选功能

完成筛选至少需要对应用进行三项更改：

- 在数据层 (`src/lib/`) 添加或完善筛选逻辑。
- 添加或更新筛选行为测试。
- 更新游戏列表页，添加筛选 UI。

此外，合并前需要运行并通过测试。Copilot 代理模式可以协助完成这些工作。

1. 可以继续当前 Copilot 对话，也可以选择 **New Chat** 开始新对话。
2. 选择 **Add Context**、**Instructions**，然后选择 **ui** 指令文件。

   ![选择 UI 指令文件的示例截图](../../../_images/ex3-select-instructions-file.png)

3. 确认 Chat 视图的代理下拉列表中仍选择 **Agent**。

   ![显示 Chat 视图中代理选择器的截图。](../../../_images/shared-chat-mode-selector.png)

4. 确认仍选择 **Claude Sonnet 4.5** 模型。
5. 根据待办事项中的相关议题，使用以下提示要求 Copilot 实现功能：

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. 观察 Copilot 探索项目并定位相关文件。它应会查找数据层辅助函数、UI 和测试，然后修改文件并运行测试。

   ![Copilot 正在探索项目文件的截图](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot 会探索项目、修改文件并运行测试。根据任务和代码库的复杂度，这可能需要几分钟。过程中编辑器可能会出现 **Keep** 和 **Undo** 按钮。工作尚未完成时无需选择；完成后，每项更改都会显示相应的 **Keep** 或 **Undo** 选项。

7. 按 Copilot 的提示选择 **Continue**，运行测试。

   ![Copilot Chat 面板中要求确认运行测试的对话框截图](../../../_images/ex3-agent-mode-run-tests.png)

8. 工作过程中可能会暂停，或暂时出现测试失败，这属于正常情况。Copilot 会在生成代码和运行测试之间反复迭代，直到任务完成且未发现错误。

   ![Copilot 代理模式完整聊天会话的截图](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 检查生成的代码，留意可能存在的问题。

> [!CAUTION]
> 务必审查 Copilot 或其他 AI 工具生成的代码。

10. 返回正在运行网站的浏览器，探索新功能。
11. 确认功能正常并审查代码后，在 Copilot Chat 窗口中选择 **Keep**。

## 总结和后续步骤

本练习介绍了如何使用 GitHub Copilot 代理模式为 Tailspin Toys 网站添加功能：

- 使用代理模式跨 UI 和数据层实现新功能。
- 让 Copilot 代理模式探索项目、定位相关文件并协调多处更改。
- 在合并到代码库之前审查 Copilot 生成的更改和测试。

接下来[使用 Playwright MCP 服务器测试功能][next-lesson]，然后为其创建拉取请求。

### 拓展练习 — 实现分页

随着游戏列表增加，需要支持分页。使用本练习中学到的技能，提示 Copilot 为网站添加分页。考虑以下事项：

- 遵循现有最佳实践，包括使用已有指令文件。
- 确定分页方式，例如是否允许用户选择每页大小，或采用固定值。
- 编写提示时提供所需信息，以便 Copilot 按预期实现。
- 可能需要通过补充上下文和要求更改来迭代 Copilot；这正是与 Copilot 协作的常见方式。

## 资源

- [Copilot 的 ask、edit 和 agent 模式：功能及适用场景][choose-mode]
- [VS Code 中的代理模式][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
