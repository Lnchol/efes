# Context

> Current working state and tribal knowledge for the next agent.

- **Stage:** Efes personalization layer complete (v0.6.0, see
  `CHANGELOG.md`) — identity established, licensed, 4-agent roster
  vendored for Claude Code + Codex. No concrete project has been forked
  from this yet.
- **Active constraints:** repo language is `{{REPO_LANGUAGE}}` (default
  English) for the skeleton itself; a forked project picks its own during
  its interview. License is proprietary (owner: Efe) — a fork should
  confirm whether to keep that or pick its own (`EFES.md` §2A).
- **Assets on hand:** the full governance skeleton (rules, docs, memory
  bank) + a vendored, generic 4-role agent roster (`.claude/agents/`,
  `.codex/agents/`) + general-manager model defaults
  (`.claude/settings.json`, `.codex/config.toml`).
- **Open questions:** identity, vision, stack, architecture, and roadmap are
  still `{{...}}` placeholders — deliberately deferred until a real project
  forks this repo. The 4 agent files' `{{...}}` project-orientation blocks
  are also still generic, for the same reason.
- **Hint for the next agent:** don't recreate the skeleton, the LICENSE, or
  the 4 agent files — they exist. When a real project starts, fork this
  repo, run the `EFES.md` interview, then **specialize** (don't recreate)
  the agent files with that project's real paths/commands, and fill the
  remaining placeholders.
