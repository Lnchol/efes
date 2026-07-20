# Decisions

> One short line per locked decision, newest on top, linking its ADR.

- Vendored a fixed 4-role agent delegation roster (explore/fast/hard/
  validate) for Claude Code + Codex CLI, specialized per project by the
  bootstrap interview; general manager = top-level session, no 5th
  orchestrator agent →
  [ADR-0007](../architecture/adr/0007-vendor-agent-role-pipeline.md)
- Established project identity as Efes with a proprietary license
  (owner: Efe) →
  [ADR-0006](../architecture/adr/0006-project-identity-and-license.md)
- Cursor entry file + skill pointer ship by default (like Claude Code); other
  tools stay on-demand → `CHANGELOG.md` v0.5.0
- Governance hardening: progress rotation, canonical session ritual, skeleton
  versioning (`CHANGELOG.md`), native per-tool skill wiring, bootstrap
  placeholder guard, post-bootstrap `EFES.md` removal →
  [ADR-0005](../architecture/adr/0005-governance-hardening.md)
- Vendored `ponytail` (minimal-code discipline) + `caveman` (terse chat output)
  as always-on built-in skills; context-compression proxies (Headroom) rejected →
  [ADR-0004](../architecture/adr/0004-vendor-ponytail-caveman-skills.md)
- Test-first discipline with a stack-appropriate runner; tests are first-class,
  not optional →
  [ADR-0003](../architecture/adr/0003-test-first-discipline.md)
- Two-lane workflow (strict vibe + spec) with shared invariants; full SDD/PR
  ceremony deferred to post-alpha/beta →
  [ADR-0002](../architecture/adr/0002-two-lane-workflow.md)
- Adopted an agent-first governance model →
  [ADR-0001](../architecture/adr/0001-adopt-agent-first-governance.md)
