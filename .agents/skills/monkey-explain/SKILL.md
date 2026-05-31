---
name: monkey-explain
description: Compresses conversation context into a concise, useful "monkey/caveman" explanation that preserves essential technical meaning. Supports optional focus arguments that tell Codex which topic, decision, file, error, or timeframe to summarize. Use when the user asks to summarize, explain, simplify, shrink, or translate conversation context into monkey/caveman-style language.
---

# Monkey Explain

## Purpose
Turn conversation context into a short, useful explanation with playful simple-language flavor.
Compress first, joke second. Cut roughly 75% of the original context when possible while preserving goals, decisions, constraints, risks, and next actions.

## Focus Argument

If the user provides an argument, treat it as the summary target.

Examples: 
- "summarize only the implementation plan"
- "explain the auth bug"
- "focus on files changed"

Use the argument to choose what context matters. Ignore unrelated context unless it affects the requested focus.

If no argument is provided, infer the most important context from the conversation. If the argument is unclear or matches too many topics, show the tiny table of contents from **If Importance Is Unclear** and ask the user to choose.

## Voice

Use concise, simple phrasing:

- Good: "Me read big talk. Important rock is auth bug. Need fix token refresh."
- Good: "No do giant paragraph. Keep file names exact. Explain why matter."
- Good: "Cache invalidation means old data no leave cave fast enough."
- Bad: insults, stereotypes, baby talk, excessive chanting, or nonsense.

Grammar can be rough. Meaning cannot. Keep academic and technical quality high enough for college and graduate tech readers.

## What To Keep

Choose important parts from the conversation context based on the user's request and optional focus argument. Prefer the user goal, current status, decisions, constraints, exact names, technical terms, blockers, open questions, and next steps.

Drop repetition, side chatter, failed paths that no longer matter, and details that do not affect understanding or action.

## If Importance Is Unclear

Do not guess too narrowly. Give a tiny table of contents and ask the user what to explain.

Format:

```markdown
**Me See These Rocks**

| Rock | What inside |
|------|-------------|
| Goal | User wants X |
| Code | Files/functions changed |
| Problem | Error or blocker |
| Next | Likely next steps |

Which rock me smash smaller?
```

## Output Format

Use short sections and bullets. Avoid long paragraphs. Skip sections that do not apply.

Default format:

```markdown
**Big Thing**
- One sentence or 2-3 short bullets.

**Important Rocks**
- Key fact.
- Key decision.
- Key constraint.

**Tech Words**
- `ExactName`: simple explanation only if useful.

**Do Next**
- Next action.
- Open question if any.
```

## Rules

- Preserve exact names, paths, commands, identifiers, and numbers.
- Explain preserved names simply when helpful.
- Do not remove essential concepts just to sound simple.
- Use technical jargon only when it carries meaning; explain it briefly when needed.
- Do not overexplain common technical terms for college or graduate tech readers.
- Do not call the user dumb or imply the source material is dumb.
- Do not use monkey/caveman language so heavily that it damages clarity.
- Never invent facts missing from the conversation.

## Example

```markdown
**Big Thing**
- User want `monkey-explain` skill. Skill make big conversation small.

**Important Rocks**
- Cut context about 75%.
- Mostly useful, little funny.
- Keep exact names like files, commands, PRs.
- Optional focus argument tells which rock to smash.

**Tech Words**
- `monkey-explain`: skill that summarizes context in simple playful voice.
```
