# Agent Triage Labels

Use these five canonical labels only for workflow state.

An issue should have exactly one canonical state label at a time.

| Label | Meaning |
|-------|---------|
| `needs-triage` | Issue exists but has not been clarified or classified yet. |
| `needs-info` | Missing facts, requirements, reproduction steps, or other blocking information. |
| `ready-for-agent` | Fully specified and safe for autonomous agent implementation. |
| `ready-for-human` | Needs human judgment, approval, review, manual testing, credentials, design decision, or merge. |
| `wontfix` | Intentionally rejected or no longer planned. |

## Default Rules

- New issue: `needs-triage`
- Approved child issue from a PRD: `ready-for-agent`
- Unclear issue: `needs-info`
- Human judgment or review required: `ready-for-human`
- Rejected issue: `wontfix`

## PRD Label Flow

- New `[PRD]` issue created by `to-prd`: `ready-for-agent`
- Missing or blocking requirements: `needs-info`
- Ready for issue slicing: `ready-for-agent`
- Human judgment or approval needed before slicing: `ready-for-human`

For a PRD, `ready-for-agent` means ready for `to-issues`, not direct code implementation.

Child issues from an approved PRD default to `ready-for-agent` unless that specific issue needs more information or human judgment.

## Needs Info Resumption

When a reporter answers a `needs-info` question, read prior triage notes, preserve what has been established, and do not re-ask resolved questions. Move the issue back to `needs-triage` or directly to the appropriate ready state once the missing information is resolved.

## Ready For Human

Whenever an issue or PR becomes `ready-for-human`, state the exact human action needed.

Good examples:

- Review PR #24.
- Confirm empty-state copy.
- Manually test login in Chrome.
- Decide between Approach A and Approach B.

Do not use vague handoffs like "needs review" without saying what the human should do.
