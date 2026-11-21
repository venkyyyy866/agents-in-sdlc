---
title: "课程 7 - 创建并使用 QA 智能体"
description: "创建 QA 自定义智能体，将议题要求、quality-checks 技能和 Playwright MCP 整合起来。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

你已使用 `quality-checks` 技能运行自动检查，也使用 Playwright MCP 在浏览器中查看筛选体验。现在，你将通过自定义智能体整合这些功能，并定义清晰的 QA 流程。

在本课程中，你将：

- 了解自定义智能体如何与指令、技能和 MCP 工具协作；
- 创建并检查可重复使用的质量保证配置；
- 选择 QA 智能体，根据筛选议题审查其发现。

## 场景

Tailspin Toys 希望在创建拉取请求（PR）前，一致地审查需求、代码质量、自动检查、测试覆盖率和浏览器行为。自定义智能体可以协调 QA 流程，并生成可重复使用的报告。

## 什么是自定义智能体？

自定义智能体是通过 Markdown 配置文件定义的 Copilot 专用版本。配置文件说明智能体的用途、指令和可用工具。在本研讨会中，你将在 `.github/agents/qa.agent.md` 中定义 QA 角色，然后在 Copilot CLI 中选择它。

你使用过的自定义功能各有用途：存储库指令说明团队标准；`quality-checks` 技能封装可重复执行的检查；Playwright MCP 提供浏览器工具；QA 配置文件则告诉 Copilot 如何利用这些能力评估需求并报告发现。它们彼此互补，无需额外开启另一个会话。

## 创建 QA 配置文件

创建功能 PR 前，先让 Copilot 创建一个可重复使用的 QA 配置文件。该配置文件将定义 QA 执行的检查及其必须遵循的边界。

1. 返回 Codespace，并确认筛选会话处于 Interactive 模式。
2. 请默认智能体创建新的自定义智能体：

   ```plaintext
   创建一个名为 QA 的自定义智能体，保存到 .github/agents/qa.agent.md。它应根据议题和已达成一致的要求检查功能，遵循存储库指令，运行 quality-checks 技能，使用 Playwright MCP 验证行为，并在测试覆盖不足时添加测试。

   对每项要求报告通过、失败或受阻状态，并提供支持证据。修改实现代码前必须先询问，而且不得提交更改或创建拉取请求。

   现在只创建配置文件，供我审查。
   ```

## 检查配置文件

使用新智能体前，先检查其配置文件，确认 Copilot 捕捉到了预期的 QA 流程和边界。这样可以避免你只想验证功能时，智能体却以不完整或过宽泛的方式修改功能。

1. 输入 `/diff`，然后打开 `.github/agents/qa.agent.md`。
2. 阅读 frontmatter。`description` 是必需的；`name` 是可选的，但添加它可以为智能体提供清楚的显示名称。
3. 阅读配置文件中的指令，确认 QA 会从需求出发、遵循存储库指令、运行 `quality-checks` 技能并使用 Playwright MCP。
4. 确认 QA 会提供支持证据；修改实现代码前会先询问；不会提交更改或创建拉取请求。
5. 如果生成的配置文件遗漏了上述职责或边界，请先让默认智能体修改，再继续。

## 根据议题运行 QA

Copilot CLI 会在会话启动时加载项目智能体。创建配置文件后，恢复同一个筛选会话并选择 QA，这样它就能使用现有上下文中的议题和规划决定。

1. 输入以下提示启用智能体：

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> 你刚创建的智能体可能不会立即出现在可用智能体列表中。它仍然可用，上述命令会启用它。

2. 使用以下提示，请 QA 智能体审查功能：

   ```plaintext
   根据议题和我们计划中确定的事项审查筛选功能。它是否已准备好创建 PR？
   ```

3. QA 智能体将开始工作！
4. 完成后，阅读它提供的报告。

## 总结和后续步骤

你已在工作流中添加了可重复使用的专用角色，并审查了它的工作。在本课程中，你：

- 了解自定义智能体如何与指令、技能和 MCP 工具协作；
- 创建并检查了可重复使用的质量保证配置；
- 选择了 QA 智能体，并根据筛选议题审查了它的发现。

现在，实现、技能更新、QA 配置文件、测试和验证报告都已准备好供审查。接下来，你将[将这些内容汇总到功能 PR 中，并使用 Agent Merge][next-lesson]。

## 资源

- [为 Copilot CLI 创建自定义智能体][create-agents]
- [自定义智能体配置][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
