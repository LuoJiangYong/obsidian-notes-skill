# Obsidian Note Style Guide

## Key takeaway

Render this section as an Obsidian callout so it appears as a highlighted block:

```markdown
## Key takeaway

> [!tip] Key takeaway
> One sentence with the reusable conclusion.
>
> One short practical explanation paragraph.
```

Write exactly two parts inside the callout:

1. One sentence: the most reusable conclusion.
2. One short paragraph: the practical explanation needed to apply that conclusion later.

The paragraph should answer: when does this matter, what is the core move, and what must not be forgotten? Do not restate the title or add generic value claims.

Good:

> Prefer the plugin's native MCP endpoint when the Obsidian Local REST API plugin already exposes `/mcp/`, and only use a stdio wrapper when the client cannot speak Streamable HTTP.
>
> This matters because wrapper packages may assume different REST paths, causing tools to initialize successfully but fail at call time. Verify the plugin's OpenAPI and run a `tools/list` plus one write/read loop before treating the setup as reusable.

Weak:

> This note explains how to connect Obsidian MCP.
>
> It is useful for future work and helps Agents be more productive.

## Properties

Use YAML frontmatter. Prefer stable, searchable values:

- `created_by`: usually `Codex`.
- `created_at`: local date in `YYYY-MM-DD`.
- `created_method`: concise origin, such as `conversation-to-obsidian-note`.
- `source`: `conversation`, `meeting`, `repo`, `document`, or `manual`.
- `project`: exact project or repo name when known.
- `topic`: specific topic.
- `note_type`: one of `agent-workflow`, `project-note`, `technical-note`, `decision-record`, `reference-note`.
- `status`: `captured`, `draft`, `validated`, or `needs-review`.
- `tags`: 2-6 tags; use lowercase English where possible for search consistency.

Do not include `links` in Properties. Put URLs and local paths in `## Key references`.

## Context

Render context as an Obsidian callout immediately after `## Context`:

```markdown
## Context

> [!info] Context
> - 背景：
> - 目标：
> - 当前状态：
> - 适用范围：
```

Keep this block compact. It should orient the reader, not duplicate the whole note.

## 摘要

Add exactly three bullets in an Obsidian callout after `Key takeaway` and before `Context`.

Use this pattern unless the note type clearly needs different labels:

```markdown
## 摘要

> [!summary] 摘要
> - 优先路径：
> - 验证闭环：
> - 主要坑点：
```

Each bullet should fit on one line when possible. Do not duplicate the full Key takeaway paragraph.

## Content Blocks

- Use H2 for stable sections and H3 for scannable subtopics.
- Prefer bullets over paragraphs for facts, decisions, commands, and caveats.
- Use tables for reusable configuration, option comparison, and "what to do next" matrices.
- Keep local paths and command names exact.
- Include a Mermaid diagram only if it compresses a process or dependency chain.

## 后续可复用关键信息

This section replaces generic "Risks / Caveats". It should contain the information a future Agent needs to act without rediscovery:

- exact paths and folders
- endpoint URLs and ports
- command snippets
- configuration keys
- auth/header format rules
- known incompatibilities
- validation checks
- decision boundaries
- next safe action

Split this section into two subsections by default:

```markdown
## 后续可复用关键信息

### 环境与入口

| 项 | 值 | 用途 |

### 迁移与验证

| 检查项 | 标准 | 失败时处理 |
```

Use `环境与入口` for stable facts: paths, endpoints, ports, config keys, vault locations.
Use `迁移与验证` for action checks: health checks, tool list checks, write/read loops, known failure handling.

## Key References

Include only references that help the next run:

- official docs or OpenAPI endpoints
- local files created or modified
- important repo paths
- user-provided links
- relevant notes already in Obsidian

Do not invent references. If there are none, write `- None captured`.

Group references by category. Use only categories that have content:

```markdown
## Key references

### Obsidian notes

### Local files

### API endpoints
```
