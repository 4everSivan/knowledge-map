# Production document writing

## Library and page form

Write Chinese prose by default. Put official Markdown directly in `docs/official/`. Use semantic Chinese filenames without ordering prefixes, dates, or revision labels. Keep actual product names and identifiers. `README.md` is the navigation exception; use it as the reader's entrypoint, grouped by actual reader tasks rather than source directories. Generate only applicable pages.

Use one H1 per page, followed by a short introduction and any scope that affects understanding. Use continuous heading levels, usually H2 and H3, without section numbers or decorative icons. The H1 and filename must describe the same topic. Task headings use actions; concept headings name the concept. Keep stable filenames across ordinary updates.

Use a normal Markdown link table of contents for long pages when useful. Do not use `[TOC]`, theme-specific components, or HTML layout. For lasting section references use an explicit stable anchor, such as `<a id="retry-policy"></a>`, and verify it exists. If an explicit anchor is unnecessary or unsupported, bind the whole article rather than guessing a renderer's slug.

Keep one meaningful last-update date per article. Change it only when content or references change substantively, not whenever a scan runs. Keep run IDs, coverage counts, hashes, and verification timestamps in `.cards/`. Link related reading when it helps the reader continue; do not manufacture previous/next sequences.

## Choose and trim an outline

Every identified business module requires an independent main design article, including a small module. Other document types and deeper topic articles are chosen for actual reader needs and evidence; do not create empty chapter templates. The module obligation cannot be waived by treating all document types as optional.

| Document type | Suggested progression |
|---|---|
| Overall system design | Purpose; boundaries; global structure; module responsibility and dependency summaries with main-article links; backbone interactions; shared state and global constraints |
| Module main design | Responsibilities and limits; external contracts and dependencies; internal structure; overall mechanisms; failures and constraints; links to deeper topics |
| Module topic | One complex mechanism, long flow, state rule, or extensive contract detail with its evidence and connection to the main design |
| Internal workflow | Entrypoint and trigger; participants; normal path; branches and states; errors, shutdown, and recovery |
| Operation guide | Goal; applicable conditions and preparation; ordered actions; result checks; failure handling |
| Quick start | Expected outcome; minimum preparation; one complete supported experience; completion check; next reading |
| Configuration or API reference | Scope; common rules; consistent entries; examples; constraints and errors |
| Troubleshooting | Symptom; evidence gathering; distinguish causes; supported treatment; recovery check |
| Glossary | Domain or concept groups; meaning; project context; boundaries and related reading |

Configuration entries describe actual name, type, default, allowed values, precedence, and activation timing as applicable. API entries describe actual inputs, outputs, errors, and constraints. Do not invent missing defaults. Explain shared rules once. Separate mechanisms such as service startup flow from human operations such as starting a service.

## Module planning and content ownership

Identify business modules from supported responsibilities, contracts, entrypoints, calls, and original domain declarations. A directory, class, or helper function does not by itself establish a business module. One responsibility can span several source directories. Describe technical components where relevant without inventing business boundaries.

Review module recognition against the declared source scope before judging document coverage. Keep unresolved boundaries and unread sources visible. For each identified business module, carry a plan with its name, responsibility, original sources, main-article path, required topic paths, and unfinished work. Use existing stable article paths when the same concept continues.

The overall design keeps a concise table linking every identified business module to its independent main design. Retain system boundaries, major relationships, backbone scenarios, shared state responsibility, and global constraints. Move module internals to their appropriate module articles without reducing the overall design to a bare link catalog.

Each main design must explain the module as a whole, not merely list topic links. Small modules can have short explanations that still meet the minimum substance below; do not merge them into the overall design or another module, and do not pad them with empty sections. For a complex module, keep the whole-module explanation in the main design and put deep details in focused topic articles.

Give a complex cross-module flow one principal article describing its complete interactions, branches, failures, and recovery. The overall design retains the backbone and global constraints. Each participating module explains its own responsibility and links to the principal flow rather than duplicating the entire sequence. Brief contextual summaries may repeat; do not maintain competing complete explanations.

Keep all official Markdown flat under `docs/official/`. Use semantic names for main articles and `<module>-<topic>.md` for module topics; these labels describe meaning, not additional subdirectories. Complete detailed reading before backfilling the final overall summaries and relationships.

Check a module's main design and required topics as a set. A main file's existence does not establish source understanding or completion. Retain the plan and pending work according to [library-state.md](library-state.md) when a batch cannot finish. Changing the plan requires an evidence-based explanation; do not drop a pending module or required topic to manufacture complete coverage.

## Prose and Markdown elements

State the needed conclusion or relationship early, then explain reasons, boundaries, and exceptions. Use concrete actors and direct verbs. Keep terms consistent instead of varying technical synonyms. Explain abbreviations only when the expansion is supported.

| Element | Use |
|---|---|
| Paragraph | Connected explanation of responsibility, causality, or boundary |
| Unordered list | Parallel roles, conditions, or independent notes |
| Ordered list | Actions whose order matters; include position and checks when needed |
| Table | Comparable parameters, fields, or conditions; move long prose outside cells |
| Fenced block | Actual code, commands, configuration, or output; label the language and explain context |
| Inline code | Identifiers, paths, arguments, and enumerations |
| Quote with a label | A useful note or concrete risk; put prerequisites before the affected action |
| Diagram | Relationships, sequences, or states that become clearer visually |

Keep commands grounded in actual project entrypoints or original operating instructions. Explain placeholders and never fill them with real secrets. Label expected output as expected; observed output requires an actual run and its environment. Writing instructions does not authorize running the project's service, deployment, tests, or external operations.

Apply the evidence-grounded required triggers and optional choices in [diagrams.md](diagrams.md). Official generated engineering figures are static SVG referenced with normal Markdown image syntax, meaningful alt text and the `图：` caption defined under [figure presentation](#professional-presentation); keep key explanations in prose. Mermaid already present in original materials may be read as declarations, not automatically treated as current implementation. Do not maintain duplicate active graph sources for the same figure or require a website.

## Professional presentation

The library must read as the project's own maintained technical documentation, written for engineers who maintain or integrate the system. These rules govern what readers see; they do not relax the evidence rules below.

### Register

Describe current behavior in neutral declarative sentences. Do not use first person (“我们”); write operation steps as direct imperatives. Do not use exclamation marks, rhetorical questions, promotional adjectives, intensifiers, or emoji.

Never narrate the generation process in reader prose. Words such as “本轮”, “本次生成”, “经分析”, “未读取到”, “已核对”, run IDs, check results, and references to samples or drills belong in `.cards/` and the run report, not in `docs/official/`.

### Evidence status, stated once

State the library's evidential basis once in the `README.md` introduction, for example “本知识库依据当前源码与原项目文档编写，不包含运行实测数据。”. Repeat it in an article only when it changes that article's conclusions, and then once in the introduction or scope.

In body text, state facts in domain terms. When the source scope that would contain a mechanism was fully read, write “当前实现不提供持久化”, not “没有读取到持久化”. When it was not fully read, give the scope and reason at that claim. Put claim-specific uncertainty at the claim once; do not end paragraphs with repeated “未经运行验证” disclaimers.

### Page skeleton and fixed labels

Every article follows this skeleton, omitting parts that do not apply:

```markdown
# <title matching the filename topic>

<introduction: 1–3 sentences stating the question answered and the key conclusion>

<scope or prerequisites, only when they affect conclusions>

## <body sections>

依据：[`tasks/dispatcher.py`](../../tasks/dispatcher.py) 的 `dispatch()`；[原项目说明](../../domain.md)。

## 相关文档

- [任务分派流程](任务分派流程.md)：完整的跨模块交互与失败处理。

最后更新：YYYY-MM-DD
```

| Purpose | Only allowed form |
|---|---|
| Section source note | A separate paragraph starting `依据：` at the end of the section it supports. Link text is the path or document title; symbols follow in inline code. Never `来源：` or `实现依据：` |
| Supplementary note / risk | `> **说明**：` / `> **注意**：`; no other callout labels |
| Further reading | Final `## 相关文档` section; each link carries one descriptive clause |
| Update date | The last line of the page: `最后更新：YYYY-MM-DD` |
| Figure | Lead-in sentence → image → caption line `图：<figure title>。<scope>` → prose interpreting the key points. The H1 never comes from a figure title |

### Minimum substance

Every article has an introduction and at least one substantive body section. A figure, a table, or a link list never constitutes an article on its own.

| Document | Must cover at least |
|---|---|
| `README.md` | Title `<project name> 知识库`; introduction stating coverage and evidential basis; H2 groups by reader purpose, ordered as a reading path (not alphabetically), each link with a one-sentence description |
| Overall system design | A positioning paragraph; a module table with responsibility, dependencies, and main-article link; continuous prose on backbone interactions; global constraints |
| Module main design | Responsibility and boundary, including what it does not do; public interface with actual signatures or inputs and outputs; main processing path; error and edge behavior; dependencies; links to topics |
| Internal workflow | Trigger and entrypoint; participants; normal path; branches and failure handling |

A small module may be short, but each applicable point gets at least one sentence. When a point cannot be established, say so once with the reason; do not create an empty section.

### Chinese typography and terminology

- Use full-width punctuation in Chinese sentences and “” for quotation marks. Keep half-width characters inside English, code, and numbers.
- Put a half-width space between Chinese and English words, digits, or inline code, except next to full-width punctuation.
- Introduce a term as 任务调度器（`Dispatcher`） on first mention, then use one name throughout the page. Use the bare identifier when no natural Chinese name exists; never coin a translation.
- Keep list items grammatically parallel: complete sentences end with “。”, fragments take no terminal punctuation; do not mix them in one list.
- Headings carry no terminal punctuation or colons. Avoid generic headings such as “其它”, “相关内容”, or “说明”.
- In tables write “—” for not applicable and “未声明” for missing information; never leave a cell empty. Put units in the header.

### Bringing existing libraries into line

These are blocking presentation defects: an H1 that does not match the filename topic, generation-process narration in reader prose, a figure-, table-, or link-only article, and an unannotated flat `README.md` list. The collection check repairs them through the normal update lifecycle; they cannot take the no-change shortcut. Other typography differences converge only when a passage is edited for content reasons; do not rewrite unrelated passages for consistency. A presentation-only repair that does not change meaning keeps the article's last-update date.

## Evidence and limitations

Explain behavior first, then add short `依据：` notes near the supported group of claims. Use original project paths, symbols, explicit document anchors, or consulted authoritative URLs. A source list without a support relationship is insufficient.

Markdown links are relative to the current article. A link from an official page to a root-level source therefore needs the corresponding relative path, whereas a card's `sources.path` is project-root relative. Do not mix these bases. Line numbers aid current navigation but are not identities.

Distinguish static implementation, original document declarations, inference, runtime observations, and human acceptance. Never infer historical design motives from current code. Preserve relevant uncertainty and disagreements near the claim. Unread material is not evidence of absence. Missing information should have a concrete reason and effect, not empty chapters or repeated placeholders.

Keep repeated explanations focused on the page's context and link to the principal explanation. Render terminology naturally in a glossary rather than exposing JSON management fields. Check names, shared contracts, sources, and card meanings across pages before official delivery.
