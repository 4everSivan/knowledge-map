# Engineering diagrams

Read this at architecture planning and topic authoring. Read [diagram-state.md](diagram-state.md) for fields and delivery, [style](diagrams/style.md) before drawing, and only the selected type reference below. Use the host's existing tools; do not install another skill, renderer, engine, or km script.

## Plan from reader questions

Required figures have these evidence-grounded triggers:

| Project fact | Required explanation |
|---|---|
| Multiple business modules depend on or collaborate with one another | Overall module relationships |
| A complex cross-module flow has consequential ordering or responsibility handoffs | Interactions, branches, and applicable failure/recovery |
| Explicit business states and conditional transitions determine behavior | States, triggers, guards, and terminal outcomes |

Select an appropriate type, not a file quota. One figure may cover several questions. Small independent modules need no decorative diagram. Add other required or optional figures when actual reader questions justify them. Record each figure's article uses, required/optional status, trigger, original evidence, and reason in the run plan. Any required use makes a shared figure required for the collection. Never downgrade because drawing or previewing failed. Changing necessity requires a source-grounded change in the plan, not an excuse after failure.

Check available tools for standalone SVG and rendered Markdown early, before deep topic writing. Resolve the actual intended Markdown viewer from project conventions or the available environment, and record the limitation if it cannot be determined. This check does not decide necessity or authorize dependency installation.

## Semantic first

1. Read original code, configuration, tests, and original documents. Trace relevant entrypoints, calls, conditions, data and states. Generated diagrams, lists and prose are comparison inputs, not independent evidence.
2. Create or update the semantic JSON candidate. Review each engineering node, relation, meaningful group and type-specific fact against its evidence. Evidence must support a relation's direction and meaning, not merely the existence of both ends. Several elements can share evidence.
3. Separate implementation from unimplemented targets in different figures. A target needs original support and a visible target/not-implemented caption. Explain configuration as declared configuration, not observed deployment. Supported abstractions of actual roles are allowed; do not invent wiring.
4. Load the chosen type and style. Adapt the [SVG base](../assets/diagrams/base.svg), retaining stable element IDs. Make the engineering meaning agree with the checked list. Preliminary layout sketches remain candidates.
5. Draft or update associated prose and its alt text, caption and references, using the figure presentation in [writing.md](writing.md#professional-presentation). Edit wording within the supported meaning; preserve identifiers, guards, negation, limits, ordering and arrow kinds. Recheck edited labels and corresponding source claims.
6. Check the figure, list and articles together, then perform both actual rendering checks. A checked JSON candidate does not establish visual readability.

Return wrong or unsupported facts to source reading and semantic drafting. Correct wrong rendering of a valid list in SVG. Revisit all affected outputs when new evidence changes the list. Never repair an unsupported drawing by manufacturing matching evidence entries.

## Select a type

| Question | Type and reference |
|---|---|
| Components, responsibility and boundary | [architecture](diagrams/type-architecture.md) |
| Decisions and control paths | [flowchart](diagrams/type-flowchart.md) |
| Ordered messages between actors | [sequence](diagrams/type-sequence.md) |
| State and conditional transitions | [state](diagrams/type-state.md) |
| Data origin, transformation and destination | [data_flow](diagrams/type-data-flow.md) |
| Logical entities and relationships | [er](diagrams/type-er.md) |
| Where software is declared or observed to run | [deployment](diagrams/type-deployment.md) |
| Consumer/provider dependencies and cycles | [dependency](diagrams/type-dependency.md) |

Each type reference defines semantic properties; they are not layout coordinates or an executable diagram language. Do not discard ordering, cardinality or boundaries to force every type into untyped arrows.

## Scope and shared figures

Give each logical figure one list, one SVG and one owner article. Other articles refer to it. Different views may use separate figures with explicit purpose, scope, and parent/detail links in their article captions. Summaries can omit disclosed detail, not contradict shared contracts. A split flow states entry, exit and its place in the overview. Never remove essential branches to meet a node budget.

For an update compare semantic changes separately from layout and reference changes. Preserve valid unchanged SVG bytes and IDs. Change affected elements and necessary nearby routing; explain unavoidable wider reflow. Follow shared evidence and contracts to all figures and article uses. Do not reflow an entire collection for style consistency.

## Required checks

- **Structure:** Parse JSON/SVG with existing tools when available. Check allowed fields, IDs, endpoints, evidence references, type properties, path roots, image links and the SVG subset in style.md. Match every list node/relation/group to one SVG `data-node-id`/`data-relation-id`/`data-group-id`. A relation can have several graphical children inside its single group. Decorative geometry needs no engineering evidence. Compare all figure uses with actual Markdown image references.
- **Meaning:** Review original support, conditions, direction, state responsibility and shared terms across list, SVG, prose and cards. Rendering geometry and labels must actually convey the meaning; a data attribute alone cannot prove correctness.
- **Rendering:** Actually inspect both standalone SVG and the Markdown article embedding it. Check Chinese glyphs, label/connector clearance, arrows, clipping, grouping, and readability at the article's intended display width. Record viewer/tool, actual observed environment, inspected article paths and figure hashes. A browser-open attempt, XML parse or accessibility text without visual inspection is not a visual pass. State exactly which viewer was checked; do not imply all Markdown/PDF/Word/site compatibility.

Reuse earlier visual evidence only for identical SVG hashes and applicable viewer, font, size and embedding conditions; identify the earlier check and actual reuse basis. Changed relevant conditions invalidate that reuse. Mark unavailable checks `not_run`, failed checks `failed`; never invent a screenshot, tool version or hash.

An unfinished required figure prevents confirmation. A previously planned optional figure can be deferred if the official collection omits it, all current references and active index entries are removed, and prose remains complete. Retain actual candidate failures and deferred work separately from source-coverage gaps. Unknown ownership or external edits still block replacement even during retirement. See diagram-state.md for retention and interrupted writes.

## Provenance

This is a local technical adaptation, not an invocation of the upstream skill. Source, license and deliberate changes: [upstream notice](diagrams/upstream-notice.md).
