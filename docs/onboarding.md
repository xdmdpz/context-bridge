# Onboarding

先看 [`docs/index.md`](./index.md)。

## 目标

把一个已有项目接入 `context-bridge`，并且统一走 [`skills/context-bridge/SKILL.md`](../skills/context-bridge/SKILL.md)。

## 步骤

1. 确认 `source_repo`
2. 创建 `project_id`（或复用已有）
3. 初始化 `project_profile` / `current_snapshot`
4. 注册到 `registry`
5. 走一条 `handoff -> feedback`

## 关键点

- 项目标识由 `source_repo` 决定
- 同 repo 不应创建多个 project
- 不要通过目录名猜项目
- 初始化后直接进入 canonical skill，不再拆分多个入口
