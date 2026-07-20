# ADR-0008: Harden the template for sharing — permissive-use license, no forced model default

## Status

Accepted

## Context

The project is now a public GitHub template repo, meant to be copied by the
owner and by people they share it with (e.g. `gh repo create ... --template
Lnchol/efes`, or GitHub's "Use this template" button). Two things from
earlier decisions don't hold up under that use case:

- **License** ([ADR-0006](0006-project-identity-and-license.md)) was plain
  "all rights reserved, no use without permission" — technically true even
  for someone the owner explicitly shared the repo with, since nothing in
  writing granted them permission to use it.
- **General-manager model default** ([ADR-0007](0007-vendor-agent-role-pipeline.md))
  hard-coded Fable 5 in `.claude/settings.json` and a Codex flagship
  placeholder in `.codex/config.toml`. Someone copying the template may not
  have access to the same models — a hard-coded default risks erroring for
  them on first use, which fails the "no issues for a friend" bar directly.

## Decision

- **`LICENSE`** now explicitly grants anyone who has been given access to
  the repository (direct sharing, invitation, or its public GitHub listing)
  permission to use, copy, modify, and build on it for their own projects.
  It still forbids redistributing the repository itself as a product/
  template/service under different terms, or for commercial resale.
- **No enforced model default.** `.claude/settings.json` is removed;
  `.codex/config.toml`'s `model =` line is commented out with instructions.
  `AGENTS.md` §10 and `EFES.md` §2F now frame the general-manager model as a
  **recommendation** ("run the most capable model you have access to"),
  pinned per-user only if they choose to, not shipped as a default that
  could fail for someone without access to a specific model.

## Consequences

- Copying this template — for the owner's own next project, or for anyone
  they share it with — carries no license ambiguity and no risk of an
  invalid/inaccessible model default breaking the first session.
- The owner's own preference (Fable 5 as general manager) is now a note in
  the docs, not an enforced config — they set it themselves per session, or
  re-add a pinned default in their own fork if they want it back.
- This partially supersedes the model-default part of
  [ADR-0007](0007-vendor-agent-role-pipeline.md); the rest of that ADR (the
  4-role roster, no 5th orchestrator agent) still holds.
