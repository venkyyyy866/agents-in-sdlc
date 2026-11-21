---
title: "课程 4 - 使用自定义指令引导 Copilot"
description: "浏览存储库指令、添加文档规范，并将其应用于筛选功能代码。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

使用生成式 AI 时，上下文至关重要。如果任务必须以特定方式完成，就要让 Copilot 能够获取相应指导。[指令文件][instruction-files]不仅说明你想要什么代码，也说明代码应该如何组织。现在你已实现筛选功能，接下来将了解 Copilot 使用的指令、添加文档规范，并将其应用于代码。

在本课程中，你将：

- 了解存储库指令和按路径限定的指令文件如何传达给智能体；
- 更新指令文件，确保遵循编码规范；
- 查看指令文件对代码的影响。

## 场景

Tailspin Toys 有一套开发实践指南和要求，包括：

- 注释应说明意图和不明显的设计决定，而不是重复代码内容。
- `db/` 和 `src/lib/` 中导出的函数应使用 TSDoc/JSDoc 说明用途、参数和返回值（如果存在可注入的 `db` 参数，也要说明）。
- 可重复使用的 Astro 组件应说明其 `Props` 接口契约；相关代码更改时，注释也应保持更新。
- 应保留现有格式和 lint 指南。

通过使用指令文件，你可以确保 Copilot 了解这些实践要求，并据此完成任务。

## 指令文件

自定义指令可以向 Copilot 提供上下文和偏好，帮助它理解你的编码风格和要求。你可以指定偏好的编码约定、库，甚至喜欢的注释形式，从而引导 Copilot 提供更相关的建议和代码片段。你可以为整个存储库创建指令，也可以为特定文件类型或任务提供上下文。

指令文件有两种：

- `.github/copilot-instructions.md` 是一个指令文件，会随该存储库的**每个**请求一起发送给 Copilot。此文件应包含适用于大多数请求的项目级信息。
- `.github/instructions/*.instructions.md` 文件可为特定语言、文件类型或任务提供指导。

> [!NOTE]
> 不同环境支持的其他指令格式可能有所不同。依赖特定格式前，请先查阅[自定义指令支持参考][custom-instructions-support]。

## 浏览本项目中的自定义指令文件

为帮助你开始使用，入门项目已包含一组指令文件。在修改之前，先浏览现有文件，之后再观察更改的效果。

1. 返回 Codespace。
2. 在 Codespaces 编辑器（不是终端）中打开 `.github/copilot-instructions.md`。
3. 浏览文件，留意项目简介和编码指导。此存储库中与 Copilot 的所有交互都会使用这些指令。
4. 打开 `.github/instructions` 文件夹并浏览其中的文件。你会看到适用于 Astro 文件、Drizzle 数据层、测试等内容的指令。
5. 打开 `.github/instructions/unit-tests.instructions.md`。留意顶部的 `applyTo` 字段；它设置一个 glob，用于确定指令适用的文件。
6. 打开 `.github/instructions/drizzle.instructions.md`，留意其中指向其他指令文件和项目现有文件的链接。这样可以将较大的指令集拆分成更小、可重复使用的文件，并为 Copilot 提供生成代码时可参考的示例。

## 更新指令文件以符合团队指南

现有文件是不错的起点，但仍有不足。我们来修改核心 `copilot-instructions.md` 文件，确保新生成的 TypeScript 代码包含 TSDoc 注释。

1. 在 `.github/copilot-instructions.md` 中找到 **Code formatting guidance** 部分，通常在第 35 行附近。
2. 在该部分末尾添加以下项目：

   ```markdown
   - 所有新建的 TypeScript 代码都应包含用于说明代码的 TSDoc 注释。
   ```

文件会自动保存！

## 使用更新后的指导

Copilot CLI 会在会话启动时加载存储库指令。保存更新后的指令后，退出并恢复筛选会话，让 Copilot 在保留功能上下文的同时加载新指导。

1. 如果筛选会话仍处于打开状态，输入 `/exit` 关闭它。Copilot CLI 会自动保存会话。
2. 在 `game-filters-cli` 分支的存储库根目录中，恢复已保存的会话：

   ```bash
   copilot --resume
   ```

   如果出现提示，请选择筛选会话，并确认当前检出的是 `game-filters-cli` 分支。
3. 请 Copilot 根据更新后的指导修改代码：

   ```plaintext
   我们刚刚更新了指令和代码指导。请根据这些指导更新你生成的代码。
   ```

4. 输入 `/diff` 并查看更改的 TypeScript 文件。留意新生成的 TSDoc 注释，并确认它们准确说明了代码。

## 总结和后续步骤

你已了解 Copilot CLI 如何读取指令文件中的上下文，并将新的规范应用于功能。具体来说，你：

- 了解存储库指令和按路径限定的指令文件如何传达给智能体；
- 更新指令文件，确保遵循编码规范；
- 查看指令文件对代码的影响。

接下来，你将[自定义并运行可重复使用的 quality-checks 技能][next-lesson]，确保 lint 和测试能够一致地运行。

## 资源

- [为 Copilot CLI 添加自定义指令][instruction-files]
- [自定义指令支持][custom-instructions-support]
- [创建自定义指令的最佳实践][instructions-best-practices]
- [Awesome Copilot — 指令文件合集及其他资源][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
