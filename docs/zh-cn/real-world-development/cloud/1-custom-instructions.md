---
title: "练习 1 - 自定义指令（云代理）"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 上一课：先决条件][previous-lesson] · [下一课：GitHub Copilot 云代理 →][next-lesson]

生成式人工智能 (AI) 的工作效果取决于它能否获取正确上下文。如果任务有特定要求，或 Copilot 需要了解背景信息，就要确保这些上下文可用。[指令文件][instruction-files]可以提供这些指导，让 Copilot 不仅了解要做什么，也了解应如何完成。

在本练习中，你将：

- 了解存储库自定义指令和按路径指定的指令文件如何向 Copilot 提供项目上下文、编码指南和文档标准。
- 在 `.github/copilot-instructions.md` 中添加新的存储库级标准。

> [!NOTE]
> 与 VS Code 和 CLI 工作环境不同，本练习不会比较提示的前后效果。GitHub Copilot 云代理会异步处理 GitHub 议题，因此难以实时并排展示指令的影响。后续审查云代理创建的拉取请求时，可以看到指令文件如何影响结果。

## 指令文件

### 场景

Tailspin Toys 有一套开发实践指南和要求：

- 数据层必须始终包含单元测试。
- UI 应采用深色模式并具有现代感。
- 代码应使用 TSDoc 文档注释。
- 每个文件开头都应有一段注释，说明文件的用途。

接下来使用指令文件向 Copilot 提供这些要求。

### 自定义指令

自定义指令可向 Copilot 提供上下文和偏好，帮助它理解编码风格和要求。可以指定编码规范、库以及注释风格，并为整个存储库或特定文件类型创建指令。

指令文件分为两类：

- `.github/copilot-instructions.md` 是发送给 Copilot 的单个存储库级指令文件，每次请求都会使用。此文件应包含适用于大多数聊天或 CLI 请求的项目级信息，例如技术栈、项目概况、最佳实践和全局指引。
- `.github/instructions/*.instructions.md` 可针对特定任务或文件类型提供指南，例如 TypeScript、Astro、UI 组件或单元测试。

> [!NOTE]
> 在 IDE 中，指令文件仅用于 Copilot Chat 代码生成，不用于代码补全或下一步编辑建议。
>
> Copilot Chat、Copilot CLI 和 Copilot 云代理在生成代码时都会使用存储库级指令，以及包含 `applyTo` frontmatter 的 `*.instructions.md` 文件。
>
> Copilot 还支持 AGENTS.md 和 CLAUDE.md 等其他标准格式的指令文件。

[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses

### 管理指令文件的最佳实践

项目示例体现了以下做法：

- 让 `copilot-instructions.md` 聚焦于项目级指引，例如项目用途、结构和全局编码规范。
- 使用 `*.instructions.md` 文件描述特定文件类型（单元测试、Astro 组件、数据层）或任务。
- 使用自然语言，保持指引清晰，并提供代码示例。

指令文件没有唯一的正确写法。通过实践找到适合项目的方式。

> [!TIP]
> 使用 GitHub Copilot 的项目应包含完善的指令文件。项目中有用于 [UI 更新][ui-instructions]和 [Astro][astro-instructions] 等任务的指令。
>
> Copilot 也可以帮助生成指令文件。不同产品界面的操作方式有所不同，例如 VS Code 中的 **Configure Chat → Generate Agent Instructions**，或 Copilot CLI 中的 `/init`。相应工作环境的课程会在相关处说明。
>
> 需要模板或起点？可以浏览 [awesome-copilot][awesome-copilot]，其中包含指令文件、自定义代理和其他资源。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 查看项目中的自定义指令文件

花些时间查看存储库提供的核心 `copilot-instructions.md` 和各类 `*.instructions.md` 文件。可以在编辑器或 GitHub 网页界面中打开它们。

1. 打开 `.github/copilot-instructions.md`。
2. 查看项目简介，以及 **Agent notes**、**Code standards**、**Scripts** 和 **Repository Structure** 等部分。注意 **Code standards** 下的 **GitHub Actions Workflows** 指引；这些内容适用于与 Copilot 的所有交互。
3. 打开 `.github/instructions` 文件夹，查看其中关于 Astro、Drizzle 数据层、测试等方面的指令。
4. 打开 `.github/instructions/unit-tests.instructions.md`。查看顶部的 `applyTo` 字段；它设置相对于存储库根目录的 glob。任何匹配 `**/*.test.ts` 的 TypeScript 测试文件都适用这些指令。
5. 查看此文件中关于为项目创建单元测试的说明。
6. 打开 `.github/instructions/drizzle.instructions.md` 并滚动到底部，查看指向其他指令文件（例如 `unit-tests.instructions.md`）和项目现有文件的链接。路径相对于指令文件所在位置，而不是存储库根目录。

> [!NOTE]
> `copilot-instructions.md` 中的 **Code formatting requirements** 部分介绍了项目编码标准，但尚未要求添加代码文档。接下来会加入 TSDoc 文档注释和文件注释头规范。

## 添加存储库级标准

接下来需要编辑一次项目文件：添加全局规则，要求代码使用 TSDoc 文档注释和文件级注释头。云代理会在本工作环境后续练习中处理你分配的议题时使用此规则。

先创建分支。云代理会从议题目标分支读取指令，但仍应妥善提交自己的更改。

1. 在 codespace 终端中创建并切换到新分支：

   ```bash
   git checkout -b custom-instructions-cloud
   ```

`.github/copilot-instructions.md` 用于向 Copilot 提供项目级信息。现在添加编码标准，改进代码建议。

1. 重新打开 `.github/copilot-instructions.md`。
2. 找到 **Code formatting requirements** 部分（应接近第 27 行）。此处说明了编码规范，但尚未要求添加代码文档，因此生成的辅助函数没有文档注释。
3. 在现有规范下方添加以下 Markdown 内容，要求 Copilot 添加文件注释头和 TSDoc 文档注释：

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. 保存 `copilot-instructions.md`。

> [!TIP]
> 指令文件既可以放在存储库级别（`.github/copilot-instructions.md`），为整个项目提供指引，也可以使用 `*.instructions.md` 文件针对特定语言、文件类型或任务提供指引。刚添加的文档注释规范适用于整个项目，因此存储库级文件是合适的位置。

## 提交、推送并合并指令更新

云代理会读取议题目标分支中的指令。在下一练习中将议题分配给 Copilot 时，它会从 `main` 分支创建新分支。因此，必须先将指令更新合并到 `main`，云代理才能使用这些指令。

1. 暂存并提交更改：

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. 推送分支：

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. 在 github.com 上创建从 `custom-instructions-cloud` 合并到 `main` 的拉取请求并完成合并。这样，云代理在下一练习中处理所分配的议题时就能读取这些指令。

> [!TIP]
> 如果希望在本练习中直接使用 `main`，可以跳过分支操作，直接提交到 `main`。此处采用分支，是为了模拟真实项目中的工作方式。

## 总结和后续步骤

你了解了 Copilot 如何从项目指令文件获取上下文，并在 `.github/copilot-instructions.md` 中添加了一项新的存储库级标准。在本工作环境后续练习中，可以查看云代理创建的拉取请求如何遵循该标准。

接下来[将第一个议题分配给 GitHub Copilot 云代理][next-lesson]。

## 资源

- [用于自定义 GitHub Copilot 的指令文件][instruction-files]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [编写更好的 Copilot 自定义指令的 5 个技巧][copilot-instructions-five-tips]
- [Awesome Copilot — 指令文件和其他资源集合][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
