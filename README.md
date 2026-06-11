# Coding Agent Starter

This repository is a small starter kit for projects that want durable, reusable
instructions for coding agents.

It provides a lightweight structure for:

- repository-local agent skills
- task lifecycle documents
- execution-ready task briefs
- issue drafting
- quantified milestones
- specs maps that connect product behavior to tests and code comments

The goal is not to prescribe one heavy process. The goal is to give agents and
humans a shared set of files that make work easier to start, continue, review,
and hand off.

## Project Structure

```text
.
├── .agents/
│   └── skills/
│       ├── draft-issue/
│       │   └── SKILL.md
│       ├── quantified-milestone/
│       │   └── SKILL.md
│       ├── task-brief/
│       │   └── SKILL.md
│       ├── task-lifecycle/
│       │   └── SKILL.md
│       ├── tmux-agent-master/
│       │   └── SKILL.md
│       └── tmux-worker-steward/
│           └── SKILL.md
└── docs/
    ├── specs_map/
    │   └── AGENTS.md
    └── tasks/
        ├── backlog/
        │   └── .gitkeep
        ├── doing/
        │   └── .gitkeep
        ├── done/
        │   └── .gitkeep
        └── trash/
            └── .gitkeep
```

## Skills

Repository-local skills live under:

```text
.agents/skills/<skill-name>/SKILL.md
```

Each skill is a focused operating guide for agents.

Current skills:

- `draft-issue`: draft concise GitHub issues with Context, Problem, Goals, and
  Acceptance Criteria.
- `task-brief`: turn an issue or request into an execution-ready task brief.
- `task-lifecycle`: move task files through `backlog`, `doing`, `done`, and
  `trash`.
- `quantified-milestone`: rewrite vague goals into measurable milestones.
- `tmux-agent-master`: create, register, inspect, and route tmux-backed worker
  agents.
- `tmux-worker-steward`: delegate work to tmux workers, supervise progress, and
  review worker output before trusting it.

## Task Lifecycle

Task documents move through:

```text
docs/tasks/backlog/
docs/tasks/doing/
docs/tasks/done/
docs/tasks/trash/
```

Use this flow:

```text
backlog -> doing -> done
              \-> trash
```

Default meanings:

- `backlog`: ideas and task briefs that are not started yet
- `doing`: active work
- `done`: completed and shipped work
- `trash`: abandoned or superseded work

## Specs Map

Specs maps live under:

```text
docs/specs_map/
```

Read `docs/specs_map/AGENTS.md` before creating or changing specs.

Specs maps are for stable product behavior and technical contracts. Code and
tests may reference specs with short comments such as:

```text
// Spec: docs/specs_map/<file>.yaml#<spec_id>
```

Do not put long implementation plans or debugging notes in specs maps. Use
`docs/tasks/`, `docs/plans/`, or knowledge-base documents for longer context,
then link to them from the spec.

## Usage Examples

### 1. Draft A GitHub Issue

Use `draft-issue` when the desired output is an issue description rather than
an implementation plan.

Example request:

```text
Use draft-issue to write an issue for making the settings page remember the
last selected workspace.
```

Expected issue shape:

```text
## Context
## Problem
## Goals
## Acceptance Criteria
```

### 2. Turn An Issue Into A Task Brief

Use `task-brief` when a request is ready to become an actionable task.

Example request:

```text
Use task-brief to create a backlog task for the workspace settings issue.
```

Default saved location:

```text
docs/tasks/backlog/YYYY-MM-DD-HH-mm-<short-title>.md
```

Expected task brief shape:

```text
## Background
## Goals
## Execution Plan
## Acceptance Criteria
## Validation Commands
```

### 3. Move Work Through The Task Lifecycle

Use `task-lifecycle` when work changes state.

Example requests:

```text
Move the workspace settings task from backlog to doing.
Mark the workspace settings task done.
Move the old onboarding task to trash.
```

The skill manages documentation flow only. It does not merge branches, close
pull requests, or delete worktrees.

### 4. Quantify A Milestone

Use `quantified-milestone` when a goal sounds useful but cannot be judged.

Vague goal:

```text
Make the onboarding flow better.
```

Quantified goal:

```text
The onboarding flow lets a new user create an account, create one project, and
reach the first usable workspace screen on desktop and mobile. Validate with one
automated happy-path test and screenshots for mobile narrow and desktop wide.
```

### 5. Connect Code To Product Behavior

Use `docs/specs_map/` when product behavior or technical contracts should stay
stable across refactors.

Example workflow:

1. Add or update a spec in `docs/specs_map/<domain>.yaml`.
2. Add tests that verify the behavior.
3. Add short `Spec:` comments only at fragile implementation boundaries.
4. Keep long rationale in task briefs, plans, or knowledge-base docs.

### 6. Coordinate Tmux Worker Agents

Use `tmux-agent-master` when a project has tmux-backed worker agents and needs
to create, register, inspect, or route work across them.

Use `tmux-worker-steward` as the pair skill when assigning concrete work. The
master chooses or creates the worker; the steward writes the assignment,
supervises progress, and reviews the answer before it drives implementation or
user-facing conclusions.

## Recommended Workflow

For a typical change:

1. Use `draft-issue` to describe the problem and desired outcome.
2. Use `task-brief` to turn the issue into a concrete task in
   `docs/tasks/backlog/`.
3. Use `task-lifecycle` to move the task into `doing` when work starts.
4. Update `docs/specs_map/` if behavior or technical contracts change.
5. Use `quantified-milestone` when a goal needs clearer completion criteria.
6. Use `tmux-agent-master` and `tmux-worker-steward` when work benefits from
   supervised tmux-backed worker agents.
7. Move the task to `done` when the work is shipped and verified.
