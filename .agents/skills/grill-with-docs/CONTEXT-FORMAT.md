# CONTEXT.md Format

`CONTEXT.md` is the project's single root glossary. It defines canonical domain language and the words agents should avoid.

Use this structure:

```markdown
# {Context Name}

One or two sentences describing what this context is and why this glossary exists.

## Language

**Canonical Term**:
One or two sentences defining what this term is.
_Avoid_: overloaded synonym, misleading synonym, rejected synonym
```

## Rules

- Be opinionated. When multiple words exist for the same concept, pick one canonical term and list the others under `_Avoid_:`.
- Keep definitions tight. One or two sentences max. Define what the term is, not what it does.
- Only include terms specific to this project's context.
- Do not include general programming concepts, implementation details, issue tracking rules, source folder maps, PRDs, plans, scratch notes, or ADR content.
- Group terms under subheadings when natural clusters emerge. If all terms belong to one cohesive area, a flat `## Language` section is fine.
- Use a single root `CONTEXT.md` for now. Do not create `CONTEXT-MAP.md`.
