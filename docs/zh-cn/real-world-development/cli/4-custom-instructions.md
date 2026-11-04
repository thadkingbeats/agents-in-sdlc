---
title: "第 4 课 - 使用自定义指令引导 Copilot"
description: "查看存储库指令，添加文档标准，并将其应用于筛选代码。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

生成式人工智能 (AI) 的工作效果取决于它能否获取正确上下文。如果任务有特定要求，就要确保 Copilot 可以获取相关指引。[指令文件][instruction-files]不仅说明希望生成什么代码，也说明代码应如何组织。现在筛选功能已经完成，可以查看 Copilot 使用的指令、添加文档标准，并将其应用于代码。

在本课中，你将：

- 了解存储库指令和按路径指定的指令文件如何传递给代理。
- 更新指令文件，确保遵循编码标准。
- 观察指令文件对代码的影响。

## 场景

Tailspin Toys 有一套开发实践指南和要求：

- 注释应解释意图和不明显的决策，而不是复述代码。
- `db/` 和 `src/lib/` 中导出的函数应使用 TSDoc/JSDoc 记录用途、参数和返回值；如果有可注入的 `db` 参数，也要记录。
- 可复用的 Astro 组件应说明其 `Props` 接口，并在相关代码更改时同步更新注释。
- 应保留现有格式和 lint 指引。

接下来使用指令文件向 Copilot 提供这些要求。

## 指令文件

自定义指令可向 Copilot 提供上下文和偏好，帮助它理解编码风格和要求。可以指定编码规范、库以及注释风格，并为整个存储库或特定文件类型创建指令。

指令文件分为两类：

- `.github/copilot-instructions.md` 是发送给 Copilot 的单个存储库级指令文件，每次请求都会使用。此文件应包含适用于大多数请求的项目级信息。
- `.github/instructions/*.instructions.md` 文件可为特定语言、文件类型或任务提供指引。

> [!NOTE]
> 不同工作环境对其他指令格式的支持情况可能不同。依赖特定格式前，请查看[自定义指令支持参考][custom-instructions-support]。

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## 查看项目中的自定义指令文件

项目模板已包含一组指令文件。先查看已有内容，再进行更改，观察其影响。

1. 返回 Codespace。
2. 在 Codespaces 编辑器（不是终端）中打开 `.github/copilot-instructions.md`。
3. 查看项目简介和编码指引。该文件适用于此存储库中与 Copilot 的所有交互。
4. 打开 `.github/instructions` 文件夹，查看其中的文件。这里包含 Astro、Drizzle 数据层、测试等方面的指令。
5. 打开 `.github/instructions/unit-tests.instructions.md`，查看顶部的 `applyTo` 字段；它设置了指令适用文件的 glob。
6. 打开 `.github/instructions/drizzle.instructions.md`，查看其中指向其他指令文件和项目现有文件的链接。这样可以将较大的指令集拆分成可复用文件，并为 Copilot 提供可遵循的示例。

## 更新指令文件以符合团队指南

现有文件已打下良好基础，但仍有缺漏。接下来修改核心 `copilot-instructions.md`，要求新生成的 TypeScript 代码包含 TSDoc 注释。

1. 在 `.github/copilot-instructions.md` 中找到 **Code formatting guidance** 部分（应位于第 35 行附近）。
2. 在该部分的最后一项后添加以下内容：

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

文件会自动保存。

## 使用更新后的指引

Copilot CLI 会在会话启动时加载存储库指令。保存指令更新后，退出并恢复筛选会话，使 Copilot 在保留功能上下文的同时加载新指引。

1. 如果筛选会话仍处于打开状态，输入 `/exit` 关闭。Copilot CLI 会自动保存会话。
2. 在 `game-filters-cli` 分支的存储库根目录中，恢复已保存的会话：

   ```bash
   copilot --resume
   ```

   如果出现提示，请选择筛选会话，并确认已检出 `game-filters-cli` 分支。
3. 要求 Copilot 应用更新后的指引：

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. 输入 `/diff`，查看更改的 TypeScript 文件。注意新增的 TSDoc 注释，并确认其准确说明了代码。

## 总结和后续步骤

你了解了 Copilot CLI 如何从指令文件获取上下文，并将新标准应用于功能代码。具体来说，你：

- 了解了存储库指令和按路径指定的指令文件如何传递给代理。
- 更新了指令文件，确保遵循编码标准。
- 观察了指令文件对代码的影响。

接下来[自定义并运行可复用的 quality-checks 技能][next-lesson]，确保一致地运行 lint 和测试。

## 资源

- [为 Copilot CLI 添加自定义指令][instruction-files]
- [自定义指令支持][custom-instructions-support]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [Awesome Copilot — 指令文件集合][awesome-copilot]

[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
