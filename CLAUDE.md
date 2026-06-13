# Global Claude Instructions

## Session Start

At the start of every session:
1. Run `git rev-parse --show-toplevel 2>/dev/null` to find the git root
2. If `project.md` exists at the root, read it and give a 2-3 line orientation: what the project is, what's pending
3. If NOT in a project, run `ls ~/projects/ 2>/dev/null` and silently note what's available — don't list them unless asked

## Project Routing

All personal projects live at `~/projects/<name>/main/`. When the user mentions a project name or describes work without being in a project directory:

1. Run `ls ~/projects/` to see available projects
2. Match the user's intent to the closest project folder name
3. Navigate there: the working path is `~/projects/<name>/main/`
4. Read `project.md` to orient, then proceed

If multiple projects could match, ask: "Did you mean X or Y?" If no projects exist yet, suggest `/personal` to create one.

## General Philosophy

Keep everything — project.md, code, prompts — as short and relevant as possible. Trim aggressively as things evolve. Dead weight compounds.

## Asking the User

Only escalate when automation genuinely can't cover it (physical device, external account login, design choice, or a problem you've iterated on and genuinely can't solve). Be specific about what you need and why.

**If you're stuck in a loop** — after **3 failed attempts** at the same approach, stop immediately. Summarize what failed, diagnose the root cause, and propose 2-3 genuinely different approaches. Ask the user to pick. Don't try a fourth time with the same strategy.

## Parallel Worktree Workflow

When working on a personal project and the task has multiple independent subtasks:

1. **Identify parallelism** — split the work into independent chunks that don't depend on each other's output
2. **Use separate worktrees** — create a git worktree for each chunk (`git worktree add ../task-name -b task-name`) so work happens in isolation
3. **Run agents in parallel** — spawn agents (or do work) across worktrees simultaneously, not sequentially
4. **Merge when done** — once all branches are complete, merge them into `main` and resolve any conflicts before reporting back

Use `git worktree remove` to clean up after merging.

## project.md

Single source of truth. Must stay current.

```
# Project: <Name>
## Overview
## Tech Stack
## Architecture
## Key Files
## How to Run
```
