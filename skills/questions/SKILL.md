---
name: questions
description: Generate a set of objective, code-answerable research questions for a task. First phase of the spec-driven development workflow. Use before researching or planning so the research phase stays grounded in facts rather than solutions.
argument-hint: [task description]
allowed-tools: Read, Write, Bash, Grep, Glob
---

# Questions Skill

Produce a set of research questions about the codebase that will inform a later research phase. The questions must stay objective and must NOT leak what we intend to build.

## Input

Use `$ARGUMENTS` as the task description if provided. Otherwise use the most recent task description from the conversation.

## Guidance

Good questions:

- Are **objective** — answerable by reading the code, not by opinion.
- Are **well-scoped** — a researcher can answer each one in bounded time.
- Focus on: existing patterns, current behavior, constraints, related code, conventions, data shapes, call sites.

Before finalizing, run the **leak test** on every question: _could a researcher answer this without knowing what we're about to build?_ If not, rewrite it.

Aim for a small, high-signal set (typically 3–8 questions).

## Orientation

You may briefly skim the codebase to make questions concrete rather than generic, but do **not** deep-dive — that's the research phase's job.

## Workflow

1. Pick a short kebab-case slug for the task.
2. Prompt the user for a Linear ticket ID. If provided, lowercase it and prefix the slug: `{ticket-id}-{slug}`.
3. Target folder: `/Users/julian/Keeper/sdd/{slug}/`.
4. Write **two** files into the folder:
   - **`task.md`** — a polished version of the task description, no frontmatter. Polish means: fix grammar and typos, tighten phrasing, drop filler and conversational asides. Preserve every concrete detail, do not add information the user did not provide, do not infer a solution, and do not reframe the task. If the input is already clean, save it as-is.
   - **`questions.md`** — copy the skeleton at `/Users/julian/.claude/skills/questions/templates/questions.md` and fill in every placeholder. Do not invent or omit frontmatter keys.

After writing, print the absolute path and stop. Do not start researching. Do not prompt for iteration — the user will reply if they want changes.
