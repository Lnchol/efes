---
name: provider-audit
description: Check that external vendors/APIs sit behind an interface or adapter instead of being called directly from domain code. Use before merging a change that adds or touches a third-party integration, or periodically to catch drift.
---

# Provider independence audit

## When to use

Before merging any change that adds or touches a third-party
integration/SDK/API — or periodically, to catch drift the first review missed.

## Steps

1. Grep for direct SDK/client imports and API calls outside this project's
   adapter boundary (naming varies by stack — check `docs/architecture/stack.md`).
2. For each hit, confirm it sits behind an interface that's swappable
   without touching callers.
3. Flag hardcoded credentials, base URLs, or vendor-specific error shapes
   leaking into domain code.
4. If a violation is found: move it behind an adapter now, or record it as
   an accepted exception in `docs/memory/decisions.md` — never leave it
   silently unrecorded.

## Notes

Provider independence is a golden rule (`AGENTS.md` §3 NEVER list), not a
suggestion. One unrecorded exception becomes the pattern the next change copies.
