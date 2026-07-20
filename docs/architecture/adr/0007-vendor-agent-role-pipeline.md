# ADR-0007: Vendor a fixed 4-role agent delegation pipeline, general manager = top-level session

## Status

Accepted

## Context

The user has already validated a 4-role agent split on another project:
read-only recon (`code-explorer`), routine implementation
(`fast-task-executor`), hard/complex implementation
(`hard-task-specialist`), and test/validation reporting
(`validation-runner`, never edits code). That project also confirmed model
routing per role (haiku / sonnet / opus / sonnet) and the value of a
dedicated validation lane so verification isn't skipped or folded into the
same pass that wrote the change.

The user wants this same pattern available from the start of every future
project, in whichever CLI they're driving that day — they expect to switch
between Claude Code and Codex CLI on the same work. `EFES.md`'s own default
(inherited from before this decision) treats sub-agent definitions as
generated on demand, never pre-made, because a generic
"planner/builder/reviewer" split is too vague to vendor blindly. That
default doesn't fit here: the roster itself isn't in question — only the
project-specific details (paths, commands, complexity heuristics) are.

A fifth "orchestrator" agent that itself dispatches the other four was
considered and rejected: the top-level chat session already performs that
role today (deciding what to delegate and to which lane) via each tool's
native agent-spawning mechanism. Adding a wrapper agent around that adds a
hop with no confirmed benefit, and Codex CLI's own docs note it does not
auto-spawn custom subagents — delegation is explicit, from whichever session
is driving.

## Decision

- **Vendor 4 generic agent definitions**, specialized later per project
  (never recreated) by the `EFES.md` bootstrap interview:
  - `code-explorer` — read-only recon. Claude: haiku,
    `tools: Read, Glob, Grep, WebFetch, WebSearch`. Codex:
    `model_reasoning_effort = "low"`, `sandbox_mode = "read-only"`.
  - `fast-task-executor` — routine/boilerplate build lane. Claude: sonnet,
    full read-write toolset. Codex: `"medium"` effort, `"workspace-write"`.
  - `hard-task-specialist` — complex/architectural build lane. Claude: opus,
    full read-write toolset. Codex: `"high"` effort, `"workspace-write"`.
  - `validation-runner` — runs tests/validation, reports pass/fail, never
    edits. Claude: sonnet, `tools: Bash, PowerShell, Read, Glob, Grep` (no
    Edit/Write). Codex: `"low"` effort, `"read-only"`.
- **Both tool formats ship together**: `.claude/agents/*.md` (Claude Code
  frontmatter) and `.codex/agents/*.toml` (Codex CLI's verified subagent
  schema — `name`, `description`, `model_reasoning_effort`, `sandbox_mode`,
  `developer_instructions`), so switching CLIs mid-project doesn't mean
  losing the roster. Codex has no per-tool allowlist equivalent to Claude
  Code's explicit `tools:` list — `sandbox_mode` (`read-only` vs
  `workspace-write`) is the closest available control.
- **No 5th orchestrator agent.** The top-level session is the general
  manager, defaulted to the most capable available model since it's the one
  deciding delegation: Claude Code via `.claude/settings.json`
  (`claude-fable-5`); Codex via `.codex/config.toml` (left as a
  `{{CODEX_FLAGSHIP_MODEL}}` placeholder — the exact current flagship id
  wasn't guessed, since it depends on the account/CLI version).
  `AGENTS.md` §10 documents the roster and this convention.
- **`EFES.md` changed accordingly**: §0.1 Mode B lists the agent files as
  already vendored (don't recreate), §2F's multi-agent bullet no longer asks
  *whether* to create sub-agents — only what's needed to specialize the
  fixed four — and §6's end-of-bootstrap ritual adds a check that the
  `{{...}}` orientation blocks actually got filled before Phase 0 is marked
  done.
- **Gemini CLI gets no subagent parity** — only requested for Claude Code
  and Codex, and no equivalent mechanism was verified to exist for Gemini;
  not invented speculatively.

## Consequences

- Every project forked from this skeleton starts with a working, familiar
  delegation pattern in both CLIs the user actually switches between,
  instead of re-designing an agent split per project.
- The agents are inert until specialized — a fork that skips the
  specialization step (§0.1/§6) has 4 generic agents that don't know the
  project's real test commands or key paths. The new end-of-bootstrap check
  exists specifically to catch that.
- Vendoring a fixed roster is a bet that "explore → fast/hard build →
  validate" fits most future projects. If a project's shape doesn't fit
  (e.g. no meaningful fast/hard split, or a fifth role turns out to be
  needed), that's a per-project deviation to record in that project's own
  `docs/memory/decisions.md` — this ADR doesn't forbid it, it just sets the
  default.
- Codex's `sandbox_mode` is coarser than Claude Code's explicit tool lists
  (no per-tool allowlist) — the two formats are equivalent in intent, not
  byte-for-byte in capability.
