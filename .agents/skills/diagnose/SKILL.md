---
name: diagnose
description: Diagnose hard bugs and performance regressions through a disciplined feedback-loop-first workflow. Use when a GitHub issue reports broken behavior, failing output, flaky behavior, or a performance regression that needs investigation before or during implementation.
---

# Diagnose

Use this skill when the problem is not yet understood. The goal is to build a reliable signal, prove the real cause, fix only after evidence supports the fix, and leave durable notes for the issue and future agents.

## Rules

- Start from a GitHub Issue and Agent Brief when available.
- Prefer a fast, deterministic, agent-runnable feedback loop before reading deeply or changing code.
- Do not hypothesize without a loop unless you explicitly cannot build one and have documented what is missing.
- Confirm the loop reproduces the user's failure, not a nearby failure.
- Rank 3-5 falsifiable hypotheses before testing them.
- Change one variable at a time while instrumenting.
- Tag temporary debug logs with a unique prefix such as `[DEBUG-a4f2]` and remove them before handoff.
- For performance regressions, establish a baseline measurement before changing code.
- Write a regression test before the fix when a correct public seam exists.
- If no correct test seam exists, document that as an architecture finding instead of creating a shallow false-confidence test.

## Start

Read `AGENTS.md` or `CLAUDE.md`, `docs/agents/issue-tracker.md`, `docs/agents/triage-labels.md`, `docs/agents/domain.md`, `CONTEXT.md`, relevant ADRs in `docs/adr/`, and the current conversation context.

If the input names a GitHub issue, fetch it:

```bash
gh issue view {NUMBER} --json number,title,body,labels,state,url,author,comments
```

Check git state before code edits:

```bash
git branch --show-current
git status --short
```

If the issue lacks observed behavior, expected behavior, access to the failing path, or enough artifacts to construct a feedback loop, ask for the missing artifact or recommend `needs-info` / `ready-for-human`.

## Build The Feedback Loop

Spend most of the early effort here. Try these options in roughly this order:

1. Failing test at the seam that reaches the bug.
2. CLI command with fixture input and expected output.
3. HTTP request or script against a running service.
4. Headless browser check that asserts DOM, console, network, or visual state.
5. Replay of a captured request, payload, trace, log, or event.
6. Throwaway harness around the smallest executable slice of the failing path.
7. Property, fuzz, stress, or repeated loop for intermittent failures.
8. Differential loop against an older version, alternate config, or known-good output.

Iterate on the loop until it is fast enough, sharp enough, and deterministic enough to guide the fix. For nondeterministic bugs, raise the reproduction rate with repetition, stress, timing control, or narrowed inputs until the failure is debuggable.

If no useful loop can be built, stop. List what you tried and ask for access, logs, traces, a recording with timestamps, or permission to add temporary instrumentation.

## Reproduce

Run the loop and capture the exact symptom, whether it matches the user's report, how often it reproduces, and the command, script, request, or test that proves it. Do not proceed to a fix until the original problem reproduces or you have explicitly documented why it cannot be reproduced.

## Hypothesize

Create 3-5 ranked hypotheses before testing. Each hypothesis must include a falsifiable prediction: `If {cause} is true, then {probe} will make {observable change}.`

Share the ranked list when the user is present. If the user is unavailable, proceed with the ranking and preserve it in notes.

## Instrument

Probe one prediction at a time. Prefer debugger or REPL inspection, targeted logs at boundaries that distinguish hypotheses, and minimal temporary harness changes.

Never scatter broad logs and search the noise afterward. For performance work, establish a comparable baseline before changing code.

## Fix And Regression Test

When the cause is proven:

1. Minimize the repro to the smallest real failure path.
2. Turn that repro into a failing regression test at the correct public seam when one exists.
3. Apply the smallest fix that addresses the proven cause.
4. Watch the regression test pass.
5. Re-run the original feedback loop against the unminimized scenario.

If the fix becomes broader than the issue allows, stop and recommend splitting follow-up work rather than expanding scope silently.

## Cleanup And Report

Before reporting done, re-run the original feedback loop, run the regression test or document why no correct seam exists, remove all `[DEBUG-...]` instrumentation, delete throwaway harnesses or move them to an explicitly named debug location if the user approves keeping them, and update the GitHub issue or handoff notes with root cause, reproduction command, fix summary, validation run, and remaining risk.

End by recommending `validate`. If the investigation found missing seams, tangled callers, or hidden coupling, recommend an architecture follow-up after the bug fix is complete.
