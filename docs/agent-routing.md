# Agent Routing

先看 [`docs/index.md`](./index.md)。

- 默认：项目 agent 处理本项目任务
- 全局任务：任意合适 agent
- 支持 agent -> agent
- 必须 handoff / feedback
- 执行层统一走 [`skills/context-bridge/SKILL.md`](../skills/context-bridge/SKILL.md)
