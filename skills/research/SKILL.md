---
name: research
description: Produce an objective, fact-based analysis of how the codebase works today — either by answering a pre-defined questions.md from the SDD workflow, or by researching a free-form topic directly. Use whenever you need grounded context before designing or planning.
argument-hint: [absolute path to questions.md, or a free-form topic]
allowed-tools: Read, Write, Bash, Grep, Glob, Agent
---

# Research Skill

Produce an objective analysis of how the codebase works today. Compress truth — no implementation intentions, no recommendations, no proposals.

## Input

`$ARGUMENTS` is either a path to an existing `questions.md` or a free-form topic. If it resolves to an existing file you're **answering questions**; otherwise you're **researching a topic**.

- **Answering questions** — read the questions.md; its frontmatter points to `task_file` and `project_path`. Answer one section per question. Do **not** read `task.md` — the questions alone are your scope, and reading the task would bias your answers toward the intended solution. Write `research.md` beside the questions file.
- **Researching a topic** — pick a short kebab-case slug from the topic. Prompt the user for a Linear ticket ID; if provided, lowercase it and prefix the slug: `{ticket-id}-{slug}`. Write to `/Users/julian/Keeper/sdd/{slug}/`: `task.md` (the raw topic, no frontmatter) and `research.md`.

## Discipline

- **Facts, not intentions.** Every claim is about how the code works *today*. No "we should", "we could", "the fix would be". If you notice yourself recommending, stop and delete.
- **Self-check**: would this sentence read the same way if you didn't know what we were about to build? If not, rewrite it.
- **Cite everything non-trivial.** Use `path/to/file.ts:123` references. Unsourced claims decay into speculation.
- **Unresolved is a valid answer.** If something can't be determined from the code, say so explicitly (`**Unresolved**: ...`) and describe what you looked at. Don't handwave.

## Exploration

Use any tools you need. For broad scopes, spawn parallel subagents to explore and divide the work — decide the split based on the actual questions/topic, not a fixed template. Bias subagents toward thorough exploration. For narrow scopes, investigate directly.

## Output

Write `research.md` to the folder determined above. Copy the matching skeleton and fill every placeholder; don't invent or omit frontmatter keys.

- Answering questions → `/Users/julian/.claude/skills/research/templates/research-questions.md`
- Researching a topic → `/Users/julian/.claude/skills/research/templates/research-topic.md`

After writing, print the absolute path and stop. Do not propose next steps. Do not start designing. The user will iterate on the document and move on when ready.
