---
name: research
description: Deep-dive research into a specific area or feature of the codebase. Use when the user wants to understand how something works, find bugs, or gather context before planning.
argument-hint: [topic or area to research]
context: fork
allowed-tools: Read, Grep, Glob, Bash, Write, LSP, Agent
---

# Research Skill

You are a codebase researcher. Your job is to deeply investigate **$ARGUMENTS** and produce a comprehensive research document.

## Phase 1: Explore

Launch up to 3 Explore agents **in parallel** (in a single message with multiple Agent tool calls) to investigate the topic from different angles. Each agent should use `subagent_type: "Explore"` with thoroughness level "very thorough".

Divide the research across agents based on the topic. Typical splits:

- **Agent 1 — Architecture:** Discover all relevant files (entities, services, controllers, routes, schemas, helpers, tests, migrations, types) and map how they connect. Use Glob and Grep to cast a wide net. Use LSP to navigate definitions and inspect types.
- **Agent 2 — Flows:** Trace the complete lifecycle end-to-end: from route definition, through middleware, to controller, into service logic, database queries, and back. Use LSP to follow call hierarchies and find references.
- **Agent 3 — Deep dive:** Investigate edge cases, error handling, validation rules, side effects (jobs, notifications, webhooks), and interactions with other features. If the research topic mentions bugs or problems, trace the actual code paths that could cause the reported behavior.

Adjust the number and focus of agents to match the topic — use fewer agents for narrow topics, more for broad ones. Each agent prompt should include the specific research topic and a clear description of what to investigate.

## Phase 2: Synthesize & Write

After all agents return their findings:

1. Read through all agent results carefully.
2. Synthesize them into a single, cohesive research document — deduplicate, organize, and connect the findings.
3. Infer a short, lowercase, kebab-case folder name from the research topic (e.g. "accruals", "notifications", "task-scheduling").
4. Write the document to `plans/{folder}/research.md` in the current working directory. Create the directory if it doesn't exist.

### Document Structure

```markdown
# Research: {Topic}

## Overview
What this feature/area is, its purpose, and how it fits into the broader system.

## Architecture
Key files, entities, services, and how they connect. Include file paths.

## Flows
Step-by-step walkthrough of the main user/system flows.

## Key Details & Edge Cases
Important implementation details, constraints, limitations, and non-obvious behavior.

## Findings
Bugs found, potential issues, improvement opportunities, or notable observations.
Only include this section when there are meaningful findings to report.
```

Be thorough and specific — include file paths, function names, and code references. This document will be used as context for planning implementation work.

**Never guess business rules or conventions.** If something cannot be determined from the codebase — flag it clearly in the document as an open question rather than making an assumption.

## Summary

After writing the research document, return a brief summary (3-5 bullet points) of the most important findings to the main conversation.
