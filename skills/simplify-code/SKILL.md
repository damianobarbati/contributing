---
name: simplify-code
description: "Simplify code for clarity while preserving behavior. Use for dense control flow, unclear names, redundant wrappers, or local complexity in working code; exclude unrelated architectural rewrites."
---

# simplify-code

## Goal

Make code easier to understand, modify, and debug without changing behavior.

## Scope

- Default to requested or recently modified code. Broaden only when authorized.
- Leave already clear code and soon-to-be-replaced modules alone.
- Understand callers, edge cases, and performance constraints before simplifying.

## Workflow

1. Read project conventions and neighboring code. Record existing edits and inspect tests, callers, side effects, and historical rationale where unclear.
2. Identify concrete obstacles to comprehension:

| Pattern | Candidate change |
| --- | --- |
| Deep nesting | Guard clauses or a named helper |
| Multiple responsibilities | Focused functions with meaningful names |
| Dense ternary chains | Explicit branches or a readable lookup |
| Repeated conditions | Shared predicate when meaning is identical |
| Misleading names | Names describing actual responsibility and mutation |
| Repeated logic | Shared implementation when contracts match |
| Wrapper without a useful role | Direct call after checking error and timing semantics |
| Redundant assertion or comment | Remove only if no type or intent information is lost |

3. Treat line counts and repetition as screening signals, not proof. Check why an abstraction exists before removing it.
4. Apply small, reviewable changes. Keep behavior changes distinguishable from simplification; avoid unrelated edits.
5. Run affected checks and compare the complete result for clarity, project consistency, and preserved behavior.

## Rules

- Preserve inputs, outputs, errors, side effects and their order, public contracts, and meaningful performance characteristics.
- Preserve comments explaining why. Prefer explicit control flow over fewer lines when comprehension improves.
- Do not replace named concepts with dense inline expressions or combine unrelated responsibilities.
- Verify omission, `undefined`, `null`, truthiness, evaluation order, and side effects before shortening expressions.
- Removing `async` or `return await` can change rejection timing and stack traces; inspect observable contracts first.
- Do not add a new state library or shared primitive just to reduce local repetition.
- Confirm dead code against exports, discovery, configuration, and side effects before deleting it.
- Use automation for large mechanical transformations when it improves reliability; do not force arbitrary PR or commit splits.
- Do not weaken tests, remove error handling, or commit or publish without authorization.

```typescript
// Preserve branch priority with explicit control flow.
function getStatusLabel(item: Item): string {
  if (item.isNew) return "New";
  if (item.isUpdated) return "Updated";
  if (item.isArchived) return "Archived";
  return "Active";
}
```

## Verification

- Run relevant existing tests, build, and lint checks in proportion to the change.
- Confirm tests need no changed expectations to accept altered behavior.
- Inspect the diff for unrelated edits, weakened errors, dead imports, and project-style drift.
- Reconsider changes that are harder to understand than the original; report unavailable checks.

## Output

Return the simplifications, why they improve comprehension, check results, and remaining uncertainty. Report unsupported opportunities as recommendations rather than applying speculative rewrites.
