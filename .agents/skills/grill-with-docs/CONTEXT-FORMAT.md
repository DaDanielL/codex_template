# CONTEXT.md Format

`CONTEXT.md` is a lightweight context map that helps agents find the right project and domain context quickly.

Use this structure:

```markdown
# Project Context

## Overview

One or two short paragraphs describing what the project is, who it serves, and what the current product or engineering goal is.

## Important Source Folders

| Path | Purpose |
|------|---------|
| `src/example` | What future agents should look here to understand. |

## Agent Configuration

| File | Purpose |
|------|---------|
| `docs/agents/issue-tracker.md` | GitHub Issues source-of-truth rules and issue formats. |
| `docs/agents/triage-labels.md` | Canonical workflow labels and label transitions. |
| `docs/agents/domain.md` | Context and ADR reading rules. |

## Issue Tracking

Planned work lives in GitHub Issues. PRD issues use the `[PRD]` title prefix.

## ADRs

Meaningful decisions live in `docs/adr/`.

## Domain Terms

**Canonical Term**:
One or two sentences defining what this term is in this project.
_Avoid_: overloaded synonym, misleading synonym
```

## Rules

- Be concise and opinionated.
- Prefer canonical domain language over vague synonyms.
- Include only facts that help future agents orient.
- Keep implementation plans, PRDs, issue drafts, and scratch notes out of `CONTEXT.md`.
- Do not manually list every PRD because PRDs live in GitHub Issues.
