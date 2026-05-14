# Backseat Driver

Installs as `bsd`. A Claude Code skill that audits your codebase for realistic failure modes
across eight categories — concurrency, silent data loss, stale derived state,
misconfig propagation, auth edge cases, persistence integrity, absent-value
assumptions, error swallowing — then quizzes you on them one round at a time.

Think of it as a real-life backseat driver. It doesn't *know* the road forks
the wrong way — it calls out every hazard in sight and makes you say out loud
whether you'd planned for it. Many flags will be false alarms. The value is
the forced moment of attention, not the hit rate.

## Install

```sh
cd ~/.claude/skills && git clone https://github.com/harikb/bsd
```

Open Claude Code; the skill is now discoverable as `/bsd`.

### Update

```sh
git -C ~/.claude/skills/bsd pull
```

### Uninstall

```sh
rm -rf ~/.claude/skills/bsd
```

## Usage

In Claude Code, invoke the skill:

```
/bsd
```

Claude scans the files in context, builds a ledger of 3–7 failure targets
(each from a different category), then walks you through them one at a time.
Each round presents a concrete scenario referencing real lines in your code
and asks: *what breaks, and what does the user see?*

You get a hint if you're stuck, the fix whenever you ask for it, and a
running tally of categories covered vs. remaining. End of session prints a
table of every target found.

## What this is — and what it isn't

This isn't a bug finder. It's a backseat driver: it points at code patterns
that *match* common failure modes and asks you to defend each one. Your job
per round is either (a) "yes, that's a real bug" and fix it, or (b) walk
through why it *can't* actually break — "this can't race because X holds the
lock," "this can't lose data because Y is idempotent."

Some findings will be real. Many won't. The discipline of explaining *why*
something is safe — out loud, against a specific call sequence — is most of
the value. You're training the instinct to pause at these patterns in the
future, when no one's quizzing you.

## License

MIT.
