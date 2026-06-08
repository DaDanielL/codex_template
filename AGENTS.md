# AGENTS.md

This repository is a reusable AI-agent-layer template for Codex. It contains workflow definitions and documentation only.

## Project Overview

The template helps Codex-driven projects move from idea to reviewed implementation through PRDs, GitHub issue-ready vertical slices, context priming, implementation plans, validation, and review workflows.

Do not create a demo app, product scaffold, or framework-specific sample inside this repository.

## Tech Stack

No application runtime is required. The repository is Markdown workflow content.

| Area | Tooling |
|------|---------|
| Workflow docs | Markdown files in `.agents/skills/` |
| Issue tracking | GitHub Issues via `gh` |
| Pull requests | GitHub CLI via `gh pr create` and `gh pr view` |

## Commands

```bash
# List template files
rg --files

# Check workflow command coverage
rg -n "AGENTS.md|GitHub Issue|gh issue view|gh issue create|gh issue comment|gh issue edit|gh pr create|gh pr view|to-issues|triage|.agents/PRDs|.agents/stories|.agents/plans" .agents README.md AGENTS.md
```

## Architecture

```text
.
|-- AGENTS.md                 # Rules for this template repository
|-- README.md                 # Root overview
`-- .agents/
    |-- README.md             # AI-layer workflow guide
    |-- AGENTS-template.md    # Template for downstream project rules
    |-- PRDs/                 # Legacy local PRDs
    |-- stories/              # Legacy local story manifests
    |-- plans/                # Generated implementation plans
    |-- reports/              # Generated implementation reports
    |-- reviews/              # Generated review reports
    `-- skills/               # Workflow definitions
```

## Workflow Order

1. `setup-agent-workflow`
2. `grill-with-docs`
3. `to-prd`
4. `to-issues`
5. `triage`
6. `rules-interactive` or `create-rules`
7. `prd-interactive` or `create-prd`
8. `prime`
9. `plan`
10. `implement`
11. `validate`
12. `review` / `security-review`

## Editing Rules

- Use `AGENTS.md` as the project rules file.
- Use `[PRD]` GitHub Issues for the default PRD workflow.
- Store local PRDs in `.agents/PRDs/` only for legacy/local PRD workflows.
- Store story manifests in `.agents/stories/` only for legacy/local story workflows.
- Store implementation plans in `.agents/plans/`.
- Keep workflows app-neutral unless a workflow explicitly discovers project-specific context.
- Use GitHub Issues instead of external issue trackers.
- Use `to-issues` after `to-prd` so `[PRD]` issues become approved vertical-slice child issues before implementation.
- Use `triage` to move issues through the five canonical issue states before implementation.
- Prefer `gh issue view`, `gh issue create`, `gh issue comment`, `gh issue edit`, `gh pr create`, and `gh pr view` where useful.
- Do not introduce framework-specific demo code.

## Key Files

| File | Purpose |
|------|---------|
| `.agents/README.md` | Explains the AI layer and every workflow |
| `.agents/AGENTS-template.md` | Base for generated downstream `AGENTS.md` files |
| `.agents/skills/setup-agent-workflow/SKILL.md` | Sets up downstream agent workflow config, root glossary, and canonical GitHub triage labels |
| `.agents/skills/grill-with-docs/SKILL.md` | Clarifies domain language and updates the `CONTEXT.md` glossary or lightweight ADRs |
| `.agents/skills/to-prd/SKILL.md` | Publishes current context as a `[PRD]` GitHub Issue labeled `ready-for-agent` |
| `.agents/skills/to-issues/SKILL.md` | Breaks a `[PRD]` issue into approved vertical-slice GitHub implementation issues |
| `.agents/skills/triage/SKILL.md` | Classifies GitHub Issues and prepares Agent Briefs for `ready-for-agent` work |
| `.agents/skills/triage/AGENT-BRIEF.md` | Template for durable `ready-for-agent` issue comments |
| `.agents/skills/rules-interactive/SKILL.md` | Greenfield interview workflow for generating `AGENTS.md` |
| `.agents/skills/create-rules/SKILL.md` | Existing-codebase workflow for generating `AGENTS.md` |
| `.agents/skills/create-stories/SKILL.md` | Legacy local story manifest workflow |
