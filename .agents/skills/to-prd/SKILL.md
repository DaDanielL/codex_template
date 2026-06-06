---
name: to-prd
description: Turn current conversation and codebase context into a [PRD] GitHub Issue labeled ready-for-agent. Use when setup-agent-workflow has configured the repo and the user wants to create a PRD from current context.
---

# To PRD

Create a source-of-truth PRD as a GitHub Issue. Do not interview the user; synthesize what is already known.

## Rules

- Use GitHub Issues only.
- Title PRD issues with `[PRD]`.
- Apply `ready-for-agent`.
- Do not create local PRD files in `.agents/PRDs/`, `docs/prd/`, or `.scratch/`.
- Do not create child implementation issues. Use `to-issues`.
- Do not implement code, create branches, open PRs, or close PRD issues.

## Start

Read `AGENTS.md` or `CLAUDE.md`, `docs/agents/issue-tracker.md`, `docs/agents/triage-labels.md`, `docs/agents/domain.md`, the root `CONTEXT.md` glossary, relevant ADRs in `docs/adr/`, current conversation context, and relevant source files if useful.

Verify GitHub is usable:

```bash
gh auth status
gh repo view --json nameWithOwner,defaultBranchRef
gh label list
```

If setup docs, GitHub auth, or the `ready-for-agent` label are missing, stop and say exactly what is missing. Suggest `setup-agent-workflow`.

## PRD Issue Body

Use this format:

```markdown
## Problem Statement

The problem from the user's perspective.

## Solution

The solution from the user's perspective.

## User Stories

A numbered list in this format: `As a {user}, I want {capability}, so that {benefit}.`

## Implementation Decisions

Known implementation decisions, such as modules, interfaces, technical clarifications, architecture, schema changes, API contracts, or interactions.

Do not include fragile file paths or code snippets unless a prototype snippet precisely captures an important decision.

## Testing Decisions

Known testing decisions, including what external behavior should be tested and any relevant existing test patterns.

## Out of Scope

What this PRD does not cover.

## Further Notes

Relevant context, links, glossary terms, ADRs, assumptions, or unresolved non-blocking notes.
```

## Publish

Create the issue with a temporary body file outside the repo:

```bash
gh issue create \
  --title "[PRD] {Title}" \
  --body-file "/tmp/{slug}-prd.md" \
  --label "ready-for-agent"
```

Do not commit or preserve the temporary file.

## Report

After publishing, summarize:

- PRD issue number and URL
- label applied
- key assumptions synthesized
- recommended next workflow: `to-issues`
