# obsidian-notes-skill · 把对话、网页与资料沉淀为长期可用的 Obsidian 笔记

![Agent Skill](https://img.shields.io/badge/Agent-Skill-111111)
![Obsidian](https://img.shields.io/badge/For-Obsidian-483699)
![lang](https://img.shields.io/badge/lang-zh--CN-blue)

把对话、项目资料、会议记录、网页、微信文章等各类材料发给 AI，即可整理成**结构化、长期可用**的 Obsidian 知识库笔记。为 AI Agent（Codex、Hermes 等）设计的技能：统一笔记结构（Properties / Key takeaway / 摘要 / 引用边界）、内容完整性要求与质量检查，并与官方 Obsidian 技能声明协作分工。

Send anything to your AI — conversations, project materials, meeting notes, web pages, WeChat articles, and more — and get structured, long-lived Obsidian notes back. A skill for AI agents (Codex, Hermes, and more) with a consistent note schema, completeness requirements, quality checks, and collaboration boundaries with the official Obsidian skills.

## 这是什么

- 一个 **AI Agent 技能**（`SKILL.md` 格式）：放入 Agent 的技能目录即可使用，适用于任何支持该机制的助手。
- **发什么整理什么**：对话、网页与微信文章、各类文档（PDF / DOCX / EXCEL / PPTX）、会议记录——发给 AI 即可整理入库。
- 解决的问题：AI 写进知识库的笔记**结构漂移、内容空心化**（只有指针和摘要卡片）、引用混乱。
- 核心承诺：笔记在数周后仍然**可搜索、可阅读、可复用**；工作项目笔记的正文必须足够完整，让读者不需要重新打开原始文件。
- 源自真实知识库（Obsidian vault）的日常使用与迭代（2026-06 起）。

## 核心能力

- **结构契约**：统一 YAML Properties（`created_at` / `updated_at` / `source` / `note_type` / `knowledge_type` / `status` / `confidence` / `related_notes` / `tags` 等），固定 `Key takeaway` / `摘要` / `Context` 三段 callout 结构。
- **五类笔记类型**：`agent-workflow`（Agent 工作流）、`project-note`（项目资料）、`technical-note`（技术排障）、`decision-record`（决策记录）、`reference-note`（长期参考）。
- **内容完整性**：工作项目归档笔记必须保留叙事主线、事实、数据、机制、案例与可复制启示；页码与截图只是证据，不能替代正文。
- **引用边界**：`Key references`（外部证据、URL、文件路径、端点）与 `文件引用`（Obsidian 内部 wiki 链接）严格分离。
- **来源处理规则**：微信文章、URL、PDF、DOCX、EXCEL、PPTX、本地文件、会议记录、已有笔记的处理标准。
- **业务领域模板**：社群与会员运营、营销策划、商业运营、品牌活动、线上产品开发、案例研究、MOC / 索引类笔记。
- **质量检查与读回验证**：写入前逐项质检；优先通过 Obsidian MCP 写入并读回验证标题、Properties 与关键章节。

## 与官方 Obsidian 技能的协作边界

本 skill 是笔记**结构的权威**；其它技能只补充语法、格式、提取或渲染能力，不得反向改变结构规范。下表六个协作对象均来自 Obsidian 官方技能仓库 [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills)，点击可跳转查看各技能的完整说明：

| 技能 | 分工边界 |
|---|---|
| `obsidian-markdown` | Obsidian 特有 Markdown 语法（embeds、LaTeX、Mermaid、脚注等） |
| `obsidian-bases` | `.base` 视图文件 |
| `json-canvas` | `.canvas` 图谱文件 |
| `obsidian-cli` | 插件调试、截图验证、DOM / console 检查等命令行能力 |
| `defuddle` | 网页正文提取：普通 URL 优先用它取正文，再消化整理 |
| `knap` | 数据 → Markdown 渲染（JSON/CSV、批量生成）；渲染产物视为初稿，须经质检后入库 |

## 仓库结构

```text
obsidian-notes-skill/
└── obsidian-notes/
    ├── SKILL.md                       # 主技能：核心流程 / 必需结构 / 写作规则 / 质量检查 / 协作边界
    ├── agents/
    │   └── openai.yaml                # Agent 接口配置（显示名 / 描述 / 默认提示词）
    └── references/
        ├── note-template.md           # 默认笔记模板（Properties、callout、章节骨架）
        ├── note-types.md              # 业务领域模板（社群运营、营销策划、案例研究等）
        ├── source-types.md            # 来源处理规则（微信、URL、PDF、文档表格、会议记录等）
        └── style-guide.md             # 样式与内容密度规范
```

## 安装与使用

1. 将 `obsidian-notes/` 目录放入你的 Agent 技能目录，例如：
   - Codex：`~/.codex/skills/`
   - Hermes：`~/AppData/Local/hermes/skills/`
   - 其它支持 `SKILL.md` 机制的 Agent 按各自技能目录约定放置。
2. 让 Agent 执行笔记任务，例如：「把这次对话整理成 Obsidian 笔记」「把这份会议记录沉淀到知识库」。
3. 可选搭配：
   - **Obsidian MCP / Local REST API**：直接写入 vault 并读回验证；不可用时 Agent 输出 Markdown 供手动写入。
   - **defuddle / knap**：网页提取与批量渲染场景可搭配使用（见上方协作边界）。

## 设计原则

- **结构权威单一**：笔记结构、Properties、质量与引用边界只由本 skill 定义。
- **完整优先**：拒绝指针笔记与摘要卡片，正文自足是硬标准。
- **边界分离**：外部证据进 `Key references`，内部关系进 `文件引用`。
- **稳定标签**：`tags` 只放稳定主题分类，不放类型、年份、状态。
- **能力委托**：提取、渲染、视图、调试等能力委托官方技能；产物一律经过本 skill 质量检查后再入库。

## License

本项目采用 [MIT License](LICENSE)（© 2026 Jiang Yong Luo）。
