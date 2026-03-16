---
name: spec
description: Create a detailed implementation plan for a feature, bug fix, or refactor. Use after /research has been done and context is available, or when the user describes work to be planned.
argument-hint: [what to implement or fix]
allowed-tools: Read, Grep, Glob, Bash, LSP, Write, AskUserQuestion
---

# Spec Skill

You are an implementation planner. Your job is to create a detailed, actionable plan for: **$ARGUMENTS**

## Process

1. **Gather context** — Look for an existing `plans/*/research.md` related to this topic. If one exists, read it thoroughly — it contains deep research that should inform your plan, and reuse the same folder for the plan. If not, do your own exploration first.

2. **Explore further** — Even with existing research, read the actual source files you plan to modify. Use the LSP tool to navigate definitions, references, and type hierarchies. Never suggest changes to code you haven't read. Base every recommendation on the actual codebase.

3. **Design the approach** — Think through the implementation step by step. Consider:
   - What entities, services, controllers, routes, schemas, and migrations need to change?
   - What existing patterns and utilities can be reused?
   - Are there analogous features already in the codebase that should serve as a reference? (e.g. if building a new CRUD endpoint, find an existing one and follow its patterns exactly)
   - What are the edge cases and error scenarios?
   - What's the right order of implementation?

4. **Discuss with the user** — Present your proposed approach and ask clarifying questions before writing the plan. Make sure you're aligned on scope, trade-offs, and any decisions that could go either way.

5. **Write the plan** — Once aligned, write the plan to `plans/{folder}/plan.md`. Infer the folder name from the topic (lowercase, kebab-case), reusing the same folder as the research if one exists. Create the directory if needed.

## Iteration

The plan is expected to go through revisions. The user will often:
- Review the `plan.md` file directly
- Add inline comments or notes right into the document (e.g. `<!-- TODO: reconsider this -->`, `NOTE: ...`, or freeform text annotations)
- Ask you to address their comments and update the document

When asked to review or address notes in the plan:
1. Read the current `plan.md` file carefully
2. Find all user comments and annotations
3. Address each one — update the plan content accordingly
4. Remove the resolved comments from the document
5. Do NOT start implementing — only update the plan unless explicitly told otherwise

## Plan Document Structure

```markdown
# Plan: {Title}

## Goal
What we're building/fixing and why.

## Changes

### 1. {Area of change}
- **File:** `path/to/file.ts`
- What to change and why
- Code snippets showing the approach

### 2. {Next area of change}
...

## Migration
SQL migration if schema changes are needed. Include the migration code.
Only include this section when applicable.

## Testing
How to verify the changes — what tests to write or update.

## Open Questions
Unresolved decisions or things to validate during implementation.
Only include this section when there are genuine open questions.
```

## Guidelines

- Include **code snippets** for non-trivial changes — show the actual function signatures, query shapes, or type definitions you're proposing.
- Reference **file paths** and **function names** so the plan is directly actionable.
- Follow the project's existing patterns — don't propose new abstractions unless necessary.
- Keep the plan scoped to what was asked. Don't suggest tangential improvements.
- Order the changes in the sequence they should be implemented.
- **Never guess business rules or conventions.** If something cannot be determined from the codebase, ask the user rather than making an assumption.
