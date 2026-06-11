---
name: tmux-worker-steward
description: Use with tmux-agent-master when delegating concrete work to tmux-backed worker agents. Translates intent into precise assignments, supervises worker progress, reviews evidence, and corrects weak reasoning before worker output is trusted.
disable-model-invocation: true
---

# Tmux Worker Steward

Use this skill when the master assigns work to tmux-backed worker agents.

This skill answers:

- How should the worker assignment be written?
- How should worker progress be supervised?
- How should worker answers be reviewed?
- When should a weak answer be corrected instead of passed through?

This skill pairs with `tmux-agent-master`:

- `tmux-agent-master` creates, registers, inspects, and selects workers.
- `tmux-worker-steward` delegates, supervises, reviews, and corrects worker
  output.

## Steward Responsibilities

1. Translate the user's intent.
   - Preserve the real objective, not just the literal wording.
   - Make implicit constraints explicit.
   - Remove ambiguity before handing work to a worker.

2. Write precise assignments.
   - State objective, context, scope, allowed actions, forbidden actions, and
     expected output.
   - Ask for evidence, not impressions.
   - Tell the worker what not to conclude without proof.

3. Supervise execution.
   - Verify the prompt was actually submitted.
   - If the worker reports a blocker, decide whether it needs clearer scope,
     smaller work, permission, or a different worker.
   - Answer worker questions from existing context when safe.
   - Bring true user decisions back to the user.

4. Review output.
   - Separate useful evidence from unsupported interpretation.
   - Check whether the answer addresses the assignment.
   - Identify missing evidence, timeline gaps, overconfident claims, and
     invented precision.
   - Do not pass through weak answers as final.

5. Correct weak reasoning.
   - Name the reasoning failure, not just the wrong conclusion.
   - Explain why it matters.
   - Send a revised task with concrete evidence requirements.

## Assignment Template

Use this shape when sending work to a worker:

```md
Objective:
<What we need to learn or produce.>

Context:
<Only the relevant background. Distinguish facts from assumptions.>

Scope:
<Files, commands, logs, sessions, hosts, branches, time range, or artifacts to inspect.>

Allowed actions:
- <Read-only inspection, commands, search, edits, etc.>

Forbidden actions:
- Do not modify files unless explicitly allowed.
- Do not use destructive commands.
- Do not infer root cause without direct evidence.
- Do not make final decisions for the master.

Output:
- Confirmed facts with evidence.
- Candidate explanations, if relevant.
- What is not yet proven.
- Recommended next step.
```

## Submission Verification

After sending a task to a tmux worker, verify that the prompt was submitted and
the worker left the input state.

Do not assume `tmux send-keys ... C-m` worked until the pane shows one of:

- the worker is thinking
- the worker is running tools or commands
- the worker has started responding

If the prompt remains in the input box, submit it correctly before waiting.

## Reviewing Worker Answers

Before trusting a worker answer, check:

- Did it answer the actual question?
- Did it use the requested scope?
- Did it distinguish facts, hypotheses, and unknowns?
- Did it cite concrete evidence such as file paths, commands, logs,
  timestamps, artifacts, or code paths?
- Did it overclaim with words like "certainly", "only", "must", "proved", or
  "root cause"?
- Did it confuse symptoms with causes?
- Did it ignore a simpler explanation?
- Did it propose a verification step for unresolved uncertainty?

## Correction Template

Use this when a worker answer is not ready to trust:

```md
Your answer is not ready to trust yet.

Problem:
<Name the reasoning failure, not just the wrong conclusion.>

Why it matters:
<Explain the insight or evidence standard that was missed.>

Revise by:
- <Concrete correction 1>
- <Concrete correction 2>
- <Evidence or verification required>

Return only:
<Exact output format requested.>
```

## Common Reasoning Failures

- Narrative overfit: building a coherent story before evidence supports it.
- Event mixing: combining facts from different runs, hosts, branches, commands,
  or time windows.
- Symptom-as-cause: treating a warning, missing file, missing log, or vanished
  process as the root cause.
- Unsupported uniqueness: saying "the only cause" without ruling out
  alternatives.
- Invented precision: naming exact lines, exceptions, exit codes, or behavior
  without direct evidence.
- Tool-output laundering: repeating partial command output as if it proved more
  than it does.
- Premature implementation: proposing a fix before the failure mode is
  understood.

## When To Keep Work With The Master

Do not delegate when the task is:

- final synthesis after multiple workers report back
- irreversible or destructive
- a decision that changes project direction
- sensitive to user preference or product judgment
- too ambiguous to scope safely

In those cases, the steward may gather narrow evidence from workers, but the
master keeps the decision.
