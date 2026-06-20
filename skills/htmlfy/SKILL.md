---
name: htmlfy
description: Turn the current conversation — research, a concept just learned, a PR walkthrough, a plan, a comparison — into a single self-contained, richly-styled HTML document. Use when the user wants the takeaways "as HTML", an "HTML explainer/report/artifact", or to make a chat result shareable beyond plain Markdown.
argument-hint: [optional: topic/title, or what to capture — defaults to the current conversation]
allowed-tools: Read, Write, Bash
---

# htmlfy

Render what we've been working on as one `.html` file. Opens by double-click, no build step (Tailwind and Mermaid load from CDN).

## Steps

1. **Source from the conversation** — real research, code, decisions, diagrams. Don't invent. If `$ARGUMENTS` names a topic, frame around it; else summarize the thread.
2. **Build from the template** at `/Users/julian/.claude/skills/htmlfy/templates/template.html` (read it) — it has the CDN includes, the Claude palette in Tailwind, and example components. Adapt; don't ship verbatim.
3. **Write** a kebab-case `.html` to the **current working directory**.
4. **Open it**: `open <file>`, then report the path + a one-line summary. Don't paste HTML into chat.

## Composition

- Use HTML's density: tables, Mermaid for flows, annotated code blocks, `<details>` for asides. Hand-author SVG when Mermaid can't express the layout.
- Structure visually: title + one-line summary header, table of contents, clear sections, whitespace.
- Color-code meaning (severity, tip vs gotcha). Accent is for links/labels/markers, not large fills.
- Be interactive only when it helps (sliders, draggable cards) — and pair editable state with a copy button that exports it back as JSON/Markdown/prompt.
- Mobile-responsive. Single file, Tailwind/Mermaid via CDN.

## Discipline

- **Faithful, not padded.** Preserve real content; don't manufacture filler to fill sections.
- **Match weight to content.** A quick explainer is one clean column; a PR review or 6-way comparison earns the full treatment. Don't over-build.
- **Working over fancy.** Every interactive element must actually work when opened.

The Claude palette is wired into the template as `claude-*` Tailwind colors — use those tokens.
