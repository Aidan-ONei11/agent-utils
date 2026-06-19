---
description: Write a concise handoff file so a fresh session can resume this task with no lost context.
argument-hint: [optional focus notes, e.g. "emphasize the checkout bug"]
allowed-tools: Bash(pwd), Bash(git status:*), Bash(git branch:*), Bash(git rev-parse:*), Write
---

You are ending this session. Produce a handoff that lets a **brand-new Claude session with an empty context window** pick up exactly where you left off.

## Steps

1. Determine the current working directory (run `pwd`) and, if this is a git repo, the current branch and dirty state (`git rev-parse --is-inside-work-tree`, then `git status -sb`). If it is not a git repo, note that instead.
2. Write a file named `HANDOFF.md` in that working directory (use the **absolute path**) with the structure below.
3. Keep the whole file under ~40 lines. It is written TO a fresh Claude — imperative and factual, no "as we discussed", no narrative recap. Capture state, not story.
4. After writing, print to me a short copy-paste prompt for the next session (the exact text is in the final step).

If the user passed focus notes, weight the handoff toward them: $ARGUMENTS

## HANDOFF.md structure

```
# Handoff — <one-line task title>

**Project dir:** <absolute path>
**Git:** <branch + clean/dirty, or "not a git repo">
**Date:** <today>

## Goal
<what we are ultimately trying to accomplish — 1-2 sentences>

## Done so far
- <concrete things completed, with file paths>

## Next action (do this first)
<the single most immediate next step, specific and actionable>

## Then
- <ordered remaining steps>

## Key files
- `path/to/file.ext:line` — <why it matters>

## Decisions & gotchas
- <choices already made and why; traps to avoid; things that look wrong but aren't>

## How to verify
<exact commands / UI steps to confirm the work, and what a correct result looks like>

## Open questions
- <anything unresolved or needing the user's input>
```

## Final step — print this to me verbatim (fill in the real absolute path)

> **Start a new session, then paste:**
> `Read <absolute path>/HANDOFF.md to load context, continue the task from "Next action", and delete HANDOFF.md once you've absorbed it.`

Do not delete HANDOFF.md yourself — the next session deletes it after reading. Confirm the file was written and show its path.
