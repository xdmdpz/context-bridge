# Project Model

先看 [`docs/index.md`](./index.md)。

## Identity

- `source_repo` = project identity
- `project_id` = repo 内部映射主键

## Lifecycle

- registered
- initialized
- activated

## Context Split

- `project_profile` = stable
- `current_snapshot` = current

## Execution Layer

- canonical skill = [`skills/context-bridge/SKILL.md`](../skills/context-bridge/SKILL.md)
- 任务、回传、快照更新都通过这个 skill 统一处理
