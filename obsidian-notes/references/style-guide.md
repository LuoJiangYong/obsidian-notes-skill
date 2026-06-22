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
- `updated_at`: local date in `YYYY-MM-DD`; set to the same value as `created_at` for new notes.
- `created_method`: concise origin, such as `conversation-to-obsidian-note`.
- `source`: `conversation`, `meeting`, `repo`, `document`, or `manual`.
- `project`: exact project or repo name when known.
- `topic`: specific topic.
- `note_type`: one of `agent-workflow`, `project-note`, `technical-note`, `decision-record`, `reference-note`.
- `knowledge_type`: one of `workflow`, `setup`, `decision`, `reference`, `troubleshooting`, or `project-context`.
- `status`: `captured`, `draft`, `validated`, or `needs-review`.
- `confidence`: `high`, `medium`, or `low`; use `high` only when the note was verified in the current run or backed by a reliable source.
- `related_projects`: YAML list of related project or repo names, empty list allowed.
- `related_notes`: YAML list of Obsidian note titles that have a meaningful knowledge relationship with this note, empty list allowed.
- `tags`: 2-6 tags; use lowercase English where possible for search consistency.

Do not include `links` in Properties. Put URLs and local paths in `## Key references`. Put Obsidian note titles in `related_notes` and explain the relationship in `## 文件引用`.

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

If the user provided a WeChat or other platform URL, include the exact original URL in `Context` as a visible source bullet. Also repeat it in `Key references` for evidence tracking.

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
- For business/project archive notes, preserve the original material's substantive content in the main body. Do not write a pointer note that only tells the reader where to look in the original file.
- For work-project materials such as 社群和会员运营、营销策划、商业运营、品牌活动、线上产品开发, prefer `原始内容完整整理`, `机制 / 模式`, `案例 / 对比`, and `可复制启示` over generic `Key points` or `Workflow / Method`.
- Do not include `Next actions` in archived work-project notes unless the user explicitly asks for an action plan or the note is an active project tracker.

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

Include only external references and concrete source locations that help the next run:

- official docs or OpenAPI endpoints
- local files created or modified
- important repo paths
- user-provided links

Do not invent references. If there are none, write `- None captured`.

Group references by category. Use only categories that have content:

```markdown
## Key references

### Obsidian notes

### Local files

### API endpoints
```

## 文件引用

Use this section to make the note work like a small personal wiki node. It should explain the main knowledge relationships between this note and other Obsidian notes.

Use Obsidian wiki links only, such as `[[Obsidian MCP 接入经验]]`. Do not put web URLs, API endpoints, or local filesystem paths here.

Default shape:

```markdown
## 文件引用

### 上游来源

- [[Source Note Title]]：This note supplied the setup, decision, source material, or prior version reused here.

### 相关主题

- [[Sibling Note Title]]：This note shares the same workflow family, tool family, project context, or reusable method.

### 后续可延展

- [[Future Note Title]]：This is a likely downstream note, index note, or broader synthesis that can reuse this note.
```

Selection rules:

- `上游来源`: use for notes that this note summarizes, updates, corrects, or depends on.
- `相关主题`: use for sibling notes with a real operational relationship, such as the same MCP/CLI/tooling family or the same project.
- `后续可延展`: use for higher-level synthesis, index, roadmap, or future workflow notes that should consume this note later.
- Do not force links. If a category has no meaningful note, write `- None captured`.
- Keep each link explanation short and action-oriented; one line per relationship is enough.

Mirror meaningful internal links in YAML `related_notes`, but keep the explanation in this section.

## Quality Checklist

Before writing or updating a note, verify:

- YAML metadata is complete and does not contain a `links` property.
- `related_notes` contains only note titles that are also explained in `## 文件引用`.
- `Key takeaway` has one strong reusable conclusion sentence and one practical explanation paragraph.
- `摘要` has exactly three scan-friendly bullets.
- `Context` orients the reader without repeating the whole note.
- User-provided WeChat or other platform URLs appear in `Context` and `Key references`.
- Business/project archive notes contain enough original substance that the reader does not need to reopen the source file for core content.
- `后续可复用关键信息` contains reusable facts, not generic caveats.
- `Key references` contains external evidence, local files, repo paths, user URLs, or API endpoints.
- `文件引用` contains internal Obsidian wiki links only.
- Secrets are excluded unless the user explicitly asks to include them.
- Chinese headings render correctly when read as UTF-8.
