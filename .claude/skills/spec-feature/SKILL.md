---
name: spec-feature
description: Scaffold a new feature spec before writing code. Use whenever starting behavior-changing work in the spec lane, or retroactively in the vibe lane once the work becomes load-bearing — enforces "spec before code."
---

# Spec a feature

## When to use

Before any new behavior-changing work starts, in the spec lane. In the vibe
lane, retroactively, the moment the change stops being throwaway.

## Steps

1. Copy `docs/features/_template.md` to `docs/features/<short-name>.md`.
2. Fill Status, Problem, Scope, Input contract (if applicable), Flow,
   Acceptance criteria, Out-of-scope.
3. In the spec lane: write the spec — and its first failing test, see
   `write-tests` — before any implementation code.
4. Link the spec from the relevant ADR or memory-bank entry if the decision
   it embodies isn't obvious from the filename.

## Notes

A spec that's just a write-up of the code's behavior after the fact isn't a
spec, it's documentation. Keep acceptance criteria testable, not aspirational.
