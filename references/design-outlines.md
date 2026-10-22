# Design document outlines

Read this when planning, drafting or reviewing design articles. This reference owns design categories, their chapter contracts and functional decomposition. [writing.md](writing.md) owns presentation and evidence formatting; [diagrams.md](diagrams.md) owns figure necessity and validation.

## Choose the category

Select by the article's main question, not its filename suffix or source directory. Use the overall outline for the required system design. Use feature design for an observable capability, architecture design for a substantial system structure/decision concern, module design for an implementation responsibility or internal mechanism, and a specialized outline for a principal flow, data, API, configuration or deployment concern. Record the choice in the document plan. A module's main article may serve the same feature/topic without a duplicate file. A technical topic still chooses an applicable category; “topic” is not an outline exemption.

Only generate categories supported by the project. A template does not require a separate file. Operation guides, quick starts, lookup references, troubleshooting, navigation and glossaries retain the reader-oriented progressions in writing.md; a reference is not an API/configuration design merely because it lists fields.

Use the Chinese H2 titles below in the stated order for default Chinese output, numbered `## 1. 简介`, etc. Translate the titles consistently if the user selects another language. H3 sections use `### 4.1 <specific concept>`; further local structure uses short bold labels or a justified article split. Honour an explicit user/project outline in preference to these defaults, recording the mapping and reason. An adapted outline must retain applicable substance, never hide an unfinished capability.

Required top-level chapters stay recognizable. If a chapter's facts are unavailable or inapplicable, give one specific scope/effect statement there; do not invent facts or fill subordinate empty headings. Optional subsections are omitted when inapplicable. This exception does not excuse unread necessary evidence. Requirements and goals need original declarations: distinguish them from observed implementation capabilities, inferences, and unimplemented targets. Never reverse-engineer historical intent, numeric targets or acceptance results from code.

Review each chapter's actual questions against the type-specific triggers in [diagrams.md](diagrams.md#select-a-type). Structural chapters can need architecture/dependency views; cross-actor activation or request/response can need sequence views; lifecycle, lineage, entity and deployment questions need their own assessments. The article category and the presence of a flowchart do not decide its other view needs.

## Decompose capabilities before drafting

Trace original requirements and actual user actions, CLI/API entrypoints, scheduled triggers and their calls. Build a source-backed hierarchy: capability → concrete functional point → consequential subscenario. A useful functional point has a distinguishable trigger/rule and observable result or state effect. Module names, screen names, classes and function signatures alone are too coarse or too mechanical. Record unwired capabilities as unwired; a symbol's existence does not establish a connected feature.

Retain every identified point's source, overall section, principal detail article and actual answer sections in the working plan. Functional coverage is checked independently of module/topic coverage. A topic may contain several points, and a point can cross modules. Do not equate existing output headings with the source inventory or silently remove an unfinished point.

For each point explain the applicable facts at its principal detail location:

- Goal and observable result; trigger, actor and prerequisites.
- Inputs, relevant fields, validation and decision rules, with actual predicates or precedence.
- Processing steps and important alternative paths, including their outputs and data/state effects.
- Failures, cancellation and boundaries: detection, retained/changed state and recovery where implemented.
- A normal and consequential alternative walkthrough for complex behavior; source notes and focused figures as required by diagrams.md.

Use H3 sections named for actual points/mechanisms. Short bold labels within a point can separate rules, effects and cases. A feature inventory row routes the reader to these explanations; it never replaces them. Shared contracts or cross-cutting flows can be explained once and linked precisely. Do not force each helper, field or simple validation into a separate point, article or diagram.

<a id="requirement-led-explanation"></a>

## Explain requirements before mechanisms

A complete design concern or functional point should let readers understand the need before the implementation. Within the chosen chapter outline, use this reading order:

1. **Need and constraints.** State the source-declared audience/problem, trigger, input origin, observable result and hard limits that apply. Do not invent a requirement to introduce a mechanism. When only implementation evidence exists, describe the current capability and leave undeclared needs visible.
2. **Design goals.** Explain the supported design direction and identify which declared need or constraint it addresses, in a short parenthesis or an explicit prose relationship. Do not manufacture targets, trade-offs or a design decision from a plausible benefit.
3. **Solution and mechanisms.** Explain each rule's purpose and input contract before its operations. Connect the mechanism to the supported goal or constraint, give dependency order, then actual branch predicates and effects. A source-supported effect does not establish why the original author chose it, that the choice was necessary, or that it guarantees the goal.
4. **Boundaries and non-goals.** Separate declared exclusions and actual limits from the mechanism. Explain applicable empty/failure outcomes, writes, partial effects and transaction limits using original evidence. Keep a prerequisite or exception beside the action it governs; this reading order must not bury an operational constraint until after the action.

Apply this to a coherent explanation, not mechanically to every nested heading. Simple rules and field entries can refer to the parent need or shared contract. Keep the existing category chapters, stable anchors and principal explanation; do not require four new headings, fixed sentence counts or a quota of goals. Non-design articles retain their own progression. An absent declaration stays a gap, not boilerplate or an inferred historical motive.

Diagnose before restructuring: locate paragraphs that start with unexplained mechanics, goals detached from constraints, mixed needs/mechanisms/boundaries, or rules without a purpose/input contract. Send evidence gaps to analysis and organization defects to drafting under [authoring.md](authoring.md); sentence defects belong to [technical-editing.md](technical-editing.md). A sentence-only request does not authorize moving sections. Retain diagnosis and change explanations in working notes or a separately requested editing report, not production prose.

## Overall system design

The required file remains `<project name>设计文档.md`, or its existing compliant equivalent.

| H2 chapter | Required content and useful H3 decomposition |
|---|---|
| 1. 简介 | System purpose, audience, scope, terminology and system boundary. State the conclusion before describing the chapter plan. |
| 2. 需求 | Original requirements/scenarios and constraints, their sources and implementation status; roles and external dependencies. When no requirements are declared, say so and identify implemented capabilities separately. |
| 3. 目标 | Source-declared design goals, non-goals, trade-offs and constraints. Never invent performance or reliability targets. |
| 4. 功能设计 | Group by capability; enumerate all concrete points and important subscenarios. Explain each point's purpose, entry, principal rules and result, linking its precise detail section. Include a compact functional index, with narrative for the groups. |
| 5. 架构设计 | Boundaries, module responsibilities/dependencies, technical layers, shared data/state ownership, backbone interactions and global constraints. Relationship and end-to-end views answer distinct questions. |
| 6. 详细设计 | A substantive H3 section with stable anchor for every design topic: contracts, key mechanisms, state/failure behavior, relationships and limits, plus its independent detailed article. This is the system-level account of all designs, not a table of links. |
| 7. 参考文献 | Actual original documents, code entrypoints and consulted references, grouped by purpose. Include related design links here when useful; retain section-level source notes. |

Chapter 4 follows capabilities, chapter 5 follows structural responsibilities, and chapter 6 follows design concerns. Summarize at each level and link principal details rather than copying the same complete explanation into all three chapters. Neither the feature index nor the topic map can substitute for the other.

## Feature design

| H2 chapter | Required content and useful H3 decomposition |
|---|---|
| 1. 目标 | Capability, actors, intended result, boundaries and supported scenarios; distinguish declared goal from current capability. |
| 2. 设计 | Functional-point index followed by named H3 explanations of every point: entry, prerequisites, inputs, concrete rules, steps, effects and dependencies. Include interaction/display rules if implemented, not an invented UI. |
| 3. 流程 | Named normal and alternative subflows with conditions and terminal outcomes; link each back to its point. Add the needed flow, sequence and/or state views. |
| 4. 数据与接口 | Shared contracts, fields, validation, configuration, storage and activation timing used by those points; link principal technical references without repeating them. |
| 5. 异常与边界 | Failure conditions, partial/retained state, recovery and unsupported scenarios, mapped to affected points. |
| 6. 验证要点 | Source-based normal and alternative cases, inputs, intermediate decisions and expected state/output. Distinguish criteria, existing test coverage and actual run evidence; do not manufacture acceptance or run tests merely to write this chapter. |
| 7. 参考文献 | Original evidence and links to the overall anchor and related detailed designs. |

Avoid a single generic “design” paragraph followed by a large function-name table. A reader must be able to follow each real point through the rules, flow and outcome; the three explanatory chapters can share precise anchors without repeating all prose.

## Architecture design

Use this for an independently substantial architecture topic. Keep the whole-system summary in the overall design; do not duplicate that article merely to create another category.

| H2 chapter | Required content and useful H3 decomposition |
|---|---|
| 1. 目标与范围 | Architectural concern, boundaries, stakeholders and connection to the overall design. |
| 2. 约束与决策 | Source-declared constraints, selected structures, trade-offs and alternatives only where recorded. Distinguish observed implementation from historic rationale. |
| 3. 架构视图 | Relevant logical, runtime and data views, with explicit boundaries and supported connections; omit inapplicable views rather than inventing layers. |
| 4. 组件与依赖 | Responsibility allocation, contracts, dependency direction, ownership and external systems. |
| 5. 关键场景 | Trace representative capabilities across components, including consequential handoffs, data changes and failure boundaries. |
| 6. 质量与演进 | Supported consistency, security, performance or compatibility mechanisms, limits and declared evolution plans. Criteria and static mechanisms are not measurements or implemented future features. |
| 7. 参考文献 | Original decisions and code evidence, overall anchor and principal feature/module designs. |

## Module or mechanism detailed design

| H2 chapter | Required content and useful H3 decomposition |
|---|---|
| 1. 目标与职责 | Responsibility, boundaries, owned capabilities, callers and connection to the overall design. |
| 2. 对外契约 | Actual entrypoints, inputs/outputs, validation, side effects and dependencies. |
| 3. 内部结构 | Components and responsibility allocation, data/state ownership and relevant structural relationships. |
| 4. 详细设计 | Named mechanisms and functional points, algorithms, exact branch rules, defaults and precedence. Include normal and alternative worked cases near their mechanisms if not owned by a flow article. |
| 5. 流程与状态 | Processing order, transitions, publication points and applicable concurrency, cancellation and lifetime rules, with internal views as needed. |
| 6. 异常与恢复 | Detection, partial results, retention/rollback, retry and recovery where implemented, plus known limitations. |
| 7. 参考文献 | Original evidence, overall anchor and links to owned topics or principal cross-module flows. |

## Flow or state topic

| H2 chapter | Required content and useful H3 decomposition |
|---|---|
| 1. 目标与范围 | Trigger, actual entrypoint, prerequisites, start/end and excluded paths. |
| 2. 参与者与契约 | Responsibilities, calls/messages, relevant inputs and outputs. |
| 3. 流程设计 | Ordered normal and consequential alternative paths, predicates and termination. Use the view appropriate to control flow or actor handoffs. |
| 4. 状态与数据变化 | Actual state transitions/invariants, mutation and publication points, resource lifetime. |
| 5. 异常与恢复 | Failure/cancellation/shutdown, partial effects and implemented recovery. |
| 6. 场景推演 | Concrete normal and alternative cases with intermediate decisions and final state. |
| 7. 参考文献 | Original evidence, overall anchor and participating designs. |

## Data design

| H2 chapter | Required content and useful H3 decomposition |
|---|---|
| 1. 目标与范围 | Data purpose, producers/consumers and boundary. |
| 2. 模型设计 | Real entities, identifiers, relationships and ownership; ER only for actual entity relationships. |
| 3. 字段与约束 | Types, units, optionality, defaults, keys and validation; use compact field tables plus rule prose. |
| 4. 数据生命周期 | Creation, transformation, updates, retention and removal; relevant data-flow views. |
| 5. 一致性与兼容 | Invariants, ordering, persistence, schema/version behavior and failure effects where implemented. |
| 6. 场景推演 | Representative data and normal/boundary transformations with resulting state. |
| 7. 参考文献 | Original schema/code evidence and owning designs. |

Do not assume an in-memory model has a database, migration strategy or durable transaction.

## API design

| H2 chapter | Required content and useful H3 decomposition |
|---|---|
| 1. 目标与范围 | Consumers, interface boundary and supported calls; APIs may be in-process. |
| 2. 通用约定 | Actual formats, units, authentication/authorization if present, defaults, ordering and shared errors. |
| 3. 接口设计 | One H3 per coherent operation: signature/route, fields, validation, response, effects and operation-specific rules/errors. |
| 4. 调用流程 | Important multi-step interaction and dependency order; focused sequence/flow views when triggered. |
| 5. 错误与边界 | Error semantics, partial effects, idempotence, retry and compatibility only as supported. |
| 6. 调用示例 | Actual contract-shaped examples, normal and important error outcomes. Expected output is not observed output. |
| 7. 参考文献 | Original declarations/implementations and owning feature designs. |

## Configuration design

| H2 chapter | Required content and useful H3 decomposition |
|---|---|
| 1. 目标与范围 | Configuration purpose, writers/readers and scope. |
| 2. 配置模型 | Actual sources, storage, ownership, precedence and defaults. |
| 3. 配置项设计 | Entries grouped by function: name, type, units, allowed values and validation, with consequential rule prose. |
| 4. 加载与生效流程 | Read/merge/validate/save/activate order, reload/restart requirements and downstream effects; focused decision/activation views. |
| 5. 异常与安全边界 | Invalid input, failed writes, retained or changed state, recovery and sensitive-value handling as implemented. |
| 6. 配置示例 | Normal and consequential invalid/failure cases, showing actual resulting configuration/state. |
| 7. 参考文献 | Original evidence, overall anchor and consumers. |

## Deployment design

| H2 chapter | Required content and useful H3 decomposition |
|---|---|
| 1. 目标与范围 | Supported deployment scope and declared goals. |
| 2. 环境与约束 | Actual platform, dependencies, resource/network/security prerequisites with evidence. |
| 3. 部署拓扑 | Declared or actually observed component placement, boundaries and connections; label the evidence category. |
| 4. 组件与配置 | Roles, actual configuration/port/path contracts, persistence and secrets injection if present. |
| 5. 部署与变更流程 | Supported startup, updates, ordering and result criteria; distinguish a design from human operation instructions. |
| 6. 故障与恢复 | Detection and documented recovery/rollback mechanisms and their limits. |
| 7. 参考文献 | Original manifests/guides and architecture links; no invented observations. |

## Review before delivery

Check category, chapter order, relevant subsection depth and layout against the article's purpose. Then derive the functional inventory again from original sources and compare it with actual prose, precise links and figure uses. A completed template or a large collection does not prove either check. Missing points, one-line point summaries, incorrect blanket no-figure decisions and unsupported “requirements” fail semantic review. Keep missing evidence and unfinished work pending and return correctable gaps to planning/drafting in the same invocation.
