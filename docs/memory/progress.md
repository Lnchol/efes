# Progress

> Newest entry on top. Each entry: what changed + the **Next step**.

## 2026-07-21 — Made the repo public and safe to share

- Made the GitHub repo public. Tried two copy mechanisms before landing on
  the final one: (1) `gh repo create --template` — rejected, forces the
  copier to create their own GitHub repo; (2) `git clone` into a named
  folder + strip `.git` — rejected, still forces a placeholder folder name
  instead of using the folder the copier is already in. Landed on: `cd`
  into your project folder, then `curl -sL
  https://github.com/Lnchol/efes/tarball/main | tar xz --strip-components=1`
  — drops the files straight into the current folder, leaves any existing
  files alone, no `.git`, no account/repo needed. Verified against both an
  empty folder and one with a pre-existing file. Turned the GitHub template
  flag back off. Documented in `README.md` and `HOW-TO-USE.md`.
- `LICENSE` now explicitly permits anyone given access to the repo to use,
  copy, modify, and build on it for their own projects — closes the gap
  where sharing it didn't actually grant permission to use it.
  ([ADR-0008](../architecture/adr/0008-harden-for-sharing.md))
- Removed the enforced general-manager model default (`.claude/settings.json`
  deleted, `.codex/config.toml`'s `model =` commented out) — a hard-coded
  Fable 5 / flagship pin could error for someone without access to that
  model. `AGENTS.md` §10 and `EFES.md` §2F now frame it as a recommendation.
- Rewrote `HOW-TO-USE.md` in plainer language per request.
- **Open:** commit history still shows the real email
  `efekosan09@outlook.com` (now public) — offered to rewrite it to a GitHub
  no-reply address; needs explicit go-ahead since it requires a force-push.
- **Next step:** fork this repo for the first real project and run the
  `EFES.md` interview.

## 2026-07-21 — Added 5 skills, wired the full skill roster

- Added `spec-feature`, `provider-audit`, `module-boundary-check`,
  `commit-msg`, `specialize-agents` to `skills/` — chosen to operationalize
  golden rules that had no ritual yet (spec-before-code, provider
  independence, module boundaries, commit convention) plus a ritual for
  re-specializing the 4 agent files after initial bootstrap.
- Symlinked **all 12** skills into `.claude/skills/` — the previous 7
  built-ins were documented as "ships pre-wired" but the symlinks had never
  actually been created in this fork; fixed while adding the new 5 so the
  claim in `skills/README.md` is now true on disk.
- Updated `AGENTS.md` §8 and `skills/README.md` with the 5 new entries.
- **Next step:** fork this repo for the first real project and run the
  `EFES.md` interview.

## 2026-07-20 — Personalized as Efes (v0.6.0)

- Established the project identity as Efes across every file (`EFES.md`,
  `AGENTS.md`, `README.md`, `README.txt`, `SECURITY.md`, `docs/`, `skills/`,
  `.github/workflows/ci.yml`, historical ADRs, `CHANGELOG.md`) — no earlier
  terminology left anywhere. Added a proprietary `LICENSE` (owner: Efe).
- Vendored a fixed 4-role agent delegation roster — `code-explorer` →
  `fast-task-executor` / `hard-task-specialist` → `validation-runner` — as
  generic templates in `.claude/agents/*.md` and `.codex/agents/*.toml`,
  each with a `{{...}}` project-orientation block for a future bootstrap to
  fill in. General manager is the top-level session itself (no 5th
  orchestrator agent), defaulted to Fable 5 for Claude Code
  (`.claude/settings.json`) and a placeholder flagship model for Codex
  (`.codex/config.toml`). `AGENTS.md` §10 documents the roster; `EFES.md`
  §0.1/§2F/§4/§6 updated so the interview specializes (never recreates)
  these files. See ADR-0006 and ADR-0007.
- Added `GEMINI.md` (thin wrapper, ships by default); documented that Codex
  CLI reads `AGENTS.md` natively (no wrapper needed); dropped Cursor from
  the default tool roster (add back on demand if it comes into use).
- Deliberately left `AGENTS.md` §§1/4/5/6 (identity, stack, repo map,
  commands) as `{{...}}` — no concrete project exists yet.
- **Next step:** fork this repo for the first real project and run the
  `EFES.md` interview — it will fill the remaining `{{...}}` placeholders
  and specialize the 4 agent files for that project's actual domain/stack.

## 2026-07-12 — Cursor ships by default (v0.5.0)

- Added `.cursor/rules/000-start-here.mdc` to the skeleton: alwaysApply pure
  pointer (read order, always-on `ponytail`/`caveman`, end-of-session checklist
  pointer — no duplicated rule content). Claude Code and Cursor now both ship
  wired by default; Codex/Copilot/Gemini stay on-demand.
- Synced every place that stated the old on-demand-only policy: `AGENTS.md` §7,
  `EFES.md` §1 tree + §4 + §F wiring, `skills/README.md` §Wiring,
  `README.md` §Works with. Bumped skeleton to **v0.5.0**.
- Swept the skeleton for other "resets on fork" gaps: everything else is
  covered (README\* replaced by Mode B, memory templated/guarded, EFES.md
  deleted, CHANGELOG keep-or-delete, ADRs/skills inherited) — the one hole was
  **`LICENSE`** (no placeholder → invisible to the guard). Interview §A now
  asks license + owner; Mode B step 3 rewrites it.
- Clarified the fork memory question: §6 step 1 now says forks **reset
  `progress.md`** (skeleton maintenance entries are upstream history;
  `CHANGELOG.md` carries it) while `decisions.md` keeps the inherited
  skeleton-decision lines. Interview §F now suggests Serena-style
  code-navigation MCP (post-scaffold) and stack-idiom pre-commit hooks
  (husky / `pre-commit`) — recommendations only; both are per-project installs,
  nothing to install in the skeleton itself.
- **Next step:** run the Efes interview to fill `{{...}}`, or revisit issue
  templates/CODEOWNERS if/when a second contributor joins.

## 2026-07-11 — Governance hardening after full-skeleton audit

- Audited all 39 files. Verdict: session-start read set is ~3k tokens (net
  saving vs re-discovery); real risks were unbounded `progress.md` growth,
  wrapper drift, and skills not being natively discovered by tools. Recorded in
  [ADR-0005](../architecture/adr/0005-governance-hardening.md); skeleton is now
  **v0.4.0** (see `CHANGELOG.md`).
- Fixed drift: `CLAUDE.md` + `README.txt` were missing the test rule;
  `README.md` trees omitted `skills/` and `.github/`; the session ritual was
  copied verbatim in three places — `ai-session-protocol.md` is now canonical,
  `wrap-session` and `AGENTS.md` §2 point to it. `README.txt` slimmed to a pure
  pointer.
- New guards: `progress.md` rotation rule (>10 entries → archive all but newest
  5), wrapper re-sync step in the end-of-session checklist, prompt-cache
  stability rule for `AGENTS.md`, placeholder `grep '{{'` check + commented CI
  step, `EFES.md` deletion added to the §6 bootstrap ritual.
- New files: `CHANGELOG.md` (skeleton versioning for forks), root `SECURITY.md`
  pointer, ADR-0005. `.claude/settings.local.json` added to `.gitignore`.
- Skill wiring: interview §F + `skills/README.md` §Wiring now generate native
  per-tool discovery (Claude Code `.claude/skills/` symlinks, Cursor rule
  pointer) so skill bodies load lazily; `automation.md` gained a cost-hygiene
  section (model routing, sub-agent fan-out).
- **Next step:** run the Efes interview to fill `{{...}}`, or revisit issue
  templates/CODEOWNERS if/when a second contributor joins.

## 2026-07-11 — Vendor ponytail + caveman skills (less code, fewer tokens)

- Vendored two MIT upstreams as always-on built-in skills, distilled to their
  rulesets (no hooks/plugins): `skills/ponytail/` (the "does this need to
  exist" ladder — YAGNI → reuse → stdlib → native → dep → one line → minimum)
  and `skills/caveman/` (terse chat output, ~65% fewer output tokens; never
  compresses repo files). Recorded in
  [ADR-0004](../architecture/adr/0004-vendor-ponytail-caveman-skills.md).
- Reconciled with existing governance instead of copying blindly: ponytail's
  minimal self-check rule is overridden by test-first (ADR-0003); its
  no-single-impl-abstraction rule yields to provider independence; caveman got
  a hard repository-file boundary; wenyan levels trimmed.
- No existing rules turned out redundant — division of labor documented:
  `clean-code` = shape of code, `ponytail` = amount of code, `caveman` = chat
  output. Cross-references added in `clean-code`.
- Updated the skill lists in `AGENTS.md` §8, `EFES.md` §1 tree + interview
  §F (also added the previously missing `write-tests` there), `skills/README.md`.
- Evaluated and rejected context-compression proxies (Headroom): machine-level,
  ~15–20% realistic gain for coding agents, provider-cache/quality risk —
  rationale in ADR-0004.
- **Next step:** run the Efes interview to fill `{{...}}`, or revisit issue
  templates/CODEOWNERS if/when a second contributor joins.

## 2026-06-19 — Close governance gaps (security, logging, PR template, CI doc)

- Added `docs/process/security.md` (secrets, authz, input, dependency/supply-chain
  hygiene, vuln disclosure) and a **Logging & observability** section in
  `conventions.md` (structured logs, levels, no secrets/PII in logs, correlation).
- Added `.github/pull_request_template.md` with the DoD checklist embedded (user
  reviews even solo, so PRs are kept).
- Fixed `automation.md` doc drift: it claimed CI runs on push/PR while `ci.yml` is
  `workflow_dispatch`-only — now states the template runs on dispatch and you
  switch the trigger when commands are filled (no CI trigger added per decision).
- Added a stack-agnostic **performance/SLO** question to the interview
  (EFES §D); fixed a duplicate `workflow.md` line in the §1 tree.
- Added `skills/write-tests/` so the test-first discipline has a ritual; wired
  `security.md` into `docs/README.md`, the DoD, and EFES §1/§4.
- Deliberately skipped (per decision): CI auto-trigger, CHANGELOG (progress.md
  covers it pre-release), data-layer process doc (DB+migration questions suffice),
  `.env.example` (created per project), slash commands (agent-agnostic).
- **Next step:** run the Efes interview to fill `{{...}}`, or revisit issue
  templates/CODEOWNERS if/when a second contributor joins.

## 2026-06-19 — Bake test-first discipline into the skeleton

- Testing was implicit (a CI slot + a DoD checkbox + a placeholder) and read as
  optional. Made it first-class across the governance: `AGENTS.md` golden rule +
  NEVER, `EFES.md` interview §F + standards §5 + NEVER, the `workflow.md` loop
  (`READ → SPEC → TEST → PLAN → BUILD → VERIFY → RECORD → COMMIT`) and its
  invariants, `definition-of-done.md`, and a real `conventions.md` §Testing.
- Recorded the decision in [ADR-0003](../architecture/adr/0003-test-first-discipline.md)
  (refines the spec-lane loop from ADR-0002); runner stays a stack choice.
- **Next step:** consider a `skills/write-tests/` skill and adding `push`/`pull_request`
  triggers to `ci.yml`; otherwise run the Efes interview to fill `{{...}}`.

## {{DATE}} — Phase 0: governance foundation

- Assembled the skeleton: `AGENTS.md`, `CLAUDE.md`, `README.txt`, the
  `docs/` tree, the memory bank, the `skills/` tree, CI scaffold, and
  ADR-0001/0002 are in place.
- Workflow is **two-lane** (strict vibe + spec); vibe is the pre-alpha default.
- **Next step:** run the Efes interview (`EFES.md`) to fill the `{{...}}`
  placeholders, choose the default lane + which skills to seed + MCP/CI, and
  generate the project-specific docs, then start Phase 1 (scaffold).
