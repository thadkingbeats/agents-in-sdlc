---
title: "练习 3 - 使用 Playwright MCP 服务器测试功能"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：代理模式][previous-lesson] · [下一课：自定义代理 →][next-lesson]

你刚刚使用代理模式构建了筛选功能。创建拉取请求之前，应确认它在浏览器中确实有效。本练习将连接 **Playwright 模型上下文协议 (MCP) 服务器**，让 Copilot 操作真实浏览器测试功能，而不是由你手动逐项操作；随后发布分支并创建拉取请求 (PR)。

在本练习中，你将：

- 了解模型上下文协议 (MCP) 以及 MCP 服务器如何使用新工具扩展 Copilot。
- 在工作区中添加 Playwright MCP 服务器。
- 让 Copilot 使用 Playwright MCP 服务器在浏览器中手动测试筛选功能。
- 发布分支，并为筛选工作创建拉取请求。

## 什么是模型上下文协议 (MCP)？

当代理模式可以访问编辑器以外的工具时，功能会更强大。Copilot 使用模型上下文协议 (MCP) 与这些工具通信；MCP 是代理与外部工具和服务通信的标准方式。

![代理模式的内部工作原理示意图，展示其与上下文、大型语言模型 (LLM) 和工具（包括 MCP 服务器及 VS Code 扩展提供的工具）的交互](../../../_images/ex1-mcp-diagram.png)

[模型上下文协议 (MCP)](https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/) 为人工智能 (AI) 代理提供了与外部工具和服务通信的方式。通过 MCP，AI 代理可以实时访问外部工具和服务，从而使用资源获取最新信息，并使用工具代表你执行操作。

代理通过 MCP 服务器访问工具和资源。MCP 服务器充当 AI 代理与外部工具和服务之间的桥梁，负责管理代理与外部工具（例如现有应用程序编程接口 (API) 或 npm 包等本地工具）之间的通信。每个 MCP 服务器都提供一组可供 AI 代理访问的工具和资源。

以下是一些常见的 MCP 服务器：

- **[GitHub MCP Server](https://github.com/github/github-mcp-server)**：提供一组用于管理 GitHub 存储库的 API，让 AI 代理可以创建存储库、更新现有存储库，以及管理议题和拉取请求。
- **[Playwright MCP Server](https://github.com/microsoft/playwright-mcp)**：使用 Playwright 提供浏览器自动化能力，让 AI 代理可以浏览网页、填写表单和选择按钮。

还有许多其他 MCP 服务器可连接不同的工具和资源。GitHub 提供 [MCP 注册表](https://github.com/mcp)，帮助发现并为生态系统做出贡献。

> [!CAUTION]
> 对待 MCP 服务器应与对待项目的其他依赖项一样谨慎。使用前请仔细审查源代码、验证发布者并评估安全影响。只使用信任的 MCP 服务器，并谨慎授予敏感资源或操作的访问权限。

## 查看 MCP 配置

`.vscode/mcp.json` 文件用于配置 VS Code 工作区可用的 MCP 服务器。

1. 在 codespace 中打开 `.vscode/mcp.json`。
2. 查看已经配置好的 `github` 服务器：

    ```json
    {
      "servers": {
        "github": {
          "type": "http",
          "url": "https://api.githubcopilot.com/mcp/"
        }
      }
    }
    ```

项目模板已配置 `github` 条目，因此上一练习中 Copilot 能够读取议题待办事项。此配置使用[远程 GitHub MCP 服务器][remote-github-mcp-server]，无需在本地安装任何内容。VS Code 通过 HTTP 连接该服务器，并在 Copilot 首次使用其工具时要求你通过 GitHub 身份验证。

## 添加 Playwright MCP 服务器

接下来添加第二个服务器。[Playwright MCP 服务器][playwright-mcp-server]为 Copilot 提供可控的浏览器，可用于测试刚实现的功能。

1. 在 `.vscode/mcp.json` 中，在 `github` 旁边添加 `playwright` 条目，使文件如下所示：

    ```json
    {
      "servers": {
        "github": {
          "type": "http",
          "url": "https://api.githubcopilot.com/mcp/"
        },
        "playwright": {
          "command": "npx",
          "args": ["@playwright/mcp@latest", "--headless"]
        }
      }
    }
    ```

2. 保存文件。

与远程 `github` 服务器不同，`playwright` 是**本地**服务器：VS Code 会在你的计算机上运行 `npx @playwright/mcp@latest` 来启动它。`--headless` 标记让 Playwright 在不显示窗口的情况下运行浏览器；codespace 没有可显示窗口的桌面环境，因此需要此选项。

> [!NOTE]
> Tailspin Toys 项目已在端到端测试中使用 Playwright，因此通常已经安装了 Playwright 所需的浏览器。如果 Copilot 随后报告缺少浏览器，请让它运行 `npx playwright install chromium`，然后重试。

## 启动并信任服务器

VS Code 会**按需**启动 MCP 服务器：Copilot 首次需要服务器工具时，VS Code 会启动服务器，并询问你是否信任该服务器。

1. 在 `.vscode/mcp.json` 中，`playwright` 条目上方会显示 **Start** 操作。选择它以立即启动服务器，并确认配置正确。
2. 如果 VS Code 询问是否信任该服务器，请先审查配置，再选择信任以启动服务器。

手动启动是可选的。如果跳过，VS Code 会在下一步中 Copilot 首次需要服务器工具时启动它，并提示你信任该服务器。

## 测试筛选功能

[Playwright MCP 服务器][playwright-mcp-server]为 Copilot 提供可以操作的真实浏览器。代理可以打开页面、进行导航、应用筛选条件并读取结果，然后向你总结观察到的内容，无需离开当前对话，也无需手动操作应用。

Playwright MCP 服务器通过页面的[无障碍树][playwright-mcp-server]而不是截图进行操作。这意味着代理可以读取带标签的结构化元素（按钮、链接和列表项），与辅助技术采用的方式类似，因此简单的功能检查也可以顺便验证基本无障碍情况。

连接服务器并启动应用后，使用以下提示让 Copilot 测试筛选功能：

```text
Using the Playwright MCP server, open a browser to the running app at http://localhost:4321 and verify the new game filtering feature:

1. Go to the games page and note how many games are listed.
2. Apply a category filter and confirm the list updates to only show games in that category.
3. Clear it, then apply a publisher filter and confirm the list updates to that publisher.
4. Combine a category and a publisher filter and confirm the results respect both.

Report what you observe at each step, and call out anything that does not behave as expected.
```

Copilot 会通过 Playwright MCP 服务器启动浏览器并执行每个步骤，然后报告结果。请根据议题中的验收标准审查其报告；如果发现异常，可以继续提问，或让它在创建拉取请求前修复代码。

> [!NOTE]
> 测试时应用必须在 `http://localhost:4321` 运行。如果已停止开发服务器，请在发送提示前重新启动。Copilot 首次使用 Playwright MCP 服务器时，可能需要下载浏览器；如果报告缺少浏览器，请让它运行 `npx playwright install chromium`，然后重试。

[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp

## 发布分支并创建拉取请求

确认功能正常后，就可以创建拉取请求 (PR)，供团队审查。首先发布 `filtering-vscode` 分支。

1. 在 codespace 中打开 **Source Control** 面板，审查 Copilot 所做的更改。
2. 选择 **+** 图标暂存更改。
3. 选择 **Sparkle** 按钮生成提交消息。

   ![显示更改内容的 Source Control 面板截图](../../../_images/ex3-source-control-changes.png)

4. 选择 **Publish**，将分支推送到存储库。

## 创建拉取请求

可以通过 github.com 或 GitHub 命令行界面 (CLI) 创建拉取请求。也可以让 Copilot 使用 GitHub 工具查找相关议题并创建关联的 PR。

1. 打开 Copilot Chat 面板并选择 **New Chat**，开始新会话。
2. 在代理下拉列表中选择 **Agent**，确保 Copilot 可以使用 GitHub 工具。
3. 使用以下提示要求 Copilot 创建 PR：

   ```plaintext
   Find the issue in the repo related to filtering by category and publisher. Create a new pull request for the current branch, and associate it with the correct issue.
   ```

4. 根据需要选择 **Continue**，允许 Copilot 执行获取信息和操作所需的任务。首次使用 GitHub 工具时，可能会提示你登录 GitHub；按提示完成身份验证。
5. 留意 Copilot 如何搜索议题、找到相关议题并创建 PR。
6. 选择 Copilot 返回的链接，审查拉取请求，但**暂时不要合并**。

## 总结和后续步骤

本练习中，你：

- 了解了模型上下文协议 (MCP) 以及 MCP 服务器如何使用新工具扩展 Copilot。
- 在工作区中添加了 Playwright MCP 服务器。
- 使用该服务器在浏览器中手动测试筛选功能。
- 发布了分支，并为筛选工作创建了拉取请求。

你使用 MCP 服务器测试了功能，但 MCP 只是扩展 Copilot 的一种方式。接下来[创建自定义代理][next-lesson]，简化无障碍审查等专项任务。

## 资源

- [MCP 是什么，为什么大家都在讨论它？][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [GitHub MCP Server][github-mcp-server]
- [GitHub MCP 注册表][mcp-registry]
- [VS Code 中的 MCP 服务器][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
