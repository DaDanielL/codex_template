# Agent Brief

An Agent Brief is the durable comment posted when a GitHub Issue becomes `ready-for-agent`. The issue body and comments are context; the brief is the contract for the AFK agent.

## Principles

- Write behavioral requirements, not step-by-step implementation instructions.
- Avoid fragile file paths and line numbers.
- Name stable interfaces, commands, config shapes, domain terms, or expected behavior when useful.
- Include concrete, externally verifiable acceptance criteria.
- State dependencies and out-of-scope boundaries.

## Template

```markdown
## Agent Brief

**Category:** bug / enhancement / refactor / docs / chore

**Summary:** One-line description of what needs to happen.

**Current behavior:** Describe the current behavior or status quo.

**Desired behavior:** Describe the expected behavior after the work is complete, including important edge cases.

**Key interfaces:** 
- Interface, command, API, config shape, domain term, or behavior to inspect

**Acceptance criteria:**
- [ ] Specific, testable criterion 1
- [ ] Specific, testable criterion 2
- [ ] Specific, testable criterion 3

**Dependencies:**
- None

**Out of scope:**
- Related behavior that should not be changed in this issue
```

## Bad Brief Smell

If the brief says only "fix this", points at a line number, lacks acceptance criteria, or omits scope boundaries, the issue is not ready for autonomous agent work.
