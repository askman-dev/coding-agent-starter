---
name: tmux-agent-master
description: Use when creating, registering, inspecting, or routing work across tmux-backed worker agents. Defines the worker registry, creation protocol, readiness checks, routing rules, and authority boundaries. Pair with tmux-worker-steward when assigning concrete work.
---

# Tmux Agent Master

Use this skill when a project coordinates tmux-backed worker agents.

This skill answers:

- Which worker agents exist?
- How should a new worker be created?
- What is each worker good for?
- Which worker should receive a given task?
- What must be verified before trusting that a worker is ready?

Pair it with `tmux-worker-steward` whenever the master assigns concrete work.
This skill manages the worker pool and routing. `tmux-worker-steward` manages
delegation, supervision, output review, and correction.

## Worker Registry

Each project should maintain a short worker registry before using tmux workers.
The registry may live in this skill, a project `AGENTS.md`, or another
repo-local instruction file.

Record each worker with:

```md
### <worker-name>

- Session: `<tmux-session-or-window>`
- Working directory: `<absolute-or-repo-relative-path>`
- Role: <primary role>
- Strengths: <what this worker is good at>
- Best use: <task shapes to send here>
- Cost profile: <cheap, moderate, expensive, scarce, etc.>
- Boundaries: <what this worker should not decide or do>
- Submission method: <Enter, Ctrl+Enter, headless command, or other verified path>
```

Keep worker identity separate from worker role. A model, CLI, or session can be
replaced while the role remains useful.

## Creation Protocol

Before creating a worker:

1. Define the worker role and why an existing worker is not enough.
2. Choose a stable session name that includes the project and role.
3. Choose the working directory.
4. Decide allowed actions: read-only, command execution, network/search,
   editing, or explicitly no destructive actions.
5. Decide how the worker will receive prompts and how readiness will be checked.

After creating a worker:

1. Verify the session exists.
2. Verify the process is running in the intended working directory.
3. Send a small visible probe or use the worker's non-interactive command mode.
4. Confirm the prompt was submitted, not merely typed into an input box.
5. Add or update the worker registry entry.

Useful inspection commands:

```bash
tmux list-sessions
tmux list-windows -a
tmux list-panes -a -F '#{session_name}:#{window_index}.#{pane_index} window=#{window_name} cmd=#{pane_current_command} cwd=#{pane_current_path} title=#{pane_title}'
tmux capture-pane -p -t <session-or-pane>
```

## Routing Rules

Match workers to task properties:

- Final judgment, code changes, or high-risk decisions: keep with the master.
- Second opinion, risk review, or competing design: use a strong reasoning
  worker.
- Broad repo search, document survey, or evidence gathering: use a scout worker.
- Cheap bounded summarization, counting, formatting, or checklist work: use a
  low-cost worker.

Do not delegate final authority. Worker output is advisory until reviewed by
the master or steward.

## Authority Boundaries

The master owns:

- task decomposition
- worker selection
- permission boundaries
- final synthesis
- deciding what evidence is trustworthy
- deciding whether code should change

Workers may:

- inspect files, logs, docs, artifacts, and process state within their scope
- produce summaries, candidate explanations, options, and recommendations
- run allowed commands when the project and user allow it

Workers must not:

- perform destructive actions without explicit approval
- make final release, merge, deletion, or irreversible infrastructure decisions
- treat their own output as accepted without master/steward review

## Readiness And Submission Checks

Never assume a tmux worker received a task just because text appears in the
pane. Verify one of:

- the worker is thinking
- the worker is running tools or commands
- the worker has started responding
- the non-interactive command returned an output artifact

If submission is uncertain, correct the interaction before waiting for results.

## Handoff To Steward

When assigning concrete work, hand off to `tmux-worker-steward` with:

- selected worker
- objective
- scope
- allowed actions
- forbidden actions
- expected output
- evidence requirements

The steward should supervise the worker and review the answer before it reaches
the user or drives implementation.
