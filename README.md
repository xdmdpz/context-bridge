# context-bridge

一个基于 Git 的多 Agent 协作上下文模板。

`context-bridge` 不是一个“万能记忆系统”，而是解决多 Agent 协作中的核心问题：

- 项目背景反复解释
- 任务状态反复同步
- Web 侧与本地代码现实逐渐脱节

本项目通过 **Git + 结构化上下文文件**，让多 Agent 协作变得：

- 可追踪
- 可复盘
- 可复用

---

## 核心设计

### 1. 仓库即事实源

所有共享信息必须写入仓库，而不是只存在于对话中。

---

### 2. 项目标识（Project Identity）

项目以 `source_repo` 为唯一标识：

- 同一个 Git 仓库 = 同一个项目
- 名称相似 ≠ 同一个项目
- task / feedback 路径不作为判断依据

---

### 3. 项目生命周期

一个项目通常经历：

- registered（已注册）
- initialized（已初始化）
- activated（已跑通任务流）

只有出现 handoff → feedback 才算真正激活。

---

### 4. 上下文分层

#### project_profile
长期稳定信息：

- 架构
- 规则
- 入口
- 约束

#### current_snapshot
当前状态：

- 当前目标
- 进度
- 阻塞
- 下一步

---

### 5. 任务流（核心）

所有任务必须走：

```text
handoff → 执行 → feedback
```

否则不算真实执行。

---

### 6. Agent 路由规则

- 默认：项目 agent 处理本项目任务
- 全局任务：任意 agent 可执行
- 支持 agent ↔ agent 派发任务
- 跨项目必须走 handoff / feedback

---

## 推荐目录结构

```text
context/
  projects/
    <project-id>/
      project_profile.md
      current_snapshot.md
      handoffs/
      feedback/

  agents/
    registry/
    bindings/

  system/
    rules.md
    project-identity.md
    agent-routing.md
```

---

## 最小规则

1. 任务必须写入 handoff
2. 执行结果必须写入 feedback
3. 状态写 snapshot，不写 profile
4. 项目标识以 repo 为准
5. 协作必须可追踪

---

## 适用场景

- ChatGPT 规划 → 本地 agent 执行
- 多 agent 协作开发
- 长周期项目上下文同步

---

## 快速开始

见：docs/quickstart.md

---

## 目标

让 Agent 协作：

- 更简单
- 更稳定
- 更少重复沟通
