---
name: triage
description: Classify GitHub Issues through the repository's five canonical workflow states and prepare ready-for-agent work with durable Agent Briefs. Use when reviewing incoming issues, moving issues between triage labels, preparing issues for AFK agent work, or finding issues needing human attention.
---

# Triage

Move GitHub Issues through the repo's small state machine. Triage classifies readiness; it does not implement code, create branches, open PRs, merge PRs, or close PRD issues.

## Rules

- Use GitHub Issues only.
- Use exactly one canonical state label per issue: `needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, or `wontfix`.
- Do not create extra category labels such as `bug` or `enhancement`; capture category in triage notes or Agent Briefs.
- Do not require an AI disclaimer on every triage comment.
- Do not create `.out-of-scope/` files yet.
- When an issue becomes `ready-for-agent`, post an Agent Brief using [AGENT-BRIEF.md](AGENT-BRIEF.md).
- When an issue becomes `ready-for-human`, state the exact human action needed.
- Ask one clarifying question at a time when an issue is unclear.

## Start

Read `AGENTS.md` or `CLAUDE.md`, `docs/agents/issue-tracker.md`, `docs/agents/triage-labels.md`, `docs/agents/domain.md`, `CONTEXT.md`, relevant ADRs in `docs/adr/`, and the current conversation context.

Verify GitHub is usable:

```bash
gh auth status
gh repo view --json nameWithOwner,defaultBranchRef
gh label list
```

If setup docs, GitHub auth, or canonical labels are missing, stop and say exactly what is missing. Suggest `setup-agent-workflow`.

## Show Needs Attention

When the user asks what needs attention, query and summarize:

```bash
gh issue list --state open --limit 100 --json number,title,labels,updatedAt,createdAt,url
```

Show three buckets, oldest first:

- Unlabeled issues
- Issues labeled `needs-triage`
- Issues labeled `needs-info` with new reporter activity since the last triage notes

Show counts and one-line summaries. Let the user choose what to triage.

## Triage One Issue

Fetch the full issue:

```bash
gh issue view {NUMBER} --json number,title,body,labels,state,url,author,createdAt,updatedAt,comments
```

Then:

1. Gather context from the issue body, comments, prior triage notes, glossary, ADRs, and relevant code if needed.
2. If conflicting canonical state labels are present, stop and ask which state should remain.
3. Recommend one state label with reasoning.
4. For bugs or performance regressions, attempt reproduction before recommending `ready-for-agent`.
5. If information is missing, ask one concrete question and recommend `needs-info`.
6. If the issue needs human judgment, approval, credentials, manual testing, merge, or design choice, recommend `ready-for-human` and state the exact action.
7. If the issue is fully specified, recommend `ready-for-agent` and draft an Agent Brief.
8. Wait for user approval before editing labels or posting comments.

## Resume Needs Info

If prior triage notes exist, read them first. Check whether new comments answer the outstanding questions, preserve what is established, and do not re-ask resolved questions. If the issue is still unclear, update the triage notes with one next question.

Use this comment shape for `needs-info`:

```markdown
## Triage Notes

**Established so far:**
- ...

**Still needed:**
- ...
```

## Quick Override

If the user explicitly says to move an issue to a state, trust the maintainer. Confirm the exact label change, comment, and close behavior first, then apply it without a full grilling session. If moving to `ready-for-agent`, include the Agent Brief in the confirmed action.

## Apply Outcome

Use `gh issue edit` to replace the old canonical state label with the new one:

```bash
gh issue edit {NUMBER} --remove-label "{old-state}" --add-label "{new-state}"
```

Omit `--remove-label` when the issue has no canonical state label yet.
Post a concise comment when the state change needs durable context. For `ready-for-agent`, post the Agent Brief. For `ready-for-human`, include the exact human action needed. For `wontfix`, explain the reason and close only after user approval.
