# Quickstart

先看 [`docs/index.md`](./index.md)，再进入执行入口。

当前仓库的正式 skill 是：

- [`skills/context-bridge/SKILL.md`](../skills/context-bridge/SKILL.md)

## 1. Fork 仓库

Fork 本仓库到你自己的账号。

## 2. 新建项目

在 `context/projects/` 下创建目录：

```text
context/projects/<project-id>/
```

## 3. 初始化文件

创建：

- `project_profile.md`
- `current_snapshot.md`
- `handoffs/`
- `feedback/`
- `task-docs/`

## 4. 注册项目

在 `context/projects/registry/` 下新增 JSON：

- `project_id`
- `source_repo`

## 5. 跑一条任务

1. 写 `handoff`
2. skill 执行
3. 写 `feedback`

只有出现 `feedback`，项目才算激活。
