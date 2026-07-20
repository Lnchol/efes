# Efes

**A personal, reusable bootstrap protocol that turns an empty repository into an agent-first, sustainable project foundation.**

Efes is a personal, reusable bootstrap protocol, pre-loaded with this user's own defaults. It is two things:

1. **A protocol** ([`EFES.md`](./EFES.md)) — point your coding agent at it and it **interviews you** about the project you want, then fills in a complete governance foundation tailored to your answers.
2. **A ready-made skeleton** — the project-agnostic parts that every project needs regardless of the answers (`AGENTS.md`, the `docs/` tree, the memory bank, ADR-0001, a vendored 4-agent delegation roster) already ship in this repo as templates. **Fork it and you start with the structure already in place.**

You never have to re-explain your project's structure again. Every future session just reads `AGENTS.md` and the memory bank, and continues from where the last one left off.

---

## Why does this exist?

Building software with AI agents (and sharing it with human teammates) breaks down when context lives only in someone's head — or in a chat that scrolls away. Efes solves this by establishing a durable, on-disk **single source of truth** the first time you start a project, designed for the reality that:

> _"Today an AI works on this, tomorrow a human, next week another team."_

Instead of re-describing your stack, conventions, and decisions every session, you bootstrap once and let the structure carry the context forward.

## What it produces

After the interview, the agent scaffolds a governance skeleton like this:

```
README.txt                  # NFO-style entry point → AGENTS.md
AGENTS.md                   # SINGLE SOURCE OF TRUTH (rules, stack, repo map)
LICENSE                     # this project's own license + owner
CLAUDE.md  GEMINI.md        # thin per-tool wrappers → point to AGENTS.md (Codex reads AGENTS.md directly)
.claude/agents/  .codex/agents/   # 4-role delegation roster (explore/fast/hard/validate)
docs/
  product/                  # vision + living, phase-based roadmap
  architecture/             # overview, locked stack, ADRs (one per decision)
  design/                   # design system (only if there's a UI)
  process/                  # workflow, conventions, definition-of-done, session protocol
  features/                 # spec-before-code template
  memory/                   # progress · context · decisions (the AI writes these every session)
skills/                     # portable, tool-agnostic SKILL.md capabilities
.github/                    # templated quality-gate CI + PR template
```

> The **code** scaffold (apps, packages, build tooling) is a later phase. Efes's job is the **governance foundation** that every subsequent session reads first.

## Two ways to start

**Mode A — fresh repo:** drop `EFES.md` into an empty repo and the agent generates the whole governance tree from scratch.

**Mode B — copy this repo (recommended):** the skeleton is already here, so you skip straight to filling it in. `efes` is a GitHub template repo — one command gets you a clean copy with no shared history:

```bash
gh repo create my-project --template Lnchol/efes --private --clone && cd my-project
```

No `gh` CLI? Use the **"Use this template"** button on the
[efes repo page](https://github.com/Lnchol/efes) instead.

Then, in your coding agent of choice:

> Follow `EFES.md`.

The agent detects that the skeleton already exists and:

1. **Runs the discovery interview** — focused, grouped questions about identity, product vision, tech stack, architecture constraints, design, process/tooling, and roadmap. Every choice has a sensible default; any group that doesn't apply is skipped.
2. **Confirms** — summarizes your decisions as a compact spec and waits for an explicit "yes".
3. **Fills the skeleton in place** — replaces every `{{...}}` placeholder and `<!-- EFES:FILL -->` block, writes the project-specific docs (vision, stack, roadmap phases), opens one ADR per locked decision, **specializes** (never recreates) the 4 vendored agent files, and updates the memory bank.

The protocol is **fully project-agnostic**: it encodes _how_ a sustainable project is set up, not _what_ any specific project is. No stack, vendor, or domain assumptions are baked in — every concrete choice comes from your interview.

## How to use this

See [`HOW-TO-USE.md`](./HOW-TO-USE.md) — starting a new project, day-to-day
usage once one exists, using/adding skills, and troubleshooting.

## Core principles

Efes bakes these non-negotiable standards into every project it bootstraps:

- **Single source of truth + thin wrappers** — one canonical `AGENTS.md`; every other tool file just points to it.
- **Language policy** — the repo is written in one chosen language; the conversation can be any language.
- **Memory bank + session protocol** — read memory at the start of a session, update it at the end. The trail you leave is the next agent's starting point.
- **Spec before code** — every feature starts from a spec file.
- **ADR for every decision** — architecture and tech choices are traceable and reversible-by-supersession, never silent.
- **Provider independence** — external vendors sit behind adapters; nothing is hardcoded to one vendor.
- **Module boundaries** — domains don't import each other; shared contracts live in one place.
- **Definition of Done is a gate** — lint, typecheck, tests, format, docs, and a memory update every time.
- **Fixed 4-agent delegation roster** — explore → fast/hard build → validate, vendored for Claude Code and Codex CLI, specialized (not recreated) per project.
- **Commit only when asked** — never auto-commit.

## What's in the box

Everything below ships pre-built as templates, so a fork starts with the
structure already in place:

```
EFES.md                     # the bootstrap protocol (interviews you, fills the skeleton)
AGENTS.md                   # SINGLE SOURCE OF TRUTH (rules, stack, repo map)
LICENSE                     # proprietary, owner: Efe (rewrite per-project if it differs)
CLAUDE.md                   # thin wrapper → points to AGENTS.md (Claude Code)
GEMINI.md                   # thin wrapper → points to AGENTS.md (Gemini CLI)
                            #   Codex CLI reads AGENTS.md directly — no wrapper file
.claude/agents/              # 4-role delegation roster: code-explorer, fast-task-executor,
                            #   hard-task-specialist, validation-runner (Claude Code format)
.codex/agents/                # same 4-role roster, Codex TOML format
.codex/config.toml            # general-manager model: optional, commented out by default
.claude/skills/              # skill wiring for Claude Code (symlinks into skills/)
README.txt                  # NFO-style entry point for humans & agents
SECURITY.md                 # reporting channel + pointer to the full policy
.gitignore  .editorconfig   # baseline tooling config
docs/
  README.md                 # docs map (who writes what)
  product/                  # vision + living, phase-based roadmap
  architecture/             # overview, locked stack, ADRs (+ ADR-0001, ADR template)
  process/                  # workflow, conventions, definition-of-done, session protocol
  features/                 # spec-before-code template
  memory/                   # progress · context · decisions (the AI writes these every session)
skills/                     # built-in skills: wrap-session · write-adr · review-own-diff
                            #   clean-code · write-tests · ponytail · caveman
.github/                    # quality-gate CI (templated) + PR template with the DoD
CHANGELOG.md                # skeleton versions — what a fork diverged from
```

Project-specific files (design system, entry files for further tools like
Copilot) are added by the interview only when they apply.

### Works with

Efes ships with **Claude Code** (`CLAUDE.md` + `.claude/skills/` + `.claude/agents/`), **Codex CLI** (reads `AGENTS.md` directly + `.codex/agents/`), and **Gemini CLI** (`GEMINI.md`) entry files by default. It's tool-agnostic, so the interview generates a matching entry file for any other agent you actually use — Cursor, Copilot, and others — on demand.

---

## License

Proprietary — see [`LICENSE`](./LICENSE). All rights reserved. A project forked from this skeleton should confirm whether to keep this license or pick its own during the interview (`EFES.md` §2A).
