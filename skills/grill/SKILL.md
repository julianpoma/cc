---
name: grill
description: Interactively grill a design, plan, or research doc — cross-referenced against the codebase — to surface inconsistencies, ambiguities, missing edge cases, and shaky assumptions. Asks the user questions one at a time to resolve issues; persists resolutions back to the artifact or a sibling file. Works on a file path, a free-form topic, or the current in-conversation plan.
argument-hint: [absolute path to an artifact, a free-form topic, or empty to grill the current plan]
allowed-tools: Read, Write, Edit, Bash, Grep, Glob, AskUserQuestion
---

# Grill Skill

Grill **$ARGUMENTS** by cross-referencing it against the codebase, then interview the user to resolve what remains. The goal is to surface real issues before implementation — don't soften.

## Discipline

- Be direct and specific; don't make the critique performative.
- Don't invent certainty where the codebase doesn't provide it. Mark inferences explicitly.
- Keep questions tied to decisions that would change implementation, scope, or risk.

## Workflow

1. **Load the artifact.** If `$ARGUMENTS` is a file path, read it and any obvious sibling context (`task.md`, `research.md`, `design.md`). If it's a free-form topic, probe the codebase for context. If it's empty, use the plan in the current conversation. If there's nothing to grill, ask the user what they want grilled.

2. **Audit and interview.** Find the weak spots — contradictions with the codebase, internal contradictions, missing edge cases, shaky assumptions, ambiguities, design-level bugs — and drill the user on them. Cite evidence (artifact line + code location) so the user can push back. Follow up when answers open new ambiguity. Stop once the material concerns are resolved.

3. **Persist resolutions.** Record each resolved concern (what, decision, why) in a `grill.md`. If the artifact lives in an SDD folder (`/Users/julian/Keeper/sdd/{slug}/`), write it there alongside the other docs. Otherwise — a free-form topic, the in-conversation plan, or an artifact outside an SDD folder — ask the user where to save it before writing. Print the absolute path.

## Tactics

- Sharpen fuzzy or overloaded terms ("'account' — Customer or User?").
- Probe with concrete edge-case scenarios to force precision.
- Surface code/claim contradictions directly ("code does X, you said Y — which?").
- Propose a recommended answer with each question so the user can confirm or redirect rather than start from blank.
