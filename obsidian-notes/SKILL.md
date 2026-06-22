---
name: obsidian-notes
description: Create structured Obsidian knowledge notes from the current conversation, project context, meeting notes, technical troubleshooting, workflow learnings, or topic discussions. Use when the user asks to summarize, capture, save, write, or organize context into Obsidian with properties, key takeaway, reusable bullet sections, and references.
---

# Obsidian Notes

Use this skill to turn a conversation or project/topic context into a durable Obsidian note. The output should be useful weeks later: searchable, concise, action-oriented, connected to adjacent notes, and easy for another Agent to reuse.

## Core Workflow

1. Identify the note subject from the current conversation: project, topic, decision, workflow, configuration, issue, or reusable method.
2. Classify the note type:
   - `agent-workflow`: Agent behavior, MCP/tool setup, repeatable workflow.
   - `project-note`: Project context, decisions, next steps.
   - `technical-note`: Configuration, commands, debugging, architecture.
   - `decision-record`: Chosen direction, rejected options, rationale.
   - `reference-note`: Durable knowledge or reusable method.
3. Choose a destination folder. Default to `00-Agent(工作流沉淀）/` for Agent workflows and tool setup unless the user specifies otherwise.
4. Draft the note using `references/note-template.md`.
5. Apply `references/style-guide.md` before writing.
6. Add internal wiki-style note relationships in `## 文件引用` when there are meaningful upstream, sibling, downstream, or project-context notes.
7. Run the quality checklist before writing.
8. If an Obsidian MCP or Local REST API connection is available, write the note and read it back to verify title, properties, `Key takeaway`, `摘要`, `文件引用`, and the final reusable section exist. If not available, provide the Markdown note for manual insertion.

## Required Note Shape

Every note must include:

- YAML Properties with creation metadata, update metadata, source, topic/project, knowledge type, confidence, related notes/projects, and tags. Do not include a `links` property; put URLs and local paths in `Key references`.
- One specific H1 title.
- `## Key takeaway`: an Obsidian callout block containing one sentence with the most reusable conclusion, followed by one short explanatory paragraph. Do not pad with generic filler.
- `## 摘要`: an Obsidian callout block with three short bullets for immediate scan-reading.
- `## Context`: an Obsidian callout block containing compact background, goal, current status, and scope bullets.
- Bullet-based content blocks with clear subheadings.
- `## 后续可复用关键信息`: split into `### 环境与入口` and `### 迁移与验证` tables with portable facts, commands, constraints, gotchas, and decisions.
- `## Key references`: grouped external evidence such as official docs, local files, repo paths, user-provided URLs, and API endpoints.
- `## 文件引用`: Obsidian internal wiki links that express major knowledge relationships between notes.

## Writing Rules

- Prefer concrete nouns, paths, commands, tool names, config keys, and decisions over generic summaries.
- Preserve exact local paths, ports, tool names, and filenames when they matter.
- Use tables for configuration matrices, option comparisons, command checklists, or field definitions.
- Use Mermaid only when a small diagram makes a workflow easier to reuse.
- Do not include secrets, API keys, cookies, or tokens unless the user explicitly asks to include them.
- Read and write Markdown as UTF-8. On Windows PowerShell, specify `-Encoding UTF8` when reading files whose Chinese headings matter.
- Keep `Key references` and `文件引用` separate: external evidence belongs in `Key references`; internal Obsidian note relationships belong in `文件引用`.
- When writing to an existing note, read first and patch targeted sections when possible. Avoid whole-file overwrite unless creating a new note or replacing a generated draft with user approval.
- For destructive actions such as delete, move, or broad replacement, require explicit user confirmation.

## Quality Checklist

Before writing or updating a note, verify:

- YAML contains `created_at`, `updated_at`, `source`, `project`, `topic`, `note_type`, `knowledge_type`, `status`, `confidence`, `related_projects`, `related_notes`, and `tags`.
- `Key takeaway` has exactly one reusable conclusion sentence and one dense explanation paragraph.
- `摘要` has exactly three bullets and does not duplicate the full takeaway paragraph.
- `Context` is compact and contains background, goal, current status, and scope.
- `后续可复用关键信息` includes concrete paths, endpoints, commands, configuration keys, validation checks, or decision boundaries when available.
- `Key references` contains only external references or local filesystem/repo paths.
- `文件引用` contains only meaningful Obsidian wiki links such as `[[Obsidian MCP 接入经验]]`, with a short reason for each relationship.
- No secret, API key, cookie, token, auth code, or bearer value is written unless the user explicitly asks for that exact disclosure.

## Obsidian Write Guidance

Prefer MCP tools in this order when available:

1. `vault_write` for new notes.
2. `vault_read` to verify write results.
3. `vault_get_document_map` before targeted edits to existing notes.
4. `vault_patch` for heading/frontmatter updates.
5. `vault_append` only when appending is intentional and duplication is acceptable or guarded.

When using Obsidian Local REST API with MCP manually:

- Use `https://127.0.0.1:27124/mcp/` for Streamable HTTP MCP.
- Send JSON without UTF-8 BOM.
- Include `Authorization: Bearer <token>`, `Content-Type: application/json`, and `Accept: application/json, text/event-stream`.
- Keep `Mcp-Session-Id` from initialization for subsequent calls.

## Reference Files

- Read `references/note-template.md` whenever drafting a note.
- Read `references/style-guide.md` whenever deciding how much detail, formatting, or visual structure to include.
