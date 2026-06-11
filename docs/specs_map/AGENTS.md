# Specs Map Instructions

This directory records product behavior specs and cross-cutting technical
contracts. These specs are the source for tests and for short implementation
comments at fragile boundaries.

## Scope

- Use one YAML file per product domain, user flow, or technical contract group.
- Product behavior and UX specs describe what the product should do, in terms a
  user or tester can understand.
- Technical contracts describe cross-cutting runtime correctness, platform
  behavior, lifecycle safety, data contracts, and build prerequisites.
- Specs must match the current intended behavior unless the task explicitly asks
  to redefine the product behavior or technical contract.
- Keep each `expected_behavior` item short, concrete, and testable.
- Link longer rationale to `docs/plans/`, `docs/tasks/`, `docs/kb/`, or other
  supporting docs through `references`.

## Do Not Include

- Do not include code paths, test paths, owners, timestamps, or version fields.
  Git already tracks history, and code paths change during refactors.
- Do not use this directory for implementation plans, design essays, evaluation
  results, debugging notes, or code-path inventories. Link those documents from
  `references` instead.
- Technical contracts must state the required behavior, not the current
  implementation design. For example, require long-running work to stay off the
  main UI thread; do not name a specific worker class unless that class is part
  of the public contract.
- Do not add speculative behavior. If code and intended behavior differ, call
  that out in the task discussion before changing the spec.

## File Shape

Use this shape for each specs map file:

```yaml
purpose: >
  Define expected product behavior, UX contracts, or cross-cutting technical
  contracts for <domain, flow, or technical group>. Specs are the source for
  tests and implementation comments. Specs may link to longer rationale docs,
  but do not track code paths.

specs:
  - spec_id: stable_snake_case_id
    expected_behavior:
      - A short, concrete behavior statement.
      - Another testable behavior statement.
    references:
      - docs/plans/example.md
```

## Referencing Specs

- Tests may reference a spec with a short comment:
  `// Spec: docs/specs_map/<file>.yaml#<spec_id>`
- Production code may reference a spec only at business or technical boundaries
  that are easy to accidentally regress:
  `// Spec: docs/specs_map/<file>.yaml#<spec_id>`
- Do not reference long-form plan, task, or KB docs directly from code when a
  spec exists. Code and tests should point to the spec; the spec points to
  background docs.
- Every `Spec:` comment must point to an existing specs map file and an existing
  `spec_id` in that file.

## Maintenance

- When changing user-visible behavior or cross-cutting technical requirements,
  update or add the relevant spec first, then align implementation and tests.
- When refactoring code without changing behavior, do not edit specs.
- When a test expectation conflicts with a spec, treat the spec as the starting
  point for discussion: either update the spec because the product behavior
  changed, or fix the test.
- Before finalizing behavior changes, check that each changed requirement maps
  to a concrete test assertion.
- If code contains a `Spec:` comment for a missing `spec_id`, fix the specs map
  or the comment before treating the work as complete.
