# Production document writing

The library must read as the project's own maintained technical documentation, written for engineers who maintain or integrate the system. This reference owns library layout, outlines, module and article ownership, presentation, and how evidence appears to readers.

## Library layout

Write Chinese prose by default. Put official Markdown directly and flat in `docs/official/`. Use semantic Chinese filenames without ordering prefixes, dates, or revision labels, and keep them stable across ordinary updates. Module topics use `<module>-<topic>.md`; the label describes meaning, not a subdirectory. Keep actual product names and identifiers. Generate only pages the project actually supports.

`README.md` is the reader's entrypoint, grouped by reader purpose rather than source directories.

For long pages, add a plain Markdown link table of contents when it helps; use ordinary links rather than `[TOC]`, theme components, or HTML layout. For lasting section references, add an explicit stable anchor such as `<a id="retry-policy"></a>` and verify it exists. Where an explicit anchor is unnecessary or unsupported, bind the whole article instead of guessing a renderer's slug.

Each article has one last-update date. Change it only when content or references change substantively. Run IDs, coverage counts, hashes, and verification timestamps live in `.cards/`. Link related reading where it helps the reader continue, without manufactured previous/next sequences.

## Outlines by document type

Every identified business module gets an independent main design (see [module planning](#module-planning-and-content-ownership)). Choose all other document types and topic articles by actual reader needs and evidence, and include only sections with applicable facts.

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

Configuration entries give the actual name, type, default, allowed values, precedence, and activation timing as applicable; API entries give actual inputs, outputs, errors, and constraints. Leave a missing default as missing. Explain shared rules once. Keep mechanisms, such as the service startup flow, separate from human operations, such as starting a service.

### Minimum substance

Every article has an introduction and at least one substantive body section. A figure, a table, or a link list is never an article on its own.

| Document | Must cover at least |
|---|---|
| `README.md` | Title `<project name> 知识库`; introduction stating coverage and evidential basis; H2 groups by reader purpose, ordered as a reading path (not alphabetically), each link with a one-sentence description |
| Overall system design | A positioning paragraph; a module table with responsibility, dependencies, and main-article link; continuous prose on backbone interactions; global constraints |
| Module main design | Responsibility and boundary, including what it does not do; public interface with actual signatures or inputs and outputs; main processing path; error and edge behavior; dependencies; links to topics |
| Internal workflow | Trigger and entrypoint; participants; normal path; branches and failure handling |

A small module may be short, but each applicable point gets at least one sentence. When a point cannot be established, say so once with the reason instead of creating an empty section.

## Module planning and content ownership

Identify business modules from supported responsibilities, contracts, entrypoints, calls, and original domain declarations. A directory, class, or helper function alone does not establish a business module, and one responsibility can span several source directories. Describe technical components where relevant without inventing business boundaries.

Review module recognition against the declared source scope before judging document coverage, keeping unresolved boundaries and unread sources visible. For each identified module, carry a plan with its name, responsibility, original sources, main-article path, required topic paths, and unfinished work. Reuse existing stable article paths when the same concept continues.

| Article | Owns |
|---|---|
| Overall system design | A concise table linking every module to its main design; system boundaries, major relationships, backbone scenarios, shared state responsibility, and global constraints. It is more than a link catalog |
| Module main design | The whole-module explanation, for every module including small ones. Small modules stay in their own article, short but complete; complex modules move deep detail to topic articles |
| Module topic | One focused mechanism, flow, state rule, or contract detail |
| Cross-module flow | The one principal explanation of a complex flow: complete interactions, branches, failures, and recovery. Participating modules explain their own part and link here; brief contextual summaries elsewhere are fine, competing complete explanations are not |

Complete detailed reading before backfilling the final overall summaries and relationships. Check a module's main design and required topics as a set; a main file's existence does not show understanding or completion. When a batch cannot finish, retain the plan and pending work as described in [library-state.md](library-state.md). A plan change needs an evidence-based reason; a pending module or required topic stays pending until it is done.

## Presentation

These rules govern what readers see. They sit on top of the evidence rules and never relax them.

### Register

Describe current behavior in neutral declarative sentences. Write operation steps as direct imperatives. Leave out first person (“我们”), exclamation marks, rhetorical questions, promotional adjectives, intensifiers, and emoji.

Keep the generation process out of reader prose. Words such as “本轮”, “本次生成”, “经分析”, “未读取到”, “已核对”, run IDs, check results, and mentions of samples or drills belong in `.cards/` and the run report.

### Evidence status, stated once

State the library's evidential basis once in the `README.md` introduction. Repeat it in an article only when it changes that article's conclusions, and then once in its introduction or scope.

In body text, state facts in domain terms. When the source scope that would contain a mechanism was fully read, state the absence directly; when it was not, give the scope and reason at that claim. Put claim-specific uncertainty at the claim, once.

| Avoid | Write |
|---|---|
| 是否得到预期结果尚未通过运行程序验证。……本轮仅审阅静态实现，没有执行程序或目标环境验收。 | `README.md` 导语：本知识库依据当前源码与原项目文档编写，描述静态实现，不包含运行实测数据。正文：`runner.main()` 显式传入 `enabled=True` 调用 `jobs.run_job()`。 |
| 没有读取到持久化、后台线程或重试间隔机制。 | 当前实现为同步调用，不提供持久化、后台线程或重试间隔。 |

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

Use one H1 per page, describing the same topic as the filename. Use continuous heading levels, usually H2 and H3, without section numbers or icons. Concept headings name the concept (“配置优先级”); task headings use an action (“启动服务”).

| Purpose | Only allowed form |
|---|---|
| Section source note | A separate paragraph starting `依据：` at the end of the section it supports. Link text is the path or document title; symbols follow in inline code |
| Supplementary note / risk | `> **说明**：` / `> **注意**：` |
| Further reading | Final `## 相关文档` section; each link carries one descriptive clause |
| Update date | The last line of the page: `最后更新：YYYY-MM-DD` |
| Figure | Lead-in sentence → image with meaningful alt text → caption line `图：<figure title>。<scope>` → prose interpreting the key points. The H1 never comes from a figure title |

### Prose and Markdown elements

State the conclusion or relationship early, then reasons, boundaries, and exceptions. Use concrete actors and direct verbs. Keep one term for one concept. Expand an abbreviation only when the expansion is supported.

| Element | Use |
|---|---|
| Paragraph | Connected explanation of responsibility, causality, or boundary |
| Unordered list | Parallel roles, conditions, or independent notes |
| Ordered list | Actions whose order matters; include position and checks when needed |
| Table | Comparable parameters, fields, or conditions; long prose goes outside cells |
| Fenced block | Actual code, commands, configuration, or output; label the language and explain context |
| Inline code | Identifiers, paths, arguments, and enumerations |
| Labelled quote | A useful note or concrete risk; prerequisites go before the affected action |
| Figure | Relationships, sequences, or states that become clearer visually |

Ground commands in actual project entrypoints or original operating instructions. Explain placeholders and keep real secrets out of them. Label expected output as expected; observed output needs an actual run and its environment. Writing instructions does not authorize running the project's services, deployment, tests, or external operations.

Figures follow [diagrams.md](diagrams.md) for necessity and checks. Official figures are static SVG referenced with normal Markdown image syntax; key explanations stay in prose. Mermaid found in original materials is a declaration, not proof of current implementation. Keep one active graph source per figure and no website dependency.

### Chinese typography and terminology

- Use full-width punctuation in Chinese sentences and “” for quotation marks. Keep half-width characters inside English, code, and numbers.
- Put a half-width space between Chinese and English words, digits, or inline code, except next to full-width punctuation.
- Introduce a term as 任务调度器（`Dispatcher`） on first mention, then use one name throughout the page. Use the bare identifier when no natural Chinese name exists instead of coining a translation.
- Keep list items grammatically parallel: complete sentences end with “。”, fragments take no terminal punctuation, and one list does not mix the two.
- Headings carry no terminal punctuation or colons. Prefer specific headings to generic ones such as “其它”, “相关内容”, or “说明”.
- In tables write “—” for not applicable and “未声明” for missing information, so no cell is empty. Put units in the header.

### Bringing existing libraries into line

These are blocking presentation defects: an H1 that does not match the filename topic, generation-process narration in reader prose, a figure-, table-, or link-only article, and an unannotated flat `README.md` list. The collection check repairs them through the normal update lifecycle; they cannot take the no-change shortcut. Other typography differences converge only when a passage is edited for content reasons. A presentation-only repair that does not change meaning keeps the article's last-update date.

## Evidence for readers

Explain behavior first, then add the `依据：` note for that group of claims. Cite original project paths, symbols, explicit document anchors, or consulted authoritative URLs, and make the support relationship clear; a bare source list is not enough.

Markdown links are relative to the current article, so a link from an official page to a root-level source needs the matching relative path. A card's `sources.path` is project-root relative; keep the two bases apart. Line numbers help navigation but are not identities.

Present historical design motives only from existing design or decision records, never inferred from current code. Keep relevant uncertainty and disagreements next to the claim. Unread material is not evidence of absence. Missing information gets a concrete reason and effect, not empty chapters or repeated placeholders.

Keep repeated explanations focused on the page's context and link to the principal explanation. Present terminology naturally in a glossary, without JSON management fields. Before delivery, check names, shared contracts, sources, and card meanings across pages.
