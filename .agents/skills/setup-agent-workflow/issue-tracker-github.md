# Agent Issue Tracker

GitHub Issues are the source of truth for planned work in this repository.

Use GitHub Issues for:

- PRDs
- vertical-slice implementation issues
- bug issues
- refactor issues
- planned docs issues
- planned chore/setup issues

Do not use `.scratch/`, `docs/prd/`, local duplicate issue drafts, or GitHub issue templates as core workflow artifacts.

## PRD Issues

PRDs are GitHub Issues with the title prefix `[PRD]`.

Example:

```text
[PRD] Build trade recommendation MVP
```

A PRD issue should stay open until every linked child issue is completed, deferred, moved out of scope, marked `wontfix`, or otherwise accounted for in PRD comments. PRD issues close manually after human review.

## Implementation Issues

Implementation issues created from a PRD must link back to the parent:

```markdown
Source PRD: #12
```

Child issues should be small vertical slices: complete, independently testable improvements. Avoid horizontal slices like "create database schema", "build API layer", or "add tests" unless a setup-only issue is truly required to unlock future vertical slices.

Every non-PRD issue must include:

```markdown
## Goal

## Scope

## Acceptance criteria

## Dependencies
- None

## Notes
```

Use `## Dependencies` for every feature, bug, refactor, docs, and chore issue. If dependencies exist, write them as `- Depends on #14`.

## Bug Issues

Bug and performance issues must include:

```markdown
## Observed

## Expected

## Reproduction

## Dependencies
- None

## Notes
```

A bug can be `ready-for-agent` only when it has observed behavior, expected behavior, a reproduction path or failing command/test, and dependencies.

## TDD Workflow

Behavior-changing `ready-for-agent` issues can go directly to `tdd` after triage. The `tdd` skill performs inline planning from the issue and Agent Brief, branches before code edits, and works in red-green-refactor cycles.

If automated TDD is impractical, the agent should explain why and use the closest verification method.

## PRs

Default traceability is one issue, one branch, one PR.

PR bodies should include:

```markdown
Closes #<issue-number>
```

The agent may open PRs for `ready-for-agent` issues after verification, but must not merge PRs or close PRD issues automatically.
