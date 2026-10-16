# Claude Routines Starter

Five production-ready routines for Claude Code — plus the guardrail checklist that stops them
failing silently. Free, MIT-licensed, no sign-up.

> A green status in the Claude Code run list means the session started and exited without an
> infrastructure error. **It does not mean the task in your prompt succeeded.**
> — [Anthropic's routines documentation](https://code.claude.com/docs/en/routines)

That gap is the entire problem with unattended automation. The run list is the only thing most
people look at, and it reports on the wrong thing: that the machine worked, not that the job
got done.

---

## The three failures that produce green

**1. The source that couldn't be read.** Your mail connector times out and the routine writes
"no urgent messages." That isn't good news — it's *no* news, and the output is byte-identical
either way. This is the expensive one, because nothing about it looks wrong.

**2. The check that never ran.** A health check that can't reach its endpoint and says nothing
reads exactly like a healthy system. On the default cloud environment a blocked host returns
`403` with `x-deny-reason: host_not_allowed` — a real, catchable error, if your prompt is
written to catch it rather than carry on.

**3. The run that fired at the wrong time.** Schedule exactly on the hour and it can start
several minutes late. A missed Desktop task runs as a single catch-up when the machine next
wakes — a 7am brief produced at 11pm, still written in the present tense about "today."

## The fix, in four lines

Every routine in this repo makes each source report exactly one of two outcomes:

```text
read: <count> items for <explicit window>
unavailable: <the exact error or refusal text>
```

Never infer absence from a failure. An empty section and an unreadable section must never look
the same. Two outcomes, never one.

---

## What's in here

| Path | What it is |
|---|---|
| `routines/` | Five full routine specs — prompt, prerequisites, sample run, first-run checklist, failure-mode table |
| `desktop-skills/` | The same five as drop-in `SKILL.md` files for `~/.claude/scheduled-tasks/<name>/` |
| `templates/` | The four state and log files the routines read and write, with exact headers |
| `GUARDRAIL_CHECKLIST.md` | The fourteen guardrail patterns, and the pre-flight check to run before you trust a routine |
| `HARDENING_SAMPLE.md` | The eight-point hardening pass, plus two of Anthropic's official templates rewritten in full |

A typeset PDF of this material is included in the free download at
[runbook.scosovan.com](https://runbook.scosovan.com) if you prefer it on paper.

The five routines:

- **A3 Morning Brief** — weekdays 06:45; relabels itself as an Afternoon Brief if it runs late
- **P1 Weekly Review & Plan** — Sunday 17:07
- **D1 Weekly Traffic & Search Digest** — Monday 08:07; works from GA4 / Search Console exports
- **O2 Weekly Reliability Review** — Monday 07:08; audits your other routines' run log
- **F4 Docs Drift Weekly** — Friday 17:07; for repositories with a docs folder

Those times end off the hour deliberately. Anthropic's docs recommend picking a few minutes
past — 9:07 rather than 9:00 — because on-the-hour runs can start late.

---

## Quick start (about 10 minutes)

1. Clone or download this repo.
2. Create a working folder and copy `templates/` into it as:
   `state/STATE.md`, `logs/RUNLOG.md`, `alerts/ALERTS.md`, `alerts/OWNER_ACTIONS.md`
3. In Claude Code Desktop: **Code → Routines → New routine → Local**
4. Paste the body of `desktop-skills/morning-brief/SKILL.md`, pick your folder, save.
5. Click **Run now**. Approve tools with "always allow" so later runs don't stall.
6. Read the transcript *and* `logs/RUNLOG.md`. The log line is the point.

Then break it on purpose: rename an input file and run again. A correct routine reports
FAILED with a clear owner action. One that invents an answer instead is the thing this repo
exists to prevent.

---

## Two things worth knowing before you schedule anything

**Every connector on your account is attached to a new routine by default**, and during a run
Claude can use any tool from an included connector — writes included — without stopping to ask.
Trim that list before the first run, not after the first incident.

**GitHub triggers don't reuse sessions.** Five pushes to an open pull request fire your routine
five times. Key your state on the head commit SHA, not the PR number, so a repeat run writes
nothing instead of writing a duplicate.

---

## Safety posture

Nothing here sends, posts, deletes or pays unattended. Every routine prepares work for a human
to approve. That's a deliberate default, not a limitation — it's what makes these safe to leave
running.

## Licence and provenance

MIT — see [LICENSE](LICENSE). Use it, fork it, adapt it commercially.

Platform behaviour cited here was verified against Anthropic's
[Routines](https://code.claude.com/docs/en/routines) and
[Desktop scheduled tasks](https://code.claude.com/docs/en/desktop-scheduled-tasks)
documentation. Claude and Anthropic are trademarks of Anthropic, PBC, used descriptively.
This is an independent project, not affiliated with Anthropic.

## The paid version, stated plainly

These five routines and the guardrail checklist are free and complete — not a trial. If you
want the rest, [The Routines Runbook](https://runbook.scosovan.com) is 32 routines across eight
job families, the full fourteen-pattern reliability kit, the memory and state architecture, the
hardening pack for all eight of Anthropic's official templates, the trigger playbook for API and
GitHub triggers, and a 55-page PDF guide.

You lose nothing by only ever using this repo.
