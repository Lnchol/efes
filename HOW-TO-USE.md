# How to Use Efes

Efes is a starter kit. You copy it, answer some questions, and it sets up
your new project for you.

## 1. Start a new project

One command — just downloads the files, no GitHub account or new repo needed:

```bash
git clone --depth 1 https://github.com/Lnchol/efes.git my-project && rm -rf my-project/.git
```

That gives you a plain `my-project` folder with all the files, no `.git`,
no link back to `efes`. Only needs `git` installed — nothing else. When
you're ready to put your own project on GitHub later, `cd my-project && git
init` (that's a separate step, whenever you actually want a repo).

Then:

1. Open the new folder in Claude Code (or Codex, or Gemini) and type:
   `Follow EFES.md`
2. It will ask you questions about your project — name, what it does, what
   language/tools you want. Not sure? Just say "use the default."
3. When it shows you a summary, say yes to confirm.
4. It fills in all the files and sets up 4 helper agents for your project.
   `EFES.md` deletes itself when done — you don't need it anymore.

## 2. Using it day to day

You don't need to do anything special. Just talk to Claude Code or Codex
like normal, and it automatically uses 4 helper agents behind the scenes:

- **code-explorer** — looks around the codebase first
- **fast-task-executor** — handles quick, simple changes
- **hard-task-specialist** — handles hard or complex changes
- **validation-runner** — runs tests to check the work

You can switch between Claude Code and Codex any time — both know about
these 4 agents, and both read the same project notes, so nothing is lost.

**Where the project "remembers" things:** the `docs/memory/` folder. Every
session reads it at the start and updates it at the end. That's how it
picks up where it left off, even days later.

**Nothing gets committed to git unless you ask for it.**

## 3. What are "skills"?

Skills are small instruction files that tell the AI how to do a specific
task well (like writing a commit message, or reviewing code). They live in
the `skills/` folder. You don't need to call them by name — just ask for
what you want, and the right one gets used.

| Skill | Use it for |
|---|---|
| `wrap-session` | Wrapping up a work session |
| `write-adr` | Writing down an important decision and why you made it |
| `review-own-diff` | Double-checking your own change before calling it done |
| `clean-code` | General code quality while writing/editing |
| `write-tests` | Adding tests for new or changed behavior |
| `ponytail` | Keeps solutions simple (always on) |
| `caveman` | Keeps chat replies short (always on) |
| `spec-feature` | Writing up a plan before building a new feature |
| `provider-audit` | Checking a 3rd-party service isn't hardcoded in |
| `module-boundary-check` | Checking parts of the code aren't tangled together |
| `commit-msg` | Writing a proper commit message |
| `specialize-agents` | Updating the 4 helper agents if the project changed a lot |

## 4. Adding your own skill

1. Copy `skills/_template/SKILL.md` to a new folder under `skills/`.
2. Fill in what it does and when to use it.
3. Link it so Claude Code can see it:
   `ln -s ../../skills/<name> .claude/skills/<name>`

## 5. If something goes wrong

- **New agent isn't showing up?** Restart the session.
- **Can't push `.github/workflows/ci.yml` to GitHub?** Run:
  `gh auth refresh -h github.com -s workflow`, then try again.
- **See a file you don't recognize in the project?** Don't delete it —
  check first, it might belong to something else running on your machine.
