---
name: clarify
description: Interview the user about a plan, research, or feature to resolve ambiguities and reach shared understanding. Use when business rules, conventions, or design decisions are unclear.
argument-hint: [plan folder name or topic]
allowed-tools: Read, Grep, Glob, LSP, Write
---

# Clarify Skill

Interview the user relentlessly about **$ARGUMENTS** until you reach a shared understanding.

## Process

1. **Load context** — If a `plans/$ARGUMENTS/plan.md` or `plans/$ARGUMENTS/research.md` exists, read them. Otherwise, treat `$ARGUMENTS` as a topic and gather context from the codebase.

2. **Explore first** — Before asking, try to answer your own questions by reading the codebase. Only ask the user about things that cannot be determined from code — business rules, product intent, edge case behavior, conventions, preferences.

3. **Interview systematically** — Walk down each branch of the design tree. Resolve dependencies between decisions one by one. Cover:
   - Business rules and expected behavior
   - Edge cases and error scenarios
   - Scope boundaries — what's in, what's out
   - Interactions with other features
   - Data constraints and invariants
   - User-facing vs internal behavior

4. **One topic at a time** — Ask focused questions, not long lists. Wait for the answer before moving to the next branch. Follow up on answers that reveal new ambiguities.

5. **Persist decisions** — After all branches are resolved, append a `## Decisions` section to the existing `plan.md` or `research.md` in `plans/$ARGUMENTS/`. Each decision should be a concise statement of what was decided and why. If no plan or research document exists yet, write the decisions to `plans/{folder}/decisions.md`.

## Rules

- NEVER guess or assume business rules — ask.
- DO explore the codebase to answer technical questions yourself.
- Keep questions concrete and specific, not abstract.
- If the user's answer contradicts something in the codebase, flag it.
