---
name: task-brief
description: Use when drafting, revising, or persisting an execution-ready task brief for a feature, bug fix, refactor, documentation update, or other repository change. Bridges draft issues into docs/tasks work items with Background, Goals, Execution Plan, Acceptance Criteria, and Validation Commands.
---

# Task Brief

Use this skill when the user asks for a plan, task brief, implementation brief,
execution plan, or when a GitHub issue or product request needs to become an
actionable task document.

This skill is for execution-ready task planning. It is distinct from:

- `draft-issue`: defines the need, problem, goals, and acceptance criteria.
- `task-lifecycle`: moves task files through `backlog`, `doing`, `done`, and
  `trash`.

## Persistence Rule

When a task brief should be saved, place it under `docs/tasks/backlog/` unless
the user explicitly says the work is already in progress or complete.

Use a timestamped filename:

```text
YYYY-MM-DD-HH-mm-<short-kebab-title>.md
```

Append a timezone suffix when useful or already established by the repository:

```text
2026-06-11-14-30-+08-add-user-skills.md
```

## Default Structure

Write the task brief in English using these sections, in this order:

```md
# <Short Task Title>

## Background

<Plain background text, or optional subsections when they help.>

### Context

<Optional: current state and relevant existing behavior.>

### Problem

<Optional: limitation, pain point, bug, or gap.>

### Motivation

<Optional: why the change is valuable.>

## Goals

- <Outcome-oriented goal 1>
- <Outcome-oriented goal 2>

## Execution Plan

1. <Phase or step 1>
2. <Phase or step 2>
3. <Phase or step 3>

## Acceptance Criteria

- <Testable and user-observable outcome 1>
- <Testable and user-observable outcome 2>

## Validation Commands

- `<command 1>`
- `<command 2>`
```

## Background Rules

- `Context`, `Problem`, and `Motivation` are optional subsections.
- Use only the subsections that fit the request size and type.
- For small or obvious changes, write direct prose under `Background` without
  subsections.
- For larger or ambiguous changes, prefer the optional subsections to separate
  current state, pain points, and value.

## Writing Rules

- Write task briefs in English unless the user explicitly asks for another
  language.
- Keep the brief execution-oriented, not product-marketing-oriented.
- Keep display names and stable storage identities separate when defining
  extensible configuration systems.
- Include validation commands as their own section, not inside acceptance
  criteria.
- Make acceptance criteria testable and user-observable where possible.
- Mention specs map updates when the change affects user-visible behavior or a
  cross-cutting technical contract.
- Mention task lifecycle placement when saving the brief, such as
  `docs/tasks/backlog/` for not-yet-started work.
- Avoid implementation trivia, but include enough phased detail that another
  agent or human can execute the work.

## Quality Checklist

Before returning or saving the task brief, check:

- The brief uses `Background`, `Goals`, `Execution Plan`, `Acceptance Criteria`,
  and `Validation Commands`.
- Optional Background subsections are used only when they improve clarity.
- Goals describe outcomes, not internal implementation steps.
- Acceptance criteria describe observable or verifiable outcomes.
- Validation commands are relevant to the touched area.
- If saved, the file lives in the correct `docs/tasks/` lifecycle folder.
- If behavior or technical contracts change, the brief calls out the expected
  specs map update.
