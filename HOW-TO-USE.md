# How to use Efes

## Starting a new project

1. Copy this repo (fork/clone/copy the folder) into your new project's location.
2. In your coding agent of choice, say `Follow EFES.md`.
3. Answer the discovery interview (§2 in `EFES.md`) — every question has a
   default; "defaults are fine" is a valid answer to any of them.
4. Confirm the summary. The agent fills every `{{...}}` placeholder, writes
   the project-specific docs, opens an ADR per locked decision, and
   **specializes** (not recreates) the 4 agent files with your project's
   real paths and test commands.
5. `EFES.md` deletes itself once done — from here on every session just
   reads `AGENTS.md` + the memory bank.

## Day to day, once a project exists

- You drive the **general manager** — whichever top-level session you're
  chatting in (Claude Code or Codex CLI). It decides what to delegate and
  to which of the 4 agents; you don't usually need to name one yourself,
  though you can ("use code-explorer to find X" / Codex's explicit
  delegation prompt).
- **Switching CLIs mid-project is expected.** Both read `AGENTS.md` (Claude
  Code via `CLAUDE.md`, Codex natively) and both have the same 4 roles
  (`.claude/agents/` and `.codex/agents/` stay in sync) — the memory bank
  (`docs/memory/`) is what actually carries context across the switch, not
  either tool's own state.
- **Each session starts by reading** `AGENTS.md`, then
  `docs/memory/context.md` → `progress.md` → `decisions.md` (§2 in
  `AGENTS.md`), and **ends by updating `progress.md`** — that trail is what
  makes picking up cold, days later or in the other CLI, actually work.
- The general-manager model defaults (`.claude/settings.json` / Fable 5,
  `.codex/config.toml` / flagship placeholder) are project-level, not
  per-session — change them there if a project needs a different default.
- Nothing auto-commits. Ask for it explicitly when you want it.

## Using the skills

Skills live in `skills/` and are symlinked into `.claude/skills/` so Claude
Code discovers them natively; Codex/Gemini read them on request. Ask for one
by what it does ("spec this feature", "audit provider independence") rather
than by exact name — the agent matches on the skill's description.

| Skill | Use it when |
|---|---|
| `wrap-session` | Ending any work session |
| `write-adr` | Locking an architecture/tech decision |
| `review-own-diff` | A change is "done" and needs a self-check before it counts |
| `clean-code` | Writing or refactoring any code |
| `write-tests` | Adding or changing behavior |
| `ponytail` | Always on — keeps solutions minimal |
| `caveman` | Always on — keeps chat output terse |
| `spec-feature` | Starting new behavior-changing work |
| `provider-audit` | Touching a third-party integration |
| `module-boundary-check` | A change crosses more than one domain/module |
| `commit-msg` | You've explicitly asked for a commit |
| `specialize-agents` | The 4 agent files' project orientation has gone stale |

## Adding a new skill

1. Copy `skills/_template/SKILL.md` to `skills/<name>/SKILL.md`, fill it in.
2. Symlink it into Claude Code's discovery path:
   `ln -s ../../skills/<name> .claude/skills/<name>`
   (on Windows without symlink privileges, this silently falls back to a
   junction/copy — still works, just keep both copies in sync by hand if
   you ever edit through `.claude/skills/` directly instead of `skills/`).
3. Note non-trivial additions in `docs/memory/decisions.md`.

## Troubleshooting

- **A new `.claude/agents/*.md` file isn't showing up as available:** restart
  the session — custom agents register at session start.
- **`gh` push rejected for `.github/workflows/ci.yml`** ("refusing to allow
  an OAuth App to create or update workflow... without `workflow` scope"):
  run `gh auth refresh -h github.com -s workflow`, then push again.
- **A file you didn't create shows up in `git status`:** check it isn't
  another tool/session's artifact sharing this working directory before
  staging it.
