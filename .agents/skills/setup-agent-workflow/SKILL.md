---
name: setup-agent-workflow
description: Set up the repository-level agent workflow context for GitHub-Issue-driven agentic engineering. Use before first use of grill-with-docs, to-prd, to-issues, triage, tdd, diagnose, verify, improve-codebase-architecture, zoom-out, or parallel-ready.
---

# Setup Agent Workflow

Scaffold the lightweight repo workflow configuration that the engineering skills consume. This setup is GitHub-only, optimized for a solo developer, and keeps workflow behavior inside skills rather than in a large repo doc.

## Creates

- `AGENTS.md` or `CLAUDE.md` with an `## Agent skills` block
- root `CONTEXT.md` glossary when missing
- `docs/agents/issue-tracker.md`, `docs/agents/triage-labels.md`, `docs/agents/domain.md`
- `docs/adr/`
- GitHub labels: `needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`

## Non-Goals

Do not create `.scratch/`, `docs/prd/`, `CONTEXT-MAP.md`, `docs/agents/workflow.md`, `.github/ISSUE_TEMPLATE/`, local duplicate issue drafts, or custom priority/type/area labels.

## Phase 1: Explore

Inspect the repo before editing:

```bash
git status --short
git remote -v
gh --version
gh auth status
gh repo view --json nameWithOwner,defaultBranchRef
```

Read whatever exists: `AGENTS.md`, `CLAUDE.md`, `CONTEXT.md`, `docs/agents/`, and `docs/adr/`.

If the repo is not a git repo, has no GitHub remote, `gh` is missing, or `gh` is not authenticated, stop and tell the user exactly what to run. Do not say setup is complete.

## Phase 2: Choose The Agent Instruction File

- If `CLAUDE.md` exists and `AGENTS.md` does not, update `CLAUDE.md`.
- If `AGENTS.md` exists and `CLAUDE.md` does not, update `AGENTS.md`.
- If both exist, ask which one is the primary agent instruction file.
- If neither exists, create `AGENTS.md` by default.

When an `## Agent skills` block already exists, update it in place instead of appending a duplicate. Preserve unrelated user edits.

## Phase 3: Write Repo Configuration

Add or update this block in the selected instruction file:

```markdown
## Agent skills

### Issue tracker
GitHub Issues are the source of truth for PRDs, implementation issues, bugs, refactors, docs, and chores. See `docs/agents/issue-tracker.md`.

### Triage labels
Use the five canonical labels: `needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, and `wontfix`. See `docs/agents/triage-labels.md`.

### Domain docs
Use one root `CONTEXT.md` as the project glossary, plus lightweight ADRs in `docs/adr/` for meaningful decisions. See `docs/agents/domain.md`.
```

Create missing docs from this skill's seed files:

- [issue-tracker-github.md](issue-tracker-github.md) -> `docs/agents/issue-tracker.md`
- [triage-labels.md](triage-labels.md) -> `docs/agents/triage-labels.md`
- [domain.md](domain.md) -> `docs/agents/domain.md`
- [context-template.md](context-template.md) -> root `CONTEXT.md`

Create `docs/adr/`, but do not add `.gitkeep` or a heavy ADR template. This template supports a single root `CONTEXT.md`; do not create `CONTEXT-MAP.md`.

## Phase 4: Ensure GitHub Labels

Use `gh label list` to inspect existing labels. Create any missing canonical labels with default GitHub styling:

```bash
gh label create needs-triage
gh label create needs-info
gh label create ready-for-agent
gh label create ready-for-human
gh label create wontfix
```

Do not create custom colors or extra labels.

## Phase 5: Report

Summarize the instruction file changed, agent docs and glossary created or updated, labels created or already present, and any blockers. Say the repo is ready for `grill-with-docs`, `to-prd`, `to-issues`, and `triage` only if all setup checks passed.
