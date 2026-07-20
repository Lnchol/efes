# ADR-0006: Establish project identity as Efes; proprietary license

## Status

Accepted

## Context

This repo is a personal, reusable bootstrap kit — something forked again for
each future project, carrying this user's own defaults rather than generic
ones. Before it carries any personal defaults (see
[ADR-0007](0007-vendor-agent-role-pipeline.md)), it needs its own name and
its own license: a project meant to be reused and possibly shared selectively
shouldn't run under a placeholder identity or with no license at all.

## Decision

- The project's name is **Efes**. The bootstrap protocol file is `EFES.md`;
  every doc, entry file, and tool wrapper refers to the project by this name
  consistently.
- **License:** a root `LICENSE` — proprietary, all rights reserved,
  copyright holder "Efe". A project later forked from this skeleton picks
  its own license during its interview (`EFES.md` §2A); this repo's own
  copy is not a template default to inherit blindly.

## Consequences

- Every doc a session reads consistently refers to this project as "Efes",
  with a license that reflects it isn't an open template — sharing it with
  anyone is the owner's explicit choice, not a default.
- A project forked from this skeleton inherits "Efes" as its own starting
  identity unless it's renamed again for that project; nothing stops that.
- Historical ADRs (0001–0005) and `CHANGELOG.md` were revised to drop
  earlier terminology in favor of this identity, so the repo reads as one
  consistent project rather than a visible fork of something else.
