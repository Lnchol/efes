---
name: module-boundary-check
description: Check that domains don't import each other directly and that shared contracts live in one place. Use before merging a change that touches more than one domain/module, or periodically to catch boundary drift.
---

# Module boundary check

## When to use

Before merging a change that touches more than one domain/module — or
periodically, once the project has enough structure for boundaries to exist.

## Steps

1. Identify this project's domain/module boundaries (`docs/architecture/overview.md`,
   `AGENTS.md` §5 repo map).
2. Grep for cross-domain imports that bypass the shared-contracts location.
3. For each hit, either route it through the shared contract or flag it as
   a boundary break to fix.
4. If boundaries were never defined yet (small/early project), skip — there's
   nothing to check.

## Notes

Complements `provider-audit`: that rule is about external vendors, this one
about internal domains. Both come from the same "small, single-responsibility,
no spaghetti" golden rule.
