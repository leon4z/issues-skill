# Issues Skill

`issues` is a lightweight agent skill for keeping project-local issues from getting lost during review, debugging, implementation, or design discussion.

It is more structured than a TODO list and lighter than a full issue tracker. The skill records each issue with a problem statement, decision, acceptance criteria, and verification notes in the current project's `ISSUES.md`.

## What It Is For

- Capturing actionable issues found during coding, testing, review, or discussion
- Keeping unresolved decisions visible without promoting them into a formal tracker too early
- Turning loose follow-ups into items that can later be implemented and verified
- Maintaining a local issue buffer for solo developers and agent-assisted workflows

## What It Is Not For

- Methodology, lessons learned, or reusable operating principles
- Benchmark conclusions, research findings, or general documentation
- Architectural or product decisions that have already been made and have no follow-up work
- General status summaries or handoff notes unrelated to existing issues
- Team notification or permission workflows
- Long discussion threads
- Release planning
- Cross-repository issue management
- Replacing GitHub Issues, Jira, Linear, or another formal tracker

Phrases such as "record this", "remember this", or "先记下来" do not make something an issue by themselves. An item belongs in `ISSUES.md` only when it represents future project work or an unresolved choice with a meaningful completion condition.

Queries, status summaries, and handoffs that explicitly concern existing issue IDs or `ISSUES.md` remain part of the skill.

## Skill Layout

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

The installable skill is the `issues/` directory.
The behavior evals cover issue capture and operations on an existing ledger. The trigger eval set contains balanced positive and near-miss prompts for checking that generic phrases such as "record this" do not cause false activation.

## Installation

Copy or import the `issues/` directory into an agent system that supports reusable instruction folders or skill-like prompts. If your platform requires a manifest or marketplace metadata, keep `issues/SKILL.md` as the source of truth and adapt only the packaging fields.

## Agent Compatibility

The skill is plain Markdown workflow guidance. It can be adapted to any agent system that supports reusable instruction folders or skill-like prompts. Some platforms may require small packaging changes, such as different metadata fields, install paths, or marketplace manifests.

## Core Issue Format

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

`Links` is optional. Omit it when there is no useful reference.

## Status Model

- `open`: recorded but not fully decided.
- `ready`: decision and acceptance are clear enough to implement.
- `implemented`: implemented and verified, waiting for explicit cleanup.
- `blocked`: cannot proceed until missing information or dependency is resolved.
- `dropped`: user decided not to do it, waiting for explicit cleanup if desired.

## Example

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

## Publishing Status

Status: alpha.

This repository is ready for an initial public release under the MIT License.
