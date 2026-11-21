---
title: "练习 2 - 使用 Copilot 智能体模式添加功能"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

即使是最简单的应用更新，通常也需要修改多个文件并执行一些操作，例如运行测试。作为开发者，你通常需要找到所有相关文件、进行更改、运行测试、调试、找出遗漏的文件、再进行修改……要做的事情远不止这些。

Copilot 智能体模式正是为此而设计的。

Copilot 智能体模式可在 IDE 中更自主地工作。它的行为类似开发者：先探索现有项目结构，再执行所需更新、运行测试等任务，并自动修复发现的问题。我们来了解如何使用智能体模式为网站添加新功能。

> [!NOTE]
> 智能体模式和云智能体的名称相似，但它们针对不同的使用场景。智能体模式在 IDE 中执行任务，支持快速反馈和交互。云智能体则像团队成员一样异步工作，通过议题和拉取请求与你协作。

在本练习中，你将了解如何：

- 使用 Copilot 智能体模式探索项目、找到相关文件并协调执行更改；
- 使用 GitHub Copilot 智能体模式跨 UI 和数据层实现新功能；
- 在将代码合并到代码库前审查 Copilot 智能体模式生成的更改和测试。

## 场景

游戏列表不断增长，你希望用户能够按类别和发行商筛选游戏。你已在上一练习中添加发行商辅助函数，现在将使用 Copilot 智能体模式完成剩余的数据层、UI 和测试工作。

## 运行 Tailspin Toys 网站

进行任何更改前，我们先了解 Tailspin Toys 网站的当前功能。

此网站是一个以开发者为主题的桌游众筹平台。用户可以浏览游戏列表和详情。网站是单体 Astro 应用，会在构建时将页面渲染为静态 HTML。页面通过 frontmatter 使用 Drizzle ORM 直接查询本地 SQLite 数据库；它没有单独的后端 API 或客户端 UI 框架。可重复使用的数据访问辅助函数放在 `src/lib/` 中，交互功能通过使用标准 DOM API 的小型、限定范围的 Astro `<script>` 添加。

### 启动网站

为了方便运行网站，项目提供了 `npm run dev` 任务，用于启动单体 Astro 开发服务器。按照以下步骤即可在 GitHub Codespace 中运行：

1. 返回 Codespace。上一练习完成后，当前应处于 `main` 分支。
2. 在 Codespace 中按 <kbd>Control</kbd>+<kbd>\`</kbd>（Mac）或 <kbd>Ctrl</kbd>+<kbd>\`</kbd>（Windows/Linux）打开新的终端窗口。
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

   Astro 开发服务器准备就绪后，会显示类似以下内容的横幅，其中包含 URL：

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> 如果弹出对话框，询问是否要为 `http://localhost:4321` 打开浏览器窗口，请选择 **x** 将其关闭。

5. 在终端中按住 <kbd>Command</kbd>（Mac）或 <kbd>Ctrl</kbd>（Windows/Linux），然后选择 Astro 服务器地址 `http://localhost:4321`，打开网站。

> [!NOTE]
> 在 Codespace 中，从终端选择 localhost URL 链接时，会自动将其重定向到 `https://<your-codespace-name>-4321.app.github.dev/`。这是连接到 Codespace 的专用隧道，此时 Web 服务器正在 Codespace 中运行！

### 浏览网站

网站运行后，你可以探索其功能。主要功能包括：

- **主页**：显示桌游列表，包括标题、图片和描述。
- **游戏详情页**：选择游戏后，会打开详情页，其中显示标题、描述、发行商和类别等信息。

## 使用 Copilot 浏览待办列表

> [!TIP]
> **打开 Copilot Chat**
>
> 开始以下练习前，返回 Codespace，打开 Copilot Chat 面板，并选择 **New Chat** 开始干净的对话。不同练习所需的模式和模型可能不同；需要时会在具体步骤中说明。

网站的初始实现已经可用，但我们希望添加新功能来改进它。先查看待办列表。根据模板设置项目时，系统已自动创建了一组议题；请 GitHub Copilot 显示这些项目。

1. 在 Chat 视图的智能体下拉列表中选择 **Agent**。**Agent** 智能体可以自主规划并跨文件实现更改、运行终端命令和调用工具。

   ![Copilot Chat 视图中的智能体选择器示意图。](../../../_images/shared-chat-mode-selector.png)

2. 从可用模型列表中选择 **Claude Sonnet 4.5**。

> [!CAUTION]
> 本研讨会作者并未偏好某个模型。编写本研讨会时，我们使用了 Claude Sonnet 4.5，因此在说明中列出了该模型。我们希望获得的代码建议相对一致，从而带来良好体验。不过，由于大语言模型具有概率性，你可能会发现建议与本研讨会所述内容不同。这完全正常，符合预期。

> [!NOTE]
> 由于大语言模型具有概率性，Copilot 可能会使用不同的 MCP 命令，但仍应该能够完成任务。

3. 向 Copilot 发送以下提示，询问待办议题：

   ```plaintext
   请显示我 GitHub 存储库中的待办事项，并帮助我按对用户最有用的程度进行优先级排序。
   ```

4. 选择 **Continue**，允许运行列出所有议题的命令。
5. 查看生成的议题列表。

留意 Copilot 会根据它认为对用户最有用的程度为项目排序。

## 查看指令文件

让智能体生成代码前，先查看将用于向 Copilot 提供工作上下文的指令文件。我们将使用[用户界面（UI）](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md)指令文件，其中包含向网站添加功能时的参考信息。

1. 在 Codespace 中打开 `.github/instructions/ui.instructions.md`。
2. 留意其中关于添加功能的总体指导，包括：
   - 架构概述；
   - 组件设计、可测试性和无障碍原则；
   - 指向多种文件类型的专用指令文件的链接，包括：
     - Astro；
     - Tailwind CSS；
     - Drizzle。

> [!TIP]
> 指令文件可以引用其他指令文件和项目中的文件。路径相对于指令文件所在位置。这样可以重复使用内容，将复杂指令拆分成更易管理的部分，并提供示例和模板。

## 实现筛选功能

要完成筛选功能，至少需要对应用程序进行三项独立更新：

- 在数据层（`src/lib/`）中添加或完善剩余筛选逻辑；
- 添加或更新筛选行为测试；
- 更新游戏列表页面，加入筛选 UI。

此外，在将更改合并到代码库前，需要运行并通过测试。Copilot 智能体模式可以为你完成这些任务！现在来添加功能。

1. 你可以继续当前 Copilot 对话，也可以选择 **New Chat** 开始新对话。
2. 选择 **Add Context**、**Instructions** 和 **ui** 指令文件。

   ![选择 UI 指令文件的示意图](../../../_images/ex3-select-instructions-file.png)

3. 确认 Chat 视图的智能体下拉列表中仍选择了 **Agent**。

   ![Copilot Chat 视图中的智能体选择器示意图。](../../../_images/shared-chat-mode-selector.png)

4. 确认仍选择 **Claude Sonnet 4.5** 模型。
5. 使用以下提示，请 Copilot 根据待办列表中的相关议题实现功能：

   ```plaintext
   请根据待办列表中相关 GitHub 议题的要求，更新网站，加入按发行商和类别筛选的功能。上一练习已添加发行商辅助函数；完成其余的数据层、UI 和测试工作时，请保留并按需完善该函数。完成前确保所有测试均通过。服务器已经在运行，无需启动。
   ```

6. 观察 Copilot 如何先探索项目并找到相关功能文件。你应该能看到它找到数据层辅助函数、UI 和测试，然后开始修改文件并运行测试。

   ![Copilot 探索项目文件的示意图](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot 会执行多个任务，例如探索项目、修改文件和运行测试。根据任务和代码库的复杂程度，这可能需要几分钟。在此过程中，代码编辑器中可能会出现 **Keep** 和 **Undo** 按钮。Copilot 完成后，每项更改都会显示 **Keep** 或 **Undo** 按钮，因此无需在工作进行期间选择它们。

7. 按照 Copilot 的提示，选择 **Continue** 运行测试。

   ![Copilot Chat 面板中提示用户确认是否运行测试的对话框示意图](../../../_images/ex3-agent-mode-run-tests.png)

8. 过程中可能会出现暂停，也可能有测试失败。这没有关系！Copilot 会在代码生成和测试之间不断迭代，直到任务完成且未发现错误。

   ![Copilot 智能体模式完整聊天会话的示意图](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 检查生成的代码，查找潜在问题。

> [!CAUTION]
> 请记住，始终需要审查 Copilot 或其他 AI 工具生成的代码。

10. 返回正在运行网站的浏览器，试用新功能！
11. 确认一切正常并完成代码审查后，在 Copilot Chat 窗口中选择 **Keep**。

## 总结和后续步骤

恭喜你！本练习介绍了如何使用 GitHub Copilot 智能体模式为 Tailspin Toys 网站添加新功能。你了解了如何：

- 使用 GitHub Copilot 智能体模式跨 UI 和数据层实现新功能；
- 使用 Copilot 智能体模式探索项目、找到相关文件并协调执行更改；
- 在将代码合并到代码库前审查 Copilot 智能体模式生成的更改和测试。

接下来，我们将[使用 Playwright MCP 服务器测试功能][next-lesson]，并为其创建拉取请求。

### 奖励探索练习 — 实现分页

随着游戏列表不断扩充，需要添加分页。运用本练习中学到的技能，请 Copilot 更新网站以实现分页。需要考虑以下代码方面：

- 遵循现有最佳实践，包括使用已有指令文件；
- 考虑分页方式，例如是否允许用户选择每页大小，还是使用固定大小；
- 编写提示时，提供必要的指导，让 Copilot 按照你的设想实现分页；
- 可能需要通过 GitHub Copilot 迭代，请它进行更改并提供上下文。这是使用 Copilot 时的正常流程！

## 资源

- [Copilot 的 ask、edit 和 agent 模式：功能及适用场景][choose-mode]
- [VS Code 中的智能体模式][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
