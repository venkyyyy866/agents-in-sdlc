---
title: "课程 2 - 添加星级评分：快速改进"
description: "使用 Copilot CLI 对游戏卡片进行小幅改进，在转发的浏览器中审查，并通过第一个拉取请求合并更改。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

安装 Copilot CLI 并尝试对话后，现在可以开始对项目进行第一次更改了。先从小处着手：游戏数据中已有星级评分，但主页上的游戏卡片尚未显示评分。你将让智能体显示评分、审查更改，并通过第一个拉取请求合并它。

在本课程中，你将：

- 在功能分支上启动专注于单一任务的 Copilot 对话；
- 请智能体对项目进行小幅更改；
- 使用 `/diff` 审查更改；
- 运行应用，并在转发的浏览器中确认更改；
- 创建并合并第一个拉取请求。

## 场景

Tailspin Toys 中的每款游戏都有星级评分，详情页已经显示评分。但主页上的游戏卡片只显示标题、类别、发行商和描述。作为热身练习，你将让智能体在每张卡片上显示现有评分。这项更改小而独立，非常适合作为第一次会话任务。

## 对话的组成部分

**对话**是你使用 Copilot CLI 处理任务的工作区。与 Copilot app 不同，普通 CLI 对话使用终端当前检出的存储库和 Git 分支，而不是创建专用工作树。保存的对话允许你稍后返回同一讨论，而文件和分支仍是磁盘上的普通 Git 状态。

对话中有三项内容：你发出的提示和智能体的回复；智能体探索和编辑文件时执行的工具操作；以及可以使用 `/diff` 检查的更改。

## 开始对话并请求更改

我们来启动一个新对话，开始实现功能。

1. 返回 Codespace。
2. 如果终端尚未打开，按 <kbd>Control</kbd>+<kbd>\`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>\`</kbd>（Windows/Linux）。
3. 如果 Copilot 尚未启动，请运行以下命令：

   ```bash
   copilot --yolo
   ```

4. 输入斜杠命令 `/new` 并按 <kbd>Enter</kbd>，确认已启动新会话。
5. 使用以下提示请求更改：

   ```plaintext
   在列表页的游戏卡片上显示每款游戏的 5 星制 `starRating`。如果评分为 null，则显示“暂时没有评分”。保持卡片布局不变，添加测试并运行相关检查。
   ```

Copilot 会探索项目，找到用于显示游戏详情的文件，并创建所需代码。你已使用 Copilot CLI 添加了新功能！

## 审查差异

所有 AI 生成的更改在合并前都应经过审查，即使更改很小也不例外。现在，我们在 Copilot CLI 中查看更改。

1. 输入 `/diff` 并检查每个更改的文件。
2. 确认游戏卡片在有评分时显示数字评分，在 `starRating` 为 `null` 时显示“暂时没有评分”。
3. 确认测试覆盖了两种状态。
4. 查看 Copilot 运行的检查结果，并要求它修复任何失败项。
5. 审查完成后，按 <kbd>Esc</kbd> 退出差异界面。

> [!NOTE]
> 与所有生成式 AI 工具一样，Copilot 具有概率性而非确定性，因此生成的代码可能各不相同。请审查其行为，而不是要求某种固定实现。

## 检查更改

当然，我们不能只阅读代码就认定它能正常工作。接下来让 Copilot 启动网站，以便我们在 Codespaces 转发的浏览器中检查更新后的用户界面（UI）。

1. 请 Copilot 启动应用：

   ```plaintext
   启动应用，以便我在浏览器中检查星级评分更改。告诉我 URL，并让服务器保持运行。
   ```

2. Codespaces 报告端口 `4321` 可用时，选择 **Open in Browser**。
3. 确认游戏卡片显示了 5 星制评分。
4. 返回 Copilot，请它停止启动的服务器：

   ```plaintext
   停止你启动的开发服务器。
   ```

## 创建并合并第一个拉取请求

你已完成新功能！现在创建拉取请求（PR），将代码合并到项目中。

1. 请默认智能体提交更改：

   ```plaintext
   使用合适的提交消息提交已审查的星级评分更改。
   ```

2. 输入 `/pr create`。创建 PR 时，Copilot CLI 会推送现有提交并显示 PR URL。
3. 按住 <kbd>Command</kbd>（Mac）或 <kbd>Ctrl</kbd>（Windows/Linux），然后选择 Copilot CLI 显示的 URL，以打开 PR。
4. 审查更改的文件和检查结果。
5. 准备就绪后，选择 **Merge pull request**，然后确认合并。
6. 返回 Codespace，输入 `/exit` 退出 Copilot CLI。
7. 更新本地 `main` 分支：

   ```bash
   git checkout main
   git pull
   ```

## 总结和后续步骤

恭喜你，你已使用 GitHub Copilot CLI 发布了第一个更改！具体来说，你：

- 在功能分支上启动了专注于单一任务的 Copilot 对话；
- 引导智能体对游戏卡片进行小幅更改；
- 使用 `/diff` 审查更改；
- 运行应用，并在转发的浏览器中确认星级评分；
- 创建并合并了第一个拉取请求。

接下来，你将[从筛选议题开始，使用 Plan 和 Autopilot 模式][next-lesson]构建更大的功能。

## 资源

- [关于 GitHub Copilot CLI][about-copilot-cli]
- [Copilot CLI 命令参考][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
