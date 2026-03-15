---
name: todo
description: Add a detailed todo checklist to an existing plan. Use after a plan.md has been finalized and the user wants an actionable task list appended.
argument-hint: [plan folder name]
allowed-tools: Read, Write, Glob
---

# Todo Skill

Read the plan at `plans/$ARGUMENTS/plan.md` and append a detailed **## Todo** section to the end of the document.

If `$ARGUMENTS` is empty, look for the most recently modified `plans/*/plan.md` file and use that.

## Todo Structure

Group tasks by implementation phase, ordered in the sequence they should be executed. Each task should be specific and actionable — reference the exact file, function, or entity involved.

```markdown
## Todo

- [ ] **Phase 1: {name}**
  - [ ] Task 1
  - [ ] Task 2
- [ ] **Phase 2: {name}**
  - [ ] Task 1
  - [ ] Task 2
...
```

## Guidelines

- Derive phases and tasks directly from the plan's **Changes** and **Testing** sections — don't invent work that isn't in the plan.
- Keep tasks granular enough to be completed independently (e.g. "Add `status` column to `Task` entity" not "Update the database").
- Include migration, testing, and any cleanup as their own phases.
- Do NOT implement anything — only update the document.
