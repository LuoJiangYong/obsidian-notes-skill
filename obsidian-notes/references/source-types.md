# Obsidian Source Types

Use this reference when the source material is not just the current conversation. Preserve source identity in `Key references`; use `文件引用` only for Obsidian internal note relationships.

## Source Handling Rules

### WeChat Article

Use for 微信推文, 公众号文章, saved HTML, screenshots, or copied article text.

Capture:

- title, account/publication name, author when available
- publish date and access/save date
- original URL or exported local file path
- key claims, examples, data, quoted framework, and reusable method
- access limitations if the page could not be fully retrieved

`Key references` should include the article URL or local export path. Do not over-quote; summarize and keep short excerpts only when necessary.

### URL / Web Page

Use for ordinary web pages, docs, blog posts, product pages, and online reports.

Capture:

- page title, publisher, author when available
- publish/update date and access date
- exact URL
- factual claims versus interpretation
- sections used, especially for long pages

When current accuracy matters, verify the URL live before writing.

### PDF

Use for reports, white papers, scanned documents, brochures, and exported slides.

Capture:

- local path or source URL
- filename, page count when known, page ranges used
- section/page references for important data
- chart/table names and data caveats
- OCR limitations when applicable

`Key references` should include page numbers or page ranges for important claims.

### DOCX

Use for Word documents, drafts, proposals, plans, summaries, and meeting documents.

Capture:

- local path, filename, version/date when available
- heading structure and sections used
- comments/revisions if relevant
- core decisions, action items, reusable language, and unresolved issues

Preserve document version context when the file may have multiple drafts.

### EXCEL / Spreadsheet

Use for Excel workbooks, CSV files, tables, KPI exports, and operational datasets.

Capture:

- local path, workbook name, sheet names used
- time range, rows/columns, field definitions, metric formulas
- filters, pivots, aggregation choices, and data limitations
- key tables or summaries instead of dumping whole sheets

Important: state metric definitions and denominator assumptions. Do not turn raw tables into generic prose without preserving the data grain.

### PPTX / Slides

Use for presentations, work reports, strategy decks, training decks, and event proposals.

Capture:

- local path, deck name, slide count when known
- slide numbers or section titles used
- main storyline, claims, data charts, examples, and decisions
- visual assets or diagrams that should be retained

PPTX often contains high-level argument structure; preserve the storyline before extracting details.

### Existing Obsidian Note

Use when updating, summarizing, splitting, or synthesizing notes already in the vault.

Capture:

- original note title and path
- whether the new note summarizes, corrects, extends, or indexes the original
- wiki links in `文件引用`
- local path in `Key references` only when useful for Agent migration

### Conversation

Use when the current chat is the primary source.

Capture:

- user intent, decisions made, tools run, files changed, validation status
- exact paths, commands, endpoints, and constraints when relevant
- unresolved next actions

## Confidence Guidance

- `high`: source was read directly in this run, or output was written and read back.
- `medium`: source came from conversation context, memory-derived facts, or partial file inspection.
- `low`: source was incomplete, inaccessible, OCR-limited, or not verified.

## Key References by Source

| Source | Required references |
|---|---|
| WeChat article | URL or local export, account name, publish/access date when known |
| URL | URL, title/publisher, access date |
| PDF | path or URL, page range, filename |
| DOCX | path, filename/version, sections used |
| EXCEL | path, workbook, sheet names, metric definitions |
| PPTX | path, deck name, slide numbers or section titles |
| Existing Obsidian note | wiki link in `文件引用`, optional path in `Key references` |
| Conversation | no invented reference; include local files or tool outputs only when they exist |
