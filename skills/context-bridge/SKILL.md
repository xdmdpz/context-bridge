# Skill: context-bridge

## 目的

把 `context-bridge` 的文档规则、项目结构和任务流变成一个统一的执行入口。

这个 skill 负责把“应该怎么协作”变成“现在该怎么做”。

## 适用场景

- 新项目初始化
- 已有项目接入
- 任务执行
- 任务回传
- 更新项目快照
- 更新文档索引

## 输入

- `docs/index.md`
- `docs/architecture.md`
- `context/system/`
- `context/projects/registry/`
- `context/projects/<project-id>/project_profile.md`
- `context/projects/<project-id>/current_snapshot.md`
- 最新 `handoff`

## 输出

- 任务执行结果
- `feedback/` 回执
- `current_snapshot.md` 更新
- 必要时更新 `docs/index.md`

## 执行顺序

1. 读取仓库当前 Git 状态
2. 确认 `project_id` 与 `source_repo`
3. 读取项目注册信息
4. 读取 `project_profile.md`
5. 读取 `current_snapshot.md`
6. 读取最新 `handoff`
7. 按任务执行
8. 写回 `feedback`
9. 更新 `current_snapshot.md`
10. 如果新增或更新了 `docs/`，先同步 `docs/index.md`

## 约束

- 只认当前项目目录，不跨目录写错位置
- 所有任务都要落到对应项目的 `handoffs/`
- 所有结果都要落到对应项目的 `feedback/`
- 稳定事实只写进 `project_profile.md`
- 当前状态只写进 `current_snapshot.md`
- 不把过程材料塞进 `docs/`

## 最低要求

- 路径正确
- 项目标识正确
- 回执完整
- 快照已更新
- 文档索引已同步

## 说明

这个 skill 是 `context-bridge` 的 canonical 执行入口。它不是替代文档，而是承接文档、把文档变成动作。
