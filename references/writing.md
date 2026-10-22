# Production document writing

The library must read as the project's own maintained technical documentation, written for engineers who maintain or integrate the system. This reference owns library layout, module and article ownership, presentation, and how evidence appears to readers. Design categories and functional decomposition belong to [design-outlines.md](design-outlines.md).

## Library layout

Write Chinese prose by default. Put official Markdown directly and flat in `docs/official/`. Use semantic Chinese filenames without ordering prefixes, dates, or revision labels, and keep them stable across ordinary updates. Module topics use `<module>-<topic>.md`; the label describes meaning, not a subdirectory. Keep actual product names and identifiers. Generate only pages the project actually supports.

`README.md` is the reader's entrypoint, grouped by reader purpose rather than source directories. The overall design is a separate required article. For a first build use `<project name>设计文档.md`; retain an existing compliant Chinese overall-design path when it serves the same purpose. Treat a misleading or noncompliant name as a managed rename, repairing current references under library-state.md.

Every design article has a plain Markdown link table of contents after its introduction/scope, covering all H2 chapters and useful functional H3 sections. Other long pages add one when it helps. Use ordinary links rather than `[TOC]`, theme components, or HTML layout. For lasting section references, add an explicit stable anchor such as `<a id="retry-policy"></a>` and verify it exists. Where an explicit anchor is unnecessary or unsupported, bind the whole article instead of guessing a renderer's slug.

Each article has one last-update date. Change it only when content or references change substantively. Run IDs, coverage counts, hashes, and verification timestamps live in `.cards/`. Link related reading where it helps the reader continue, without manufactured previous/next sequences.

## Outlines by document type

The overall design, every identified business module's main design, and every identified design topic's detailed article are required (see [module planning](#module-planning-and-content-ownership)). A module main design or principal flow article can be the detailed article for that same topic. Choose other document types and deeper topics by reader needs and evidence, including only sections with applicable facts.

Read [design-outlines.md](design-outlines.md) before planning or drafting any design article. Select its category and use the prescribed chapters and concrete functional-point decomposition. The overall design follows the seven chapters requested by the user; feature, architecture, module/mechanism, flow/state, data, API, configuration and deployment designs have their own outlines. Do not use the non-design progressions below to bypass design requirements.

| Non-design document type | Progression |
|---|---|
| Operation guide | Goal; applicable conditions and preparation; ordered actions; result checks; failure handling |
| Quick start | Expected outcome; minimum preparation; one complete supported experience; completion check; next reading |
| Configuration or API lookup reference | Scope; common rules; consistent entries; examples; constraints and errors |
| Troubleshooting | Symptom; evidence gathering; distinguish causes; supported treatment; recovery check |
| Glossary | Domain or concept groups; meaning; project context; boundaries and related reading |

Configuration entries give the actual name, type, default, allowed values, precedence, and activation timing as applicable; API entries give actual inputs, outputs, errors, and constraints. Leave a missing default as missing. Explain shared rules once. Keep mechanisms, such as the service startup flow, separate from human operations, such as starting a service.

### Minimum substance

Every article has an introduction and at least one substantive body section. A figure, a table, or a link list is never an article on its own.

| Document | Must cover at least |
|---|---|
| `README.md` | Title `<project name> 知识库`; introduction stating coverage and evidential basis; H2 groups by reader purpose, ordered as a reading path (not alphabetically), each link with a one-sentence description |
| Overall system design | Positioning and global architecture; a responsibility/dependency table; a substantive section for every design topic explaining its purpose, responsibilities/contracts, key mechanisms, relationships and constraints, linked to its detailed article; backbone interactions and global constraints |
| Module main design | Responsibility/boundary, actual external contracts and dependencies, internal components and main processing path; applicable detailed-design depth below; links to deeper topics |
| Detailed design / module topic | The applicable contracts, ordered mechanism, consequential branches, state/data effects, failures/recovery and worked cases below; its relation to the overall design and any module main article |
| Internal workflow | Trigger and entrypoint; participants; normal path; branches and failure handling |

A small module may be short when its actual contract is simple. A sentence naming a mechanism does not explain a complex mechanism. Keep missing necessary evidence pending rather than treating a placeholder, source link, or an unexplained label as completion.

### Detailed-design depth

Apply this to module main designs serving as details, module topics, and principal flow articles. Use the chosen category outline, organizing its subsections by actual functional points and mechanisms. Cover the applicable facts:

| Reader question | Required explanation |
|---|---|
| Where does it start? | Actual entrypoint, triggers, prerequisites, participants, and responsibility boundaries |
| What crosses the boundary? | Relevant signatures or input/output shapes, field meaning, units, defaults, precedence, validation and error semantics |
| How does it work? | Ordered steps, essential algorithms and the predicates that select consequential branches; what each branch produces or changes |
| What owns the state/data? | State transitions and invariants, mutation/publication points, lifetime, and applicable cache, persistence, concurrency or cancellation rules |
| What happens on failure? | Failure detection, partial results, retry/backoff, rollback or retention, recovery and terminal outcomes where implemented |
| How does a concrete case proceed? | For a complex mechanism, one source-grounded normal walkthrough and one consequential boundary/failure walkthrough, with intermediate decisions and final output/state |
| Why these constraints? | Source-supported design rationale, limitations, compatibility and design/implementation differences; do not infer historical motives from code |

Use [requirement-led explanation](design-outlines.md#requirement-led-explanation) to connect the need, goal and mechanism within that depth. Start a rule explanation with its supported purpose and relevant input contract; listing predicates alone does not explain the rule.

For missing fields, malformed inputs and parsing failures, explain the actual trigger, caller-visible result or error, retained/changed state, diagnostic retention and recovery where applicable. These are separate dimensions: an empty/error outcome may coexist with retained diagnostics. Follow the project's real distinctions instead of forcing every issue into “empty state / service error / diagnostic retention”; leave unknown behavior unknown and invent no retry, rollback or transaction guarantee.

Walkthroughs may use clearly labelled illustrative inputs derived from actual contracts. Identify them as static source-based reasoning unless executed; do not invent benchmark, network, or acceptance results. A simple lookup or field-only contract can be complete without artificial multi-step examples. Absent mechanisms do not need empty chapters.

Before calling an article complete, use its reader questions to trace a real mechanism from entry to output and its important alternative outcome using the prose. A reader should understand the ordering, decision conditions, data/state effects, and failure consequences without having to reconstruct them from source links. Follow linked principal explanations when they own a shared detail; do not leave a chain of summaries with the mechanism explained nowhere. Reject synopsis-only details, interface-name catalogues, unexplained tables, code dumps, repeated overall background, or filler added to meet a word count. Judge substance and correctness, not length.

Assess each design article's figures under diagrams.md. An overall figure does not replace a needed internal flow, interaction, state or data explanation. Keep reader-question/answer and figure assessments in the working plan under library-state.md; these review notes stay out of reader prose.

## Module planning and content ownership

Identify business modules from supported responsibilities, contracts, entrypoints, calls, and original domain declarations. A directory, class, or helper function alone does not establish a business module, and one responsibility can span several source directories. Describe technical components where relevant without inventing business boundaries.

Review module recognition against the declared source scope before judging document coverage, keeping unresolved boundaries and unread sources visible. For each identified module, carry a plan with its name, responsibility, original sources, main-article path, required topic paths, and unfinished work. Reuse existing stable article paths when the same concept continues.

Identify design topics alongside modules from original design declarations, responsibilities, contracts, state ownership, and actual entrypoints. A design topic is a coherent design concern with its own behavior or rules; it may belong to one module or cross modules. Distinct concerns such as dashboard interaction and settings calibration keep separate detailed articles even when they share a platform. Individual fields, helpers, and minor constraints remain within their owning topic. Do not replace topic recognition with a list of platforms, directories, or existing articles.

Map each design topic to its original sources, one explicit stable section anchor in the overall design, and its detailed article. The overall section must explain the design sufficiently to understand the whole system before reading details; a title, short label, diagram, or link alone is insufficient. The detailed article expands contracts, algorithms, states, and failures and links back to that overall section. A module main design or principal cross-module flow may fulfill the same topic's detail role without a duplicate article; distinct complete topics cannot all be assigned to a generic platform overview. Retain this plan under library-state.md.

| Article | Owns |
|---|---|
| Overall system design | The complete system-level explanation of every design topic and its relationships, plus boundaries, module responsibilities/dependencies, backbone scenarios, shared state and global constraints; stable sections link to corresponding detailed designs |
| Module main design | The whole-module explanation, for every module including small ones. Small modules stay in their own article, short but complete; complex modules move deep detail to topic articles |
| Module topic | One focused mechanism, flow, state rule, or contract detail |
| Cross-module flow | The one principal explanation of a complex flow: complete interactions, branches, failures, and recovery. Participating modules explain their own part and link here; brief contextual summaries elsewhere are fine, competing complete explanations are not |

Plan the overall article and its topic sections before drafting details; finalize those sections and relationships after detailed reading. Check topic recognition against original sources, then check every topic's overall section and detailed article, separately from each module's article set. File existence and valid links alone do not establish substantive coverage. When a batch cannot finish, retain the plan and pending work as described in [library-state.md](library-state.md). A plan change needs an evidence-based reason; an unfinished overall design, module, or design topic stays pending until done.

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

The following shared skeleton illustrates a non-design article. Design articles insert the linked contents and use their category chapters, ending in `参考文献` instead of a separate `相关文档` chapter:

```markdown
# <title matching the filename topic>

<introduction: 1–3 sentences stating the question answered and the key conclusion>

<scope or prerequisites, only when they affect conclusions>

## <body sections; numbered chapters for designs>

依据：[`tasks/dispatcher.py`](../../tasks/dispatcher.py) 的 `dispatch()`；[原项目说明](../../domain.md)。

## 相关文档

- [任务分派流程](任务分派流程.md)：完整的跨模块交互与失败处理。

最后更新：YYYY-MM-DD
```

Use one H1 per page, describing the same topic as the filename. Use continuous heading levels, usually H2 and H3, without icons. Design body chapters use consecutive numbers (`## 1. 目标`, `### 2.1 <functional point>`), while H1, filenames and the `## 目录` label remain unnumbered. Other article types default to unnumbered headings. Keep stable explicit anchors independent of visible chapter numbers. Concept headings name the concept (“配置优先级”); task headings use an action (“启动服务”).

| Purpose | Only allowed form |
|---|---|
| Section source note | A separate paragraph starting `依据：` at the end of the section it supports. Link text is the path or document title; symbols follow in inline code |
| Supplementary note / risk | `> **说明**：` / `> **注意**：` |
| Further reading | Non-design pages use final `## 相关文档`; designs place an optional numbered H3 `相关文档` inside the final `参考文献` chapter. Each link carries one descriptive clause |
| Update date | The last line of the page: `最后更新：YYYY-MM-DD` |
| Figure | Lead-in sentence → image with meaningful alt text → caption line `图：<figure title>。<scope>` → prose interpreting the key points. The H1 never comes from a figure title |

### Design page layout

Use the category outline as the body of the page skeleton above. A design page starts with one H1, a short introduction/scope and a linked contents list. Use H2 chapters and named H3 functional/mechanism sections; avoid deep heading ladders. Keep an inventory table compact (point, behavior summary, precise detail link); put rules, steps and failure explanations in prose below it, not paragraphs inside wide cells. Separate tables, lists and fenced blocks with blank lines and label code fences. Place a figure next to its relevant explanation, with the standard lead-in, meaningful alt text, caption and interpretation. Split an unreadably dense view by semantic scope and explain how the views connect; shrinking text or adding tiny whole-system images is not a repair. Inspect the rendered design page for hierarchy, table width, image legibility, spacing and usable contents/anchors in the actual preview environment.

### Prose and Markdown elements

State the conclusion or relationship early, then reasons, boundaries, and exceptions. Draft source-supported actions, objects and applicable results; after the content check, apply the [sentence construction rules](technical-editing.md#sentence-construction) in the independent expression-editing pass. Keep one term for one concept. Expand an abbreviation only when the expansion is supported.

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

Choose table columns from genuinely comparable facts; a provider/input/result/boundary table is only one possible form. Explain causal or ordered branches in prose, ordered steps or a figure under diagrams.md, rather than packing them into long cells. A diagram placeholder is unfinished work, not a formal figure.

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

These are blocking presentation defects: noncompliant article filenames, an H1 that does not match the filename topic, generation-process narration in reader prose, a figure-, table-, or link-only article, and an unannotated flat `README.md` list. Missing overall design, missing topic sections/details or functional points, and an architecture-summary-only overall article are blocking coverage defects. Design category/outline omissions and unreadable required figures or tables are blocking presentation defects; apply the current outline/layout checks before reusing an older design, repairing only affected structure, prose, links and rendering. The collection check repairs them through the normal update lifecycle; they cannot take the no-change shortcut. Other typography differences converge only when a passage is edited for content reasons. A presentation-only repair that does not change meaning keeps the article's last-update date; substantive content or reference changes follow the normal date rule.

## Evidence for readers

Explain behavior first, then add the `依据：` note for that group of claims. Cite original project paths, symbols, explicit document anchors, or consulted authoritative URLs, and make the support relationship clear; a bare source list is not enough.

Markdown links are relative to the current article, so a link from an official page to a root-level source needs the matching relative path. A card's `sources.path` is project-root relative; keep the two bases apart. Line numbers help navigation but are not identities.

Present historical design motives only from existing design or decision records, never inferred from current code. Keep relevant uncertainty and disagreements next to the claim. Unread material is not evidence of absence. Missing information gets a concrete reason and effect, not empty chapters or repeated placeholders.

Keep repeated explanations focused on the page's context and link to the principal explanation. Present terminology naturally in a glossary, without JSON management fields. Before delivery, check names, shared contracts, sources, and card meanings across pages.
