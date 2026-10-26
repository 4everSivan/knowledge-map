# Engineering diagrams

Read this when scoping preview capability, planning, and authoring. It owns figure necessity, semantic-first creation, required checks, and deferral. Read [diagram-state.md](diagram-state.md) for fields and delivery, [style](diagrams/style.md) before drawing, and only the selected type reference below.

## Plan from reader questions

Assess the eight views below against original sources before choosing figures. These are independent explanation needs: one mechanism can trigger several. A required view needs the type-specific meaning in the table, not merely an image or a sequence of boxes.

Apply these triggers to every design article: overall design, module main design, each detailed topic, and principal flow. Identify the actual internal mechanism first. A short synopsis, a platform label, or a diagram elsewhere does not establish that this article needs none. For each article record the decision, original-source reason and applicable figure IDs in its document-plan assessment. A no-figure decision needs a concrete reason, such as a simple field-only contract without a consequential flow/state/relationship; “optional”, “short article” and “already has an overview” alone are insufficient.

Assess the functional points and their important submechanisms separately within each article, using the decomposition in [design-outlines.md](design-outlines.md). Record the question, sources, needed/no-figure reason and applicable figure IDs for each point. An article-level decision is a summary of these assessments, not permission to stop after one image. Overall relationship and end-to-end views, feature flows, internal decisions, failure retention, state transitions and activation sequences can require different views. Combine questions only when the actual drawing remains complete and legible at article width. No fixed image quota replaces this review.

Required figures are embedded in the articles whose explanation needs them, with captions and prose explaining the key branches or handoffs. Reuse an existing figure only when its scope and detail answer the same question; otherwise draw a focused detail view and explain its place in the larger flow within the article. Evaluate all important mechanisms: one token figure does not satisfy unrelated cache, recovery and activation questions.

Select an appropriate type, not a file quota. One figure may cover several questions at the same scope. Small independent modules need no decorative diagram. Record view decisions and each figure's article uses, required/optional status, trigger, original evidence, and reason under diagram-state.md. Any required use makes a shared figure required for the collection. Necessity changes only through a source-grounded change in the plan, never because drawing or previewing failed.

Check available tools for standalone SVG and rendered Markdown early, before deep topic writing. Resolve the actual intended Markdown viewer from project conventions or the available environment, and record the limitation if it cannot be determined. This check does not decide necessity or authorize dependency installation.

## Semantic first

1. Read original code, configuration, tests, and original documents. Trace relevant entrypoints, calls, conditions, data and states.
2. Create or update the semantic JSON candidate. Review each engineering node, relation, meaningful group and type-specific fact against its evidence. Evidence must support a relation's direction and meaning, not merely the existence of both ends. Several elements can share evidence.
3. Separate implementation from unimplemented targets in different figures. A target needs original support and a visible target/not-implemented caption. Explain configuration as declared configuration, not observed deployment. Supported abstractions of actual roles are allowed; every drawn connection needs evidence.
4. Load the chosen type and style. Adapt the [SVG base](../assets/diagrams/base.svg), retaining stable element IDs. Make the engineering meaning agree with the checked list. Preliminary layout sketches remain candidates.
5. Draft or update associated prose and its alt text, caption and references, using the figure presentation in [writing.md](writing.md#presentation). Edit wording within the supported meaning; preserve identifiers, guards, negation, limits, ordering and arrow kinds. Recheck edited labels and corresponding source claims.
6. Check the figure, list and articles together, then perform both actual rendering checks. A checked JSON candidate does not establish visual readability.

Return wrong or unsupported facts to source reading and semantic drafting. Correct wrong rendering of a valid list in SVG. Revisit all affected outputs when new evidence changes the list. Repair an unsupported drawing by changing the drawing, never by adding evidence entries to match it.

## Select a type

| Type and reference | Source-grounded trigger | Required meaning |
|---|---|---|
| [architecture](diagrams/type-architecture.md) | Several responsibilities/components collaborate, or a system/trust boundary needs a whole-system explanation | Components, responsibility allocation, boundaries and supported call/read/write/publication directions |
| [flowchart](diagrams/type-flowchart.md) | Decisions, validation, algorithms, loops or early exits select consequential outcomes | Entry, actions, explicit predicates, alternative paths and exits |
| [sequence](diagrams/type-sequence.md) | Correctness depends on who calls whom and when: multi-party request/response, synchronous waiting, asynchronous handoff, save-before-activate, or error propagation between actors | Actor lifelines and ordered messages, call/return/async mode, guards and conditional scenarios. Synchronous in-process calls can trigger this too |
| [state](diagrams/type-state.md) | A stored domain status has meaningful event/condition-driven transitions, or an object/resource lifecycle changes permitted actions, recovery or terminal outcomes | One named subject's actual states, transition events, applicable guards and actions. State writes need not implement an enforced transition validator, and an enum is unnecessary; control steps or one call's result codes alone do not establish a state machine |
| [data_flow](diagrams/type-data-flow.md) | Data passes through material parsing, normalization, filtering, aggregation, caching or persistence and readers need to track origin, derivation, ownership or destination | Sources, transformations, stores and sinks; arrows name payloads and distinguish movement, derivation and persistence |
| [er](diagrams/type-er.md) | Relationships between domain entities, their identities or cardinalities matter to supported behavior, with evidence from models, schema, ORM or original declarations | Entities, relevant fields, associations and endpoint cardinalities. Logical entities need no database; a lone DTO or field list does not by itself justify ER |
| [deployment](diagrams/type-deployment.md) | Original deployment/configuration evidence establishes meaningful placement in processes, hosts, containers, environments or network boundaries and their connections | Placement, boundaries and supported connection/port/protocol facts, visibly declared or observed as appropriate. A package import is not deployment evidence |
| [dependency](diagrams/type-dependency.md) | Understanding coupling, layering, shared providers, integration or cycles requires consumer/provider relationships between modules, packages or services | Consumer-to-provider direction, dependency scope and applicable conditions; distinguish build/import dependencies from runtime calls. A graph can be necessary without cycles |

Use the selected reference before drafting its semantic list. Its fields are meaning, not coordinates or an executable diagram language. Preserve order, modes, state guards, data payloads, cardinality and placement rather than reducing every question to control-flow arrows.

### Keep the views distinct

Start with the questions, then select the type. A save/refresh mechanism can need a flowchart for validation decisions, a sequence view for persistence and callback return ordering, and a data-flow view for the saved configuration's effect on derived results. Draw only the independently needed views and explain how their scopes relate; the existence of one does not settle the others.

A necessary sequence view shows actors, lifelines and messages; a state view shows the subject and event/guard transitions; a data-flow view shows named payload lineage. Do not relabel a flowchart or change only its JSON `type` to claim another view. A state view must not turn `fresh`, `partial` and `failed` return values into stored states without evidence. An ER/deployment view must not invent tables, foreign keys, hosts, replicas or ports.

When a question is already fully answered by an existing view, record the actual figure and the facts carrying that explanation. For example, an architecture view with explicit consumer-to-provider dependencies may make a second dependency drawing redundant; a generic calls diagram does not. Omitting a separate view needs this concrete equivalence or a source-supported simplicity/inapplicability reason, not “there is already a flowchart”. Unread relevant evidence remains pending.

During initial builds and structural repairs, retain view assessments for all eight types across the collection (diagram-state.md), with article-specific records for the independently needed questions. Reassess affected views on updates. If nearly all outputs are flowcharts, revisit the other source dimensions and record why they are unnecessary or still missing; do not manufacture type diversity or accept a quota as proof of coverage.

## Scope and shared figures

Give each logical figure one list, one SVG and one owner article. Other articles needing the same view embed that SVG directly with their own necessary explanation, without linking to its owner article. Different views may use separate figures with explicit purpose, scope and parent/detail relationships described in their article captions; links to explanations stay within the same article under writing.md. Summaries can omit disclosed detail, not contradict shared contracts. A split flow states entry, exit and its place in the overview. Never remove essential branches to meet a node budget.

For an update compare semantic changes separately from layout and reference changes. Preserve valid unchanged SVG bytes and IDs. Change affected elements and necessary nearby routing; explain unavoidable wider reflow. Follow shared evidence and contracts to all figures and article uses. Do not reflow an entire collection for style consistency.

## Required checks

- **Structure:** Parse JSON/SVG with existing tools when available. Check allowed fields, IDs, endpoints, evidence references, type properties, path roots, image links and the SVG subset in style.md. Match every list node/relation/group to one SVG `data-node-id`/`data-relation-id`/`data-group-id`. A relation can have several graphical children inside its single group. Decorative geometry needs no engineering evidence. Compare all figure uses with actual Markdown image references.
- **Meaning:** Review original support, conditions, direction, state responsibility and shared terms across list, SVG, prose and cards. Rendering geometry and labels must actually convey the meaning; a data attribute alone cannot prove correctness.
- **View coverage:** Record required `figure_view_coverage`. Independently derive the needed questions from sources and compare the view assessments with actual figure types, type-specific meaning, article embeddings and no-view reasons. Missing required sequence/state/data/entity/placement/dependency meaning fails even when every article has a valid flowchart. Counts and type labels alone cannot pass this check. A justified simple project may use only one type.
- **Rendering:** Actually inspect both standalone SVG and the Markdown article embedding it. Check Chinese glyphs, label/connector clearance, arrows, clipping, grouping, and readability at the article's intended display width. Record viewer/tool, actual observed environment, inspected article paths and figure hashes. A browser-open attempt, XML parse or accessibility text without visual inspection is not a visual pass. State exactly which viewer was checked; do not imply all Markdown/PDF/Word/site compatibility.

Reuse earlier visual evidence only for identical SVG hashes and applicable viewer, font, size and embedding conditions; identify the earlier check and actual reuse basis. Changed relevant conditions invalidate that reuse. Mark unavailable checks `not_run` and failed checks `failed`.

An unfinished required figure prevents confirmation. A previously planned optional figure can be deferred if the official collection omits it, all current references and active index entries are removed, and prose remains complete. Retain actual candidate failures and deferred work separately from source-coverage gaps. Unknown ownership or external edits still block replacement even during retirement. See diagram-state.md for retention and interrupted writes.

## Provenance

This is a local technical adaptation, not an invocation of the upstream skill. Source, license and deliberate changes: [upstream notice](diagrams/upstream-notice.md).
