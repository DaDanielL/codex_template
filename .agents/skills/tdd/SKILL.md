---
name: tdd
description: Implement ready-for-agent issues with inline planning and red-green-refactor cycles. Use when a behavior-changing feature, refactor, docs, or chore issue is ready for autonomous implementation without separate prime or plan workflows.
---

# TDD

Use test-driven development as the default implementation path for behavior-changing `ready-for-agent` issues. This skill does its own lightweight planning inline; it does not require `prime` or `plan` first.

## Rules

- Start from a GitHub Issue and Agent Brief when available.
- Branch before code edits. If already on a suitable work branch, continue there.
- Do not enforce one issue, one branch, one PR inside this skill.
- Test observable behavior through public interfaces.
- Mock only system boundaries such as external APIs, time, randomness, filesystem, or sometimes databases.
- Do not mock internal collaborators, private methods, or modules you control.
- Work vertically: one failing behavior test, minimal code to pass, repeat.
- Do not write all tests first and then all implementation.
- Never refactor while RED. Refactor only after tests are GREEN.
- If automated TDD is impractical, explain why and use the closest verification method.

## Start

Read `AGENTS.md` or `CLAUDE.md`, `docs/agents/issue-tracker.md`, `docs/agents/triage-labels.md`, `docs/agents/domain.md`, `CONTEXT.md`, relevant ADRs in `docs/adr/`, and the current conversation context.

If the input names a GitHub issue, fetch it:

```bash
gh issue view {NUMBER} --json number,title,body,labels,state,url,comments
```

Check git state before code edits:

```bash
git branch --show-current
git status --short
```

If on the default branch, create a work branch before editing. If the tree contains unrelated changes, preserve them and ask only if they block the TDD work.

## Inline Planning

Before editing, inspect relevant source and test files with focused searches. Then form a compact TDD plan:

- **Public interface**: command, API, component, workflow, or behavior under test
- **Behavior list**: externally visible behaviors to prove
- **First tracer bullet**: the smallest behavior that proves the path end to end
- **Test command**: focused command for the first loop
- **Validation command**: broader command to run before handoff

Use the Agent Brief as prior approval. Ask a question only when the public interface, behavior priority, or acceptance criteria are unclear.

## Red-Green Loop

For the tracer bullet and each next behavior:

1. **RED**: Write one focused test for one behavior.
2. Run the focused test and confirm it fails for the expected reason.
3. **GREEN**: Implement only enough code to pass that test.
4. Run the focused test until it passes.
5. Add the next behavior test and repeat.

Good tests describe what the system does, not how it is built. A refactor should not break them unless behavior changed.

## Refactor

After the behavior tests are GREEN:

- Remove duplication.
- Simplify awkward interfaces.
- Move complexity behind smaller public surfaces where natural.
- Keep tests on public behavior.
- Run the focused tests after each refactor step.

If a refactor becomes risky or broad, stop and propose a follow-up issue instead of expanding scope.

## Validate

Run the focused test command, then the broader relevant checks from `AGENTS.md` or project scripts. Check acceptance criteria from the issue and Agent Brief.

If automated TDD was impractical, document:

- why the normal red-green loop could not be used
- the closest automated or manual verification performed
- any residual risk

## Report

Summarize:

- GitHub issue and branch
- behaviors tested
- red-green cycles completed
- files changed
- validation run
- known gaps or follow-up issues

Recommended next workflow: `validate`.
