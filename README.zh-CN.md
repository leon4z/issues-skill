# Issues Skill

`issues` 是一个轻量级 agent skill，用来在评审、排障、实现或设计讨论过程中，把项目里的可执行问题先记录下来，避免丢失。

它比 TODO 更结构化，比完整 issue tracker 更轻。这个 skill 默认把问题写入当前项目的 `ISSUES.md`，每个问题都包含问题描述、决策、验收条件和验证记录。

## 适用场景

- 记录编码、测试、评审或讨论中发现的可执行问题
- 在不急着进入正式跟踪系统时，保留未解决的决策点
- 把零散后续事项整理成之后可以实现和验证的条目
- 给个人开发者和 agent 协作流程提供本地 issue 缓冲区

## 不适用场景

- 方法论、经验总结或可复用的工作原则
- Benchmark 结论、研究发现或一般性文档
- 已经确定且没有后续工作的架构或产品决策
- 与既有 Issue 无关的一般状态总结或 handoff 记录
- 团队通知或权限流程
- 长讨论串
- 发布计划
- 跨仓库 issue 管理
- 替代 GitHub Issues、Jira、Linear 或其他正式跟踪系统

“记录一下”“先记下来”等表达本身不代表这是一个 issue。只有当内容指向未来仍需完成的项目工作或尚未解决的选择，并且能够说明完成条件时，才应写入 `ISSUES.md`。

如果查询、状态总结或 handoff 明确涉及已有 Issue ID 或 `ISSUES.md`，仍然属于这个 skill 的适用范围。

## 目录结构

```text
issues-skill/
  README.md
  README.zh-CN.md
  LICENSE
  issues/
    SKILL.md
    evals/
      evals.json
      files/
        ISSUES.md
      trigger-evals.json
```

可安装的 skill 是 `issues/` 目录。
行为评测覆盖新 Issue 的捕获以及对既有 Issue 台账的操作。触发评测集包含数量均衡的正例和易混淆反例，用来检查“记录一下”等泛化表达不会造成误触发。

## 安装

把 `issues/` 目录复制或导入到支持可复用 instruction 目录或类似 skill 提示词机制的 agent 系统中。如果目标平台需要 manifest 或 marketplace 元数据，请以 `issues/SKILL.md` 作为行为来源，只适配外层打包字段。

## Agent 兼容性

这个 skill 的核心是普通 Markdown 工作流说明。只要某个 agent 系统支持可复用的 instruction 目录或类似 skill 的提示词机制，就可以适配使用。不同平台可能只需要调整元数据字段、安装路径或 marketplace 描述文件。

## 核心 issue 格式

```md
## I-001 Short Title

Status: open
Area: UI / feature / docs / tests / behavior
Source: YYYY-MM-DD discussion
Updated: YYYY-MM-DD
Links: optional

Problem:
What is wrong or unclear from the user's perspective.

Decision:
The agreed direction. Leave as `TBD` if not settled.

Acceptance:
- Observable condition that proves the issue was handled.

Verification:
- pending
```

`Links` 是可选项。没有有价值的参考链接时直接省略。

## 状态模型

- `open`：已记录，但决策还不完整。
- `ready`：决策和验收条件已经足够清楚，可以实现。
- `implemented`：已经实现并验证，等待用户明确清理。
- `blocked`：缺少信息或依赖，暂时无法继续。
- `dropped`：用户决定不做，等待用户明确清理。

## 示例

```md
## I-002 Import preview should show all blocking conflicts

Status: ready
Area: Import / review flow / error display
Source: 2026-05-19 review
Updated: 2026-05-19
Links: https://github.com/example/project/issues/42

Problem:
The import preview stops at the first blocking conflict. Users need to see all conflicts before deciding whether to continue.

Decision:
Show every actionable blocking conflict in the preview, grouped by affected item.

Acceptance:
- The preview lists all blocking conflicts found in one scan.
- Each conflict includes enough context for the user to decide the next action.
- Non-blocking warnings remain visually separate from blocking conflicts.

Verification:
- pending
```

## 发布状态

状态：alpha。

这个仓库已经可以按 MIT License 做首次公开发布。
