---
name: impl
description: Implement a specific phase (or all phases) from an existing plan. Executes tasks step by step, runs typechecks and tests, and marks progress in the plan document.
argument-hint: [phase number or "all"] [plan folder name]
allowed-tools: Read, Grep, Glob, Bash, Write, Edit, LSP
---

# Impl Skill

Implement from the plan. If `$0` is a number, implement only that phase. If `$0` is "all", implement all phases sequentially. If a folder name is provided as `$1`, use `plans/$1/plan.md`. Otherwise, find the most recently modified `plans/*/plan.md`.

## Process

1. **Read the plan** — Read the full `plan.md` and locate the target phase in the Todo section.
2. **Find project commands** — Read `package.json` to identify the correct scripts for typechecking (`build`, `typecheck`, `tsc`, etc.) and testing.
3. **Execute each task** — Implement the tasks in order, one by one. Do not skip any task. Do not stop until all tasks in the phase are completed.
4. **Mark progress** — After completing each task, update the `plan.md` to mark it as done (`- [x]`). When all tasks in the phase are done, mark the phase itself as done too.
5. **Verify continuously** — Run the project's typecheck command regularly as you work to catch type errors early. Fix any issues you introduce before moving on.
6. **Run tests** — Before marking the phase as complete, run the relevant tests and make sure they pass. If tests fail, fix them.

## Rules

- When a specific phase is given: do NOT implement tasks from other phases — only the specified phase.
- When "all" is given: proceed through every phase in order, marking each phase complete before moving to the next.
- Do NOT make changes outside the scope of the plan.
- Follow the project's CLAUDE.md for all code style and conventions.
