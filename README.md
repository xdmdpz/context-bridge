# context-bridge

一个基于 Git 的共享上下文仓库，用来连接网页聊天 AI、本地代码 agent、以及其他自动化 agent。

核心目标不是做“万能记忆库”，而是解决多 agent 协作中的三个现实问题：

1. 项目背景需要反复重讲
2. 当前任务进度需要反复同步
3. 网页侧对本地代码现实的认知会逐渐过时

因此，`context-bridge` 采用 **Git + 标准化上下文文件** 的方式，把真正需要跨 agent 共享的内容沉淀为可追踪、可审阅、可版本化的事实。

---

## 设计原则

- **Git 是事实源**：共享内容通过仓库文件沉淀，而不是散落在聊天记录里
- **总结优先，原文保留**：跨 agent 共享时优先使用总结后的结构化内容，必要时再回溯原文
- **任务交接优先**：先解决 handoff、反馈、快照同步，再考虑更复杂的长期记忆
- **格式统一**：不同 agent 读写同一批标准文件，降低人工搬运成本
- **渐进演化**：第一版先用文件规范跑通，后面再考虑 API / 自动化服务

---

## 仓库结构

```text
context/
  projects/
    demo-project/
      project_profile.md
      current_snapshot.md
      decisions.md
      open_questions.md
      handoffs/
        README.md
        example-handoff.json
      feedback/
        README.md
        example-feedback.json
schemas/
  task-handoff.schema.json
  task-feedback.schema.json
templates/
  project_profile.template.md
  current_snapshot.template.md
  decisions.template.md
  open_questions.template.md
```

---

## 四类核心对象

### 1. `project_profile`
项目的稳定事实层，用来描述项目是什么、边界是什么、长期约束是什么。

适合记录：
- 项目目标
- 当前职责分工
- 固定规则
- 关键文件/模块入口
- 长期约束

### 2. `task_handoff`
网页聊天 AI 或上游 agent 发给下游 agent 的任务包。

适合记录：
- 当前目标
- 相关背景
- 已确认约束
- 期望产出
- 待解决问题

### 3. `task_feedback`
本地 agent 或下游 agent 回传给网页侧的执行回执。

适合记录：
- 当前状态
- 已完成事项
- 修改过的文件
- 遇到的问题
- 需要确认的问题
- 给网页 AI 继续接手的摘要

### 4. `current_snapshot`
项目当前现实的快照，用来给网页聊天 AI 补课，减少认知过时。

适合记录：
- 当前目标
- 当前架构/模块状态
- 最近重要变更
- 已完成/未完成事项
- 当前风险与阻塞

---

## 建议协作流程

### 网页聊天 AI → 本地 agent
1. 基于讨论生成 `task_handoff`
2. 必要时更新 `project_profile` 或 `current_snapshot`
3. 本地 agent 读取任务包执行

### 本地 agent → 网页聊天 AI
1. 执行结束后写入 `task_feedback`
2. 如项目状态已明显变化，更新 `current_snapshot`
3. 网页聊天 AI 根据反馈继续分析、确认、下发下一轮任务

### 长期演进
- 被反复确认的稳定规则，写入 `project_profile`
- 关键决策写入 `decisions.md`
- 尚未拍板的问题写入 `open_questions.md`

---

## 约定建议

- 文件名尽量语义化，不依赖聊天平台
- 时间戳建议使用 ISO 8601
- `handoffs/` 与 `feedback/` 可按日期或任务编号组织
- 对于关键决策，优先写结论，不要只保存聊天原文
- 对于会变动很快的信息，优先更新 `current_snapshot`

---

## 下一步可扩展方向

- 为不同 agent 提供统一读写脚本
- 自动从对话生成 handoff / feedback
- 自动从代码仓库生成 snapshot 草稿
- 增加 `confirmed_decisions.jsonl` 等更强结构化索引
- 后续服务化为 API / MCP Server

---

## 适用场景

- ChatGPT 讨论思路，生成提示词，下发给本地代码 agent
- 本地 agent 执行后回传结果，网页侧继续多轮确认
- 项目开发一段时间后，用 snapshot 快速给网页 AI 拉齐认知
- 多个 agent 共享同一套项目事实与任务状态

`context-bridge` 的第一目标是 **减少重复解释与人工搬运**，而不是替代所有记忆系统。
