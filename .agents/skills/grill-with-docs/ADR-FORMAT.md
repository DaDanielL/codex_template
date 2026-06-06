# ADR Format

ADRs live in `docs/adr/` and use sequential numbering:

```text
0001-short-slug.md
0002-short-slug.md
```

Scan `docs/adr/` for the highest existing number and increment by one.

## Template

```markdown
# Short title of the decision

One to three sentences explaining the context, what decision was made, why it was made, and what future agents should not re-litigate.
```

That is enough for most ADRs.

Optional sections are allowed only when they add real value:

- `Status`: `proposed`, `accepted`, `deprecated`, or `superseded`
- `Considered options`
- `Consequences`

## When To Create One

Create an ADR only when the decision is hard to reverse, surprising without context, and the result of a real tradeoff.

Good ADR candidates:

- architectural shape
- integration boundaries
- technology choices with meaningful lock-in
- product or workflow scope boundaries
- deliberate deviations from the obvious path
- constraints not visible in code
