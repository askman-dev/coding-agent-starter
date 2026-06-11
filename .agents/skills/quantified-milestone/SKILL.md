---
name: quantified-milestone
description: Use when drafting, reviewing, or revising milestone goals for engineering, product, documentation, research, evaluation, or agent work. Guides agents to replace vague success language with measurable completion criteria while keeping the milestone structure flexible.
---

# Quantified Milestone

Use this skill when the user asks for a milestone, next goal, handoff goal, work
package, experiment goal, or asks whether a goal is clear enough for an AI or
human to execute.

This skill is not a rigid template. The core rule is:

```text
Turn important adjectives into measurable completion criteria.
```

Agents often write milestones that sound useful but cannot be judged, such as
"improve quality", "make it stable", "run enough tests", "build a usable first
version", or "validate the design". A quantified milestone defines what "done"
means with numbers, thresholds, comparison targets, explicit coverage, or
pass/fail checks.

## When To Apply

Apply this skill whenever a milestone includes vague words such as:

- better, stronger, improved
- enough, sufficient, usable, complete
- larger, smaller, faster, slower
- stable, reliable, robust
- high quality, good, acceptable
- validate, test, evaluate, compare
- production ready, reviewable, releasable

Do not force every milestone into the same headings. Preserve the user's
natural structure when possible, but add measurable criteria where the goal
would otherwise be ambiguous.

## Quantification Checklist

For each important goal, ask whether at least one of these is specified:

- **Count**: records, cases, screens, files, samples, tests, commits, runs.
- **Coverage**: categories, sources, platforms, modes, user flows, edge cases.
- **Ratio**: pass rate, completion rate, error rate, coverage rate, accuracy.
- **Threshold**: minimum acceptable value or maximum allowed value.
- **Comparison**: baseline artifact, previous version, current production path,
  known-good behavior, or fixed reference implementation.
- **Budget**: time, memory, file size, latency, CPU, cost, token usage.
- **Failure handling**: what to report and commit if the target is not reached.
- **Artifacts**: exact output files, reports, manifests, logs, screenshots, test
  results, or pull requests that prove completion.

## Rewrite Examples

Prefer concrete criteria over vague direction:

```text
Improve the onboarding flow.
```

Becomes:

```text
Update the onboarding flow so a new user can complete account setup, create one
project, and reach the first usable workspace screen on desktop and mobile.
Validate with one automated happy-path test and two screenshots: mobile narrow
and desktop wide.
```

```text
Make the UI stable.
```

Becomes:

```text
The target flow completes 20 consecutive runs on desktop and mobile viewports
with no severe console errors, no overlapping controls in screenshots, and no
failed interaction checkpoint.
```

```text
Write better docs.
```

Becomes:

```text
Create or update the docs page so it defines the feature, lists the supported
states, includes one minimal example, links to the relevant task or spec, and
removes any outdated behavior claims from the old page.
```

## Engineering Milestones

For implementation work, quantify:

- supported platforms or modes
- required user flows
- exact tests or evidence runs
- failure states that must be handled
- performance, size, or cost limits when relevant
- migration, compatibility, or rollback requirements

Avoid claiming "done" because code exists. Completion requires evidence that
the behavior works under the stated conditions.

## Product And Documentation Milestones

For product or documentation work, quantify:

- what a user can do after the change
- which concepts, states, or terms must be defined
- which pages, sections, or examples must be updated
- which outdated descriptions must be removed
- which acceptance criteria can be checked by a human reviewer
- which specs, tasks, or plans must be linked as supporting context

Keep product goals outcome-oriented. Avoid turning them into implementation
task lists unless the user explicitly asks for a delivery plan.

## Research And Evaluation Milestones

For experiments, do not require success when the outcome is genuinely unknown.
Instead, quantify the experiment and require a useful conclusion:

```text
Run at least N trials under fixed settings. If the target is not met, commit the
report and state the leading hypothesis for why the experiment failed.
```

Good research milestones include:

- a fixed baseline
- fixed settings shared by baseline and candidate
- minimum sample size
- success threshold
- negative-result reporting requirement
- required artifact paths

## Good Final Check

The milestone is ready when another agent or human can answer these questions
without reading the original chat:

- What does done mean?
- How will it be verified?
- Where will the proof live?
- What baseline or current behavior is it compared against?
- What happens if the target is not reached?
- What is explicitly out of scope?

If any answer is missing, tighten the milestone before treating it as ready.
