---
name: issues
description: Use for actionable project-local work items that need a lifecycle such as open, ready, implemented, and verified, and for operations on existing issue IDs or ISSUES.md. Trigger when the user wants to capture, query, organize, implement, hand off, or clean up a bug, fix, TODO, follow-up action, unresolved project decision, named issue ID, or existing issue ledger. Do not trigger for methodology, lessons learned, reusable principles, completed architectural decisions, research findings, benchmark conclusions, general documentation, or handoffs and status summaries unrelated to existing issues, even when the user says "记录一下", "先记下来", "record this", or "remember this". If such content is explicitly turned into a follow-up item with a closure condition, it can be captured as an issue.
---

# Issues

Use this skill to keep lightweight project issues from getting lost while discussion is still evolving. It is intentionally local and minimal: the default storage is `ISSUES.md` at the current project root, and the workflow must not assume GitHub, Jira, Linear, OpenSpec, or any other external tracker.

This is not a GitHub Issues replacement. It is a local issue buffer for agent-assisted work: more structured than a TODO list, lighter than a project tracker, and focused on making each item actionable, decidable, acceptable, and verifiable.

## Publishing Notes

- Publish this skill as a lightweight local issue ledger, not as a full issue tracker.
- Keep the model small. Do not add labels, assignees, milestones, priorities, project boards, comments, or sync behavior unless the user explicitly asks for them.
- The key value is the execution loop: `Problem` -> `Decision` -> `Acceptance` -> `Verification`.
- `Links` is optional. Add it only when there is a useful reference such as a discussion, pull request, external issue, spec, or design note.
- This skill is suitable for solo developers, agent-assisted coding sessions, review follow-ups, and temporary issue queues before work is promoted into a formal planning flow.
- This skill is not suitable for team notification, permission control, long discussion threads, release planning, or cross-repository issue management.

## Core Rules

1. Capturing or organizing issues does not imply implementation.
2. Record only actionable issues with a future action or unresolved choice and a meaningful closure condition.
3. Prefer updating an existing issue over creating a duplicate.
4. Keep item IDs stable. Do not renumber existing items.
5. Implemented issues stay in `ISSUES.md` until the user explicitly asks to clean them up or approves a cleanup suggestion.
6. Never delete issues during implementation. You may remind the user that implemented issues are ready for cleanup, but cleanup still requires explicit user approval.
7. When implementing issues, follow the current project's normal planning, editing, testing, documentation, and commit rules.
8. If a turn is issue-linked because the user named an issue id, `ISSUES.md` was read for the task, or an issue was implemented or updated, preserve that issue context through later verification, handoff, archive, or commit steps.
9. If a turn reads or modifies `ISSUES.md`, the final handoff must report all currently `implemented` issue IDs and count, even when they were not touched in the current turn, and remind the user they are ready for cleanup but require explicit approval.

## Classification Gate

Apply this gate only before capturing or creating a new issue. Do not use it to block queries, organization, implementation, handoff, or cleanup involving an existing issue ID or `ISSUES.md`; enter the corresponding workflow directly for those operations.

A new candidate belongs in the issue ledger only when:

1. It describes unresolved project work, a defect, a follow-up action, or a decision that still needs to be made.
2. A next action such as implement, investigate, decide, or verify can be named.
3. An observable completion or closure condition can be stated.
4. Tracking a lifecycle status is useful.

If these conditions are not met, do not create an issue. Route the information according to its purpose and the project's existing conventions:

| Information type | Preferred destination |
| --- | --- |
| Bug, fix, TODO, follow-up action, or unresolved project decision | `ISSUES.md` |
| Reusable methodology, lesson learned, or operating principle | Methodology or knowledge document |
| Architectural or product decision already made | Decision record |
| Benchmark observation, result, or research finding | Benchmark or research report |
| Current project state or continuity context | README, status document, or handoff |

Words such as "问题", "issue", "测试发现", "记录一下", or "先记下来" are not sufficient by themselves. Infer the intended artifact from the surrounding conversation and project structure. If the intent remains genuinely ambiguous and choosing the wrong artifact would materially change the result, ask one concise clarification instead of defaulting to `ISSUES.md`.

## Storage

Default file:

`ISSUES.md`

If the file does not exist and the user asks to record issues, create it with this skeleton:

```md
# Issues

This file tracks lightweight project issues. Implemented items stay here until the user explicitly asks to clean them up or approves a cleanup suggestion.

## Active Issues

_No active issues._
```

If project rules require another location, use the project-native location and mention that choice briefly.

## Item Format

Use this format for each item:

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
- Another observable condition if needed.

Verification:
- pending
```

Omit `Links` when there is no useful reference.

## Statuses

- `open`: recorded but not fully decided.
- `ready`: decision and acceptance are clear enough to implement.
- `implemented`: implemented and verified, waiting for explicit cleanup.
- `blocked`: cannot proceed until missing information or dependency is resolved.
- `dropped`: user decided not to do it, waiting for explicit cleanup if desired.

## Capture Workflow

Use this workflow in either of two cases:

1. The user asks to create a new issue and the classification gate is satisfied.
2. The user asks to update only the ledger fields of an existing issue; the new-item classification gate does not apply.

Mentioning an issue ID does not select this workflow by itself; route by the requested action. For example, "implement I-004" uses the Implementation Workflow, while "change I-004 acceptance criteria" uses this capture/update workflow. Generic capture phrases such as "record this", "remember this for later", or "先记下来" activate this workflow only when the surrounding context clearly describes future project work with a closure condition.

1. Read `ISSUES.md` if it exists.
2. Identify whether this is new or updates an existing item.
3. Record the smallest useful version of the issue.
4. Use `ready` only when the decision and acceptance are clear.
5. Use `open` when the problem is clear but the decision is still being discussed.
6. Add `Links` only when there is a useful reference.
7. Do not edit code.

## Boundary Examples

Should trigger:

- "把这个 bug 记到 `ISSUES.md`，后面修复。"
- "标题切分需要优化，先记为待办；验收标准是 FP052 重跑后命中正确制度。"
- "实现 I-004，并在测试通过后更新状态。"
- "这个方案还没定，记一个 issue 跟踪选型和验收结果。"
- "交接前列出 `ISSUES.md` 中所有 implemented 条目和当前状态。"

Should not trigger:

- "把这次测试暴露的问题沉淀成企业知识库建设方法论。"
- "记录一个原则：不能依赖人工审核每个文档标题。"
- "把 PDF Benchmark 的结果和结论整理进报告。"
- "记录我们已经确定的架构选择和原因。"
- "把目前做到哪里写进 handoff，方便下个 Agent 接手。"

## Organize Workflow

When the user asks to review, sort, or organize issues:

1. Read `ISSUES.md`.
2. Merge duplicates.
3. Split unrelated concerns into separate items.
4. Promote items from `open` to `ready` only when decision and acceptance are explicit.
5. Mark stale items as `blocked` or `dropped` only when the user agrees or the project facts clearly make them obsolete.
6. Do not edit code unless the user explicitly asks to implement.

## Implementation Workflow

When the user asks to implement issues:

1. Read `ISSUES.md`.
2. Select only `ready` items unless the user names specific items.
3. Present a short checklist grouped by implementation area.
4. Follow the current project's normal implementation and verification rules.
5. After verification, update completed items to `implemented` and add concise verification notes.
6. Do not remove implemented items.
7. In the final response, list the touched issue ids and current statuses, and say how many implemented issues remain ready for cleanup.

## Handoff Workflow

When the current turn is issue-linked and the work reaches final handoff, archive, or commit:

1. Re-read or re-check `ISSUES.md` if it may have changed since the issue was last updated.
2. Report the touched issue ids and current statuses.
3. Report the full set of currently `implemented` issue ids and the total count, even if some were not touched this turn.
4. If any issue is currently `implemented`, remind the user it is ready for cleanup, but cleanup still requires explicit approval.
5. If the implementation flow switched into another flow, such as proposal, archive, or commit prep, do this issue handoff after that flow completes and before the final response.

## Cleanup Workflow

Only clean up issues when the user explicitly asks or approves a cleanup suggestion, for example "clean implemented issues", "清理已完成 issues", or "删除 I-003".

1. Read `ISSUES.md`.
2. Remove only the requested items or statuses.
3. Preserve `open`, `ready`, and `blocked` items unless the user explicitly includes them.
4. If no active items remain, keep the skeleton and `_No active issues._`.
5. Do not treat implementation completion as cleanup permission.

## Examples

### Capture an undecided issue

```md
## I-001 Settings page copy is unclear

Status: open
Area: UI / settings / copy
Source: 2026-05-19 discussion
Updated: 2026-05-19

Problem:
The settings page uses similar labels for two different actions, so users may not know which action changes the active configuration.

Decision:
TBD

Acceptance:
- The confusing labels are identified and replaced with distinct user-facing wording.
- The revised wording makes the action outcome clear before the user confirms.

Verification:
- pending
```

### Capture a ready issue with a reference

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

### Mark an issue as implemented

```md
## I-003 Export history should keep verified results visible

Status: implemented
Area: Export / history
Source: 2026-05-19 discussion
Updated: 2026-05-19

Problem:
Users cannot tell which export entries were successfully verified after a rerun.

Decision:
Keep the verified result visible on each export history entry.

Acceptance:
- Successful reruns show a verified state in the history list.
- Failed reruns keep the previous result visible and show the new failure separately.

Verification:
- Implemented and verified with focused history flow checks.
```
