# Agent Domain Docs

This repository uses a single root domain glossary:

- `CONTEXT.md` for canonical project/domain language
- `docs/adr/` for meaningful architecture, product, workflow, testing, or repo-structure decisions

Do not create `CONTEXT-MAP.md` for now. Do not create a large `docs/agents/workflow.md`. Workflow rules live in skills. Repo-local docs only configure the project.

## Reading Rules

Before planning, implementation, diagnosis, architecture review, or zoom-out, read:

1. `CONTEXT.md` for domain language
2. `docs/agents/issue-tracker.md`
3. `docs/agents/triage-labels.md`
4. `docs/agents/domain.md`
5. relevant ADRs in `docs/adr/`
6. relevant source files and existing tests

## CONTEXT.md

`CONTEXT.md` is a glossary and nothing else. It defines the canonical terms this project uses and the fuzzy synonyms agents should avoid.

It should include only:

- a short context name and description
- a `## Language` section
- project-specific terms with one or two sentence definitions
- `_Avoid_:` entries for synonyms, overloaded words, or misleading terms

It should not include implementation details, issue tracking rules, source folder maps, PRD indexes, implementation plans, scratch notes, or general programming concepts.

## ADRs

Create ADRs only when meaningful decisions crystallize and future agents should not re-litigate them.

ADRs may be brief. A single paragraph is acceptable if it records:

- what decision was made
- why it was made
- what future agents should not re-litigate

Do not create ADRs for every small implementation detail.
