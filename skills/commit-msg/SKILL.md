---
name: commit-msg
description: Format and validate a commit message against this project's chosen convention. Use only after the user has explicitly asked for a commit — never to decide whether to commit.
---

# Commit message

## When to use

Only once the user has explicitly asked for a commit — commit-on-demand,
never inferred.

## Steps

1. Confirm the ask was explicit for *this* commit — a past approval doesn't
   carry forward.
2. Check `docs/process/conventions.md` for the chosen commit convention
   (e.g. Conventional Commits) and branch naming.
3. Write the message: `type(scope): summary`, body explaining why not what,
   footer for breaking changes/issue refs.
4. Confirm the staged diff actually matches what the message claims — no
   secrets, no unrelated files swept in (`git status` after a broad `git add`).

## Notes

This skill formats the message once permission is already given — it is
never itself the permission to commit.
