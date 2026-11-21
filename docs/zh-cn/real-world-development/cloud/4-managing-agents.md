---
title: "练习 4 - 监控和管理智能体"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

在前几项练习中，你让 Copilot 云智能体处理了三项任务，重点是改善用户体验和添加功能。云智能体虽然能够异步自主工作，但监控这些任务仍然很重要。

你可以使用多种工具管理分配给云智能体的任务，包括 GitHub.com 上的[智能体页面][agents-page]。在这个任务控制中心，你可以查看所有创建了开放拉取请求（PR）的智能体任务，了解它们执行的操作，甚至可以引导正在进行的会话。

在本课中，你将：

- 浏览智能体页面，监控云智能体任务。
- 引导正在进行的会话，请求添加其他功能。

## 场景

将高对比度模式任务分配给智能体后，团队意识到也可以同时添加浅色模式。既然正在更新网站样式并添加切换功能，将浅色模式一并加入也很合理。你将引导智能体的工作，确保它同时添加浅色模式和高对比度模式。

## 查看 Copilot 云智能体任务

我们来查看当前分配给 Copilot 云智能体的所有任务的状态。

1. 打开 [Copilot agents 页面](https://github.com/copilot/agents)。
2. 留意主面板和左侧面板中的任务列表。你应该能看到分配给 Copilot 的任务，包括：
    - 更新代码库文档；
    - 生成用于修改游戏的 API；
    - 为网站添加高对比度模式。
3. 选择一个正在运行的任务，查看 Copilot 已执行的操作。这些操作可能包括：
    - 从存储库检出代码；
    - 为 Copilot 创建工作环境；
    - 设置 MCP 服务器；
    - 执行完成所分配任务所需的各种步骤。

> [!NOTE]
> 列出的具体步骤会因 Copilot 工作进度和采用的方法而异。

4. 还要留意右侧显示的拉取请求（PR）面板。你可以在这里查看 PR 和更改的文件，以便进一步监控任务。

## 引导云智能体

现在你已查看正在进行的任务，可以在 Copilot 实现高对比度模式的同时，让它也添加浅色模式。

1. 选择添加高对比度模式的会话。确切标题可能会因 Copilot 使用的名称和当前工作状态而异。

    ![任务控制中心中的无障碍会话](../../../_images/ex6-accessibility-session.png)

2. 观察会话几分钟，直到会话显示已完成设置并开始工作。出现类似下方的消息时，就说明已经开始工作。
3. 在 **Steer active session while Copilot is working** 对话框中，输入以下提示：

    ```plaintext
    添加高对比度模式的同时，也添加浅色模式。该模式也应有一个开关，供用户选择自己需要的显示模式。
    ```

    ![智能体页面中突出显示用于引导活动会话的 Copilot 任务对话框](../../../_images/ex6-steer-cloud-agent-task.png)

4. 按 <kbd>Enter</kbd> 发送提示。
5. 留意 Copilot 如何确认提示并将其纳入工作流程。

## 让 Copilot 继续工作

与之前一样，Copilot 会继续处理更新后的任务！收到消息时，它会先完成当前步骤，再将新请求加入工作流程。

如前所述，这需要几分钟；正好可以暂停一下，回顾目前学到和探索的内容。

## 总结和后续步骤

本课介绍了 Copilot agents 页面，这是监控和引导 GitHub Copilot 云智能体任务的中心位置。在这个任务控制中心，你可以跟踪所有进行中和已完成的任务、审查智能体正在执行的工作，也可以重定向正在运行的任务，调整范围或提供更多指导。

你了解了以下内容：

- 使用任务控制中心和智能体页面监控云智能体任务。
- 重定向正在进行的会话，请求添加其他功能。

Copilot 正在完成功能开发，接下来我们将[迭代改进 Copilot 创建的拉取请求][next-lesson]。

## 资源

- [Copilot agents 页面][agents-page]
- [关于自定义智能体][custom-agents]

---

| [← 上一课：自定义智能体][previous-lesson] | [下一课：迭代改进 Copilot 的工作 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
