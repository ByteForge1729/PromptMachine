# Archetype: CLI tool

Load when the brief mentions a terminal, a command, a script, a developer tool, or
"something I run from the command line".

**The governing rule of this archetype:** a command-line tool lives inside other
people's machines and other people's scripts. It meets Windows paths, missing runtimes,
shell history, pipes, CI servers with no human watching, and users who read none of the
docs. Every one of those is a decision the user has not made yet.

---

### C1: who runs it `[required]`
**Ask:** Who types this command: only you, other developers, or people who have never
opened a terminal? If it is the last group, a command-line tool is probably the wrong
shape; a small web page or desktop app would reach them better.
**Options:** just me / developers (recommended scope for a CLI) / non-technical people
(consider switching to `web-app.md`)
**Opens:** install method (C2), how friendly errors must be (C9)

### C2: how it gets installed `[required]`
**Ask:** How does someone install it? A package manager (npm, pip or pipx, Homebrew) is
easy but requires them to already have Node or Python. A single downloadable file works
anywhere but must be built separately for each operating system.
**Options:** the package manager of the language you write it in (recommended) / single
download per OS / clone the repo and run it (fine for "just me")
**Opens:** C3, release process, update path (C10)

### C3: Windows `[required, when others will use it]`
**Ask:** Must it work on Windows? That is where command-line tools break: different path
separators, a different shell, different line endings, colour codes that print as junk.
Deciding now costs little; discovering it from a bug report costs a lot.
**Options:** Mac and Linux only, say so (recommended if the audience allows) / all three,
tested on each / Windows through WSL only
**Opens:** path handling, test matrix, C2 builds

### C4: people or scripts `[required]`
**Ask:** Will people run it by hand, or will it also run inside scripts and automated
pipelines with nobody watching? A tool that stops to ask a question hangs forever in a
pipeline.
**Options:** both: prompts only when a person is watching, flags for everything
(recommended) / by hand only / scripts only
**Opens:** flag design, C5 output, C7 confirmations

### C5: output for humans and machines `[required]`
**Ask:** Will other programs read its output? Pretty tables for people and plain JSON for
programs are two different outputs. Mixing messages into the data breaks every script
that pipes it.
**Options:** readable by default plus a `--json` option (recommended) / readable only /
JSON only
**Opens:** stdout versus stderr split, exit codes

### C6: settings and secrets `[required, when it needs a token or password]`
**Ask:** Where do settings and secrets (API keys, tokens) come from? A secret passed as a
command argument is saved in shell history and visible to other users on the machine.
**Options:** environment variables plus an optional config file (recommended) / config
file only / flags (never for secrets)
**Opens:** config location, O3 privacy, docs

### C7: destructive actions `[required, when it deletes, overwrites or sends anything]`
**Ask:** When it deletes, overwrites or sends something, does it show what it would do
first? A `--dry-run` preview and a confirmation, skippable with `--yes` for scripts, stop
the "I just wiped the wrong folder" moment.
**Options:** dry-run plus confirmation plus `--yes` (recommended) / confirmation only /
nothing
**Opens:** C4, undo possibilities

### C8: long jobs and Ctrl+C `[optional]`
**Ask:** If a job takes minutes, what shows while it runs, and what happens when someone
presses Ctrl+C halfway? A half-written file or half-sent batch is worse than no run.
**Options:** progress shown, clean stop, can resume (recommended for long jobs) / progress
and clean stop only / neither
**Opens:** temp files, idempotency (I5), state files

### C9: errors that say what to do `[optional]`
**Ask:** When it fails, does the message say what went wrong and what to do next? "Error:
ENOENT" loses users; "Couldn't find config.yml. Run `tool init` to create one." keeps them.
**Options:** every known error has a next step (recommended) / plain error plus
`--verbose` for detail
**Opens:** error catalogue, docs

### C10: updates `[optional]`
**Ask:** How do users learn a new version exists, and what happens when you rename a flag?
Scripts that use the old flag break silently.
**Options:** semantic versions, old flags kept with a warning for one release
(recommended) / update notice when run / no promise
**Opens:** changelog, release process

### C11: phoning home `[optional]`
**Ask:** Will it send any usage data back to you? Developers react strongly to this.
**Options:** none (recommended) / opt-in only / on by default with an easy opt-out
**Opens:** O3 privacy, docs

### C12: no internet `[optional, when it calls a service]`
**Ask:** Does it need the internet? What happens on a plane or behind a company firewall?
**Options:** works offline for everything local, clear message otherwise (recommended) /
online only
**Opens:** S4 outside services, caching

### C13: help `[optional]`
**Ask:** Beyond `--help`, should it have examples, a man page, or tab-completion for
commands?
**Options:** `--help` with real examples, plus tab-completion (recommended) / `--help` only
**Opens:** docs, release assets

---

## Defaults for this archetype

- `--help` and `--version` on every command.
- Exit code 0 on success, non-zero on failure, documented.
- Data to stdout, messages and progress to stderr.
- Respect `NO_COLOR` and plain output when not in a terminal.
- No usage data sent anywhere.
- Config under the platform's standard config folder.

## Cascade rules

| If the answer is | Add these |
|---|---|
| used by others | C2, C3, C9, C10 |
| runs in scripts | C4 no-prompt mode, C5 JSON, exit codes |
| handles secrets | C6, O3 |
| deletes or sends things | C7, C8 |
| calls a service | C12, S4, rate limits |
