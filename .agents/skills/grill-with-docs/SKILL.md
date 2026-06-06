---
name: grill-with-docs
description: Clarify project and domain context through a question-by-question grilling session, updating CONTEXT.md and lightweight ADRs as decisions crystallize. Use when a feature, MVP, product idea, domain model, or repo context needs sharper language before to-prd, to-issues, triage, tdd, diagnose, or architecture review.
---

# Grill With Docs

Build shared understanding before durable work begins. This skill may inspect code and update context docs, but it must not implement code, create PRDs, create GitHub Issues, open PRs, or expand into planning unless the user explicitly asks afterward.

## Start

Read:

- `AGENTS.md` or `CLAUDE.md`
- `CONTEXT.md`
- `docs/agents/domain.md`
- relevant ADRs in `docs/adr/`
- relevant source files if the user's claim can be checked locally

If setup docs are missing, suggest `setup-agent-workflow`, then continue best-effort with available context.

## Session Rules

- Ask one clarifying question at a time and wait for the answer.
- For each question, include your recommended answer and why.
- If the answer can be discovered from docs or code, inspect those instead of asking.
- Challenge conflicts with existing `CONTEXT.md`, ADRs, or code.
- Replace fuzzy or overloaded terms with precise canonical terms.
- Use concrete scenarios and edge cases to test domain boundaries.
- Stop when implementation-blocking context is clear enough for the next workflow.

Good challenge:

```text
Your context says "Customer" is the account owner, but you seem to mean the logged-in person. Should this be "User" instead?
```

## Update CONTEXT.md Inline

When a project fact, domain term, source folder, or context pointer is resolved, update `CONTEXT.md` immediately using [CONTEXT-FORMAT.md](CONTEXT-FORMAT.md).

`CONTEXT.md` is a lightweight context map. It is not a PRD index, implementation plan, issue draft, scratch pad, or giant knowledge base.

Do not manually list every PRD. PRDs live in GitHub Issues.

## ADRs

Offer or create an ADR only when all three are true:

1. The decision is hard to reverse.
2. The decision would be surprising without context.
3. The decision came from a real tradeoff.

Use [ADR-FORMAT.md](ADR-FORMAT.md). Do not create ADRs for obvious choices or small implementation details.

## Handoff

When the grilling session is done, summarize:

- clarified domain terms and project facts
- docs updated
- ADRs created or proposed
- open questions that remain
- recommended next workflow, usually `to-prd`, `to-issues`, or `triage`

Do not continue into implementation in the same skill run.
