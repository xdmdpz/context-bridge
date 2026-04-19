# context-bridge

`context-bridge` 是一个基于 Git 的多 Agent 协作上下文仓。

它的作用不是做“万能记忆系统”，而是把协作里最容易丢失的内容固定下来：

- 项目背景
- 当前状态
- 任务交接
- 执行回执
- 跨项目边界

这样做的结果是：

- 可追踪
- 可复盘
- 可复用
- 少依赖口头转述

## 适合的场景

- Web AI 负责规划和拆任务
- 本地 coding agent 负责执行
- 跨项目协作需要显式落库
- 长周期项目需要持续对齐上下文

## 核心原则

1. Git 是事实源
2. 项目标识以 `source_repo` 为准
3. 状态写 `current_snapshot.md`
4. 稳定事实写 `project_profile.md`
5. 任务流必须走 `handoff → 执行 → feedback`
6. 所有协作必须显式、可追踪、可复盘

## 运行模型

- 项目任务：默认由所属项目相关 agent 处理
- 全局任务：规则、README、onboarding、registry 维护等，可由合适 agent 处理
- 跨项目任务：允许，但必须把 handoff / feedback 落库到 Git

## 快速入口

- [`docs/index.md`](docs/index.md)
- [`docs/architecture.md`](docs/architecture.md)
- [`docs/quickstart.md`](docs/quickstart.md)
- [`docs/onboarding.md`](docs/onboarding.md)
- [`docs/project-model.md`](docs/project-model.md)
- [`docs/agent-routing.md`](docs/agent-routing.md)
- [`examples/README.md`](examples/README.md)
- [`CONTRIBUTING.md`](CONTRIBUTING.md)
- [`LICENSE`](LICENSE)

## 目录概览

```text
context/
  projects/
    registry/
    _template/
  agents/
    registry/
    bindings/
  system/

docs/
  index.md
  architecture.md
  quickstart.md
  onboarding.md
  project-model.md
  agent-routing.md
examples/
  README.md
  2026-04-19-example-note.md
  task-handoff.example.json
  task-feedback.example.json
```

## 约定

- `project_profile.md` 记录长期稳定信息
- `current_snapshot.md` 记录当前状态
- `handoffs/` 记录任务输入
- `feedback/` 记录执行输出

## 目标

让 Agent 协作更简单、更稳定、更少重复沟通。
