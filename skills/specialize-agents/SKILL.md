---
name: specialize-agents
description: Fill or refresh the 4 vendored agent files' project-orientation blocks (.claude/agents/*.md, .codex/agents/*.toml) with this project's real paths, commands, and complexity heuristic. Use once at bootstrap, and again whenever the project has changed enough that the agents' orientation has gone stale.
---

# Specialize the agent roster

## When to use

Once during the `EFES.md` bootstrap interview, and again whenever the
project's structure drifts enough that `code-explorer`, `fast-task-executor`,
`hard-task-specialist`, or `validation-runner` are working off stale
assumptions (new stack layer, renamed entry points, changed test commands).

## Steps

1. Read the current `## Project orientation` block in each of the 4 files
   (`{{...}}` placeholder or a previous fill).
2. Gather what changed: key entry points, the real
   test/lint/typecheck/build commands, a concrete example of "fast" vs
   "hard" work for this project.
3. Update all 4 files in **both** `.claude/agents/` and `.codex/agents/`
   together — they must stay in sync; one CLI's roster shouldn't know
   things the other's doesn't.
4. Note the refresh in `docs/memory/progress.md` if it's a meaningful
   update, not for trivial wording tweaks.

## Notes

A generic orientation block left unfilled is an unfinished bootstrap
(`EFES.md` §6 checks for this). This skill is what makes finishing it — or
re-finishing it later — a repeatable ritual instead of relying on memory.
