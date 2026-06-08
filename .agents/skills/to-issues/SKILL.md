---
name: to-issues
description: Break a PRD, plan, or issue into approval-gated GitHub implementation issues using independently grabbable vertical slices. Use when a [PRD] GitHub Issue or approved plan should become child issues for agent implementation.
---

# To Issues

Turn a source PRD or plan into GitHub implementation issues. GitHub Issues are the source of truth; do not create local draft issue files, `.scratch/`, or `docs/prd/*-issues.md`.

## Rules

- Use GitHub Issues only.
- Prefer thin vertical slices over phase or layer tickets.
- Do not create horizontal tickets such as "create schema", "build API", "add UI", or "write tests" unless setup work is truly required.
- Every non-PRD issue must include `## Dependencies`.
- Draft the breakdown in chat and get human approval before publishing issues.
- Publish child issues in dependency order so real issue numbers can be referenced.
- Do not close, edit, or mark complete the parent `[PRD]` issue.
- Do not implement code, create branches, open PRs, or merge PRs.

## Start

Read `AGENTS.md` or `CLAUDE.md`, `docs/agents/issue-tracker.md`, `docs/agents/triage-labels.md`, `docs/agents/domain.md`, `CONTEXT.md`, relevant ADRs in `docs/adr/`, and the current conversation context.

If the input names a GitHub issue, fetch it; then verify GitHub is usable:

```bash
gh issue view {NUMBER} --json number,title,body,labels,state,url,comments
gh auth status
gh repo view --json nameWithOwner,defaultBranchRef
gh label list
```

If setup docs, GitHub auth, or canonical labels are missing, stop and say exactly what is missing. Suggest `setup-agent-workflow`.

## Draft Vertical Slices

Break the source into child issues where each issue is a small, complete, independently testable improvement.

For each proposed issue, show:

- **Title**: short user-facing or behavior-facing title
- **Mode**: `AFK` or `HITL`
- **Label**: usually `ready-for-agent`; use `ready-for-human` only when exact human action is required
- **Blocked by**: issue titles or `None`
- **Acceptance criteria**: 2-5 externally verifiable checks
- **Source coverage**: PRD user stories, requirements, or decisions covered

Ask the user to approve the breakdown before creating issues. Good slices deliver one narrow behavior end to end, include validation/tests, can be reviewed independently, and preserve a dependency DAG. Setup-only issues are allowed only when required to unlock future vertical slices, and must have concrete acceptance criteria.

## Issue Body

Use this body for normal implementation, refactor, docs, and chore issues:

```markdown
## Source PRD
#{prd_issue_number}

## Goal
What this issue should accomplish.

## Scope
What is included and excluded.

## Acceptance criteria
- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Criterion 3

## Dependencies
- None
```

If there are dependencies, write `- Depends on #{issue_number}` in `## Dependencies`.

Add `## Notes` only for useful context, links, glossary terms, ADRs, edge cases, or suggested tests.

## Publish

Only after approval, create issues with temporary body files outside the repo:

```bash
gh issue create \
  --title "{Issue title}" \
  --body-file "/tmp/{slug}-issue.md" \
  --label "{ready-for-agent|ready-for-human}"
```

After all child issues are created, comment on the parent PRD issue. The parent `[PRD]` issue remains open until all child issues are completed, deferred, moved out of scope, or marked `wontfix`.

```bash
gh issue comment {PRD_NUMBER} --body "Implementation issues created from this PRD:
- #{issue_number} {Issue title}
- #{issue_number} {Issue title}"
```

## Report

Summarize the created issues, dependency order, HITL issues, AFK-ready issues, parent PRD comment, and recommended next workflow: `triage` or implementation on the first unblocked `ready-for-agent` issue.
