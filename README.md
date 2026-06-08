# codex_template

Reusable AI-agent-layer template for Codex-driven projects.

This repository does not contain a demo app. It provides the `.agents/` workflow layer used to create product requirements, generate GitHub issue-ready vertical slices, prime context, plan implementation, implement safely, validate work, and review changes.

Start with [.agents/README.md](.agents/README.md).

For a downstream repo, run `setup-agent-workflow` first to create agent workflow config, a root glossary, and the canonical GitHub triage labels. Use `grill-with-docs` when terminology needs clarification, `to-prd` to publish a `[PRD]` GitHub Issue from current context, then `to-issues` to create approved child implementation issues.
