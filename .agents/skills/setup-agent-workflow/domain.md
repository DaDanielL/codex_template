# Agent Domain Docs

This repository uses a single lightweight context map:

- `CONTEXT.md` for project overview, domain language, important source folders, and where to find context
- `docs/adr/` for meaningful architecture, product, workflow, testing, or repo-structure decisions

Do not create a large `docs/agents/workflow.md`. Workflow rules live in skills. Repo-local docs configure project context.

## Reading Rules

Before planning, implementation, diagnosis, architecture review, or zoom-out, read:

1. `CONTEXT.md`
2. `docs/agents/issue-tracker.md`
3. `docs/agents/triage-labels.md`
4. `docs/agents/domain.md`
5. relevant ADRs in `docs/adr/`
6. relevant source files and existing tests

## CONTEXT.md

`CONTEXT.md` is a lightweight context map, not a giant knowledge base and not a PRD index.

It should include:

- project overview
- important source folders
- where agent config lives
- where ADRs live
- where issue tracking lives
- core domain terms when useful

It should not manually list every PRD because PRDs live in GitHub Issues.

## ADRs

Create ADRs only when meaningful decisions crystallize and future agents should not re-litigate them.

ADRs may be brief. A single paragraph is acceptable if it records:

- what decision was made
- why it was made
- what future agents should not re-litigate

Do not create ADRs for every small implementation detail.
