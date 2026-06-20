---
name: design
description: Turn a research.md artifact into a design document — chosen approach, tradeoffs, and a task breakdown to tackle individually with plan mode. Third phase of the spec-driven development workflow.
argument-hint: [absolute path to research.md]
allowed-tools: Read, Write, Bash, Grep, Glob
---

# Design Skill

Synthesize a research artifact into a design: what approach we're taking, why, what alternatives we rejected, and a list of tasks to tackle individually.

This is a thinking artifact, not an implementation plan. No file paths with line numbers, no code snippets, no step-by-step edits. Those belong in plan mode, one task at a time.

## Input

`$ARGUMENTS` is an absolute path to an existing `research.md`. Read it in full, then read `task.md` via the `task_file` pointer in its frontmatter — that's the original task description you'll use to frame the design. Write `design.md` to the same folder as the research file.

If no path is given or the file doesn't exist, stop and ask the user for the path.

## Discipline

- **Reason through alternatives; document them rarely.** Always weigh other approaches before committing — that reasoning is what makes this a design, not a plan, and it should shape your `Chosen approach`. But the doc is not a transcript of that thinking. Document an alternative only when it was a genuine contender a reader would ask "why not X?" about, with a concrete reason you rejected it. If you're reaching for an option to fill the section, that's the signal to omit it. Most designs document zero alternatives.
- **Ground recommendations in the research.** Every tradeoff should cite research findings or existing patterns. If you're about to recommend something the research didn't surface, stop and verify it against the code.
- **No implementation detail.** No line numbers, no code, no method signatures, no "add X to file Y". Describe *what* changes conceptually, not *how* to edit. If a task starts naming files and lines, it's a plan, not a task.
- **tasks are units of work, not steps.** A task is something you'd tackle in one plan-mode session. "Add provider-dimension filter to the payment line query" is a task. "Edit line 142 of SagePaymentService.ts" is not.
- **Make dependencies explicit.** If tasks have a required order, say so. If they're independent, say that too.
- **Surface open questions in the doc.** If there are material ambiguities you'd otherwise guess at — tradeoffs, preferences, scope — list them in the `Open questions / gotchas` section so the user can answer on review. Don't silently pick.

You may spot-check the research against the code, but don't do new research here. If the research is insufficient, say so and stop — the user should iterate on research first.

## Output

Write `design.md` beside the research file. Copy the skeleton at `/Users/julian/.claude/skills/design/templates/design.md` and fill every placeholder; don't invent or omit frontmatter keys. Keep or drop the `Alternatives considered` and `Open questions / gotchas` sections per the rules in their placeholders.

After writing, print the absolute path and stop. Do not start planning tasks. Do not propose implementation. The user will iterate on the design, then tackle tasks individually with plan mode.
