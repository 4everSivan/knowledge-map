# Per-article authoring

Apply this lifecycle to each article inside a topic batch. The workflow owns project scope, collection checks, and delivery, so a finished article stays a candidate until those pass. A finished article is also not a finished module: the module's main design and required topics are checked as a set ([writing.md](writing.md#module-planning-and-content-ownership)).

Every article passes through four separate stages: analysis, drafting with a source check, expression editing, and a fact recheck. Expression editing (去 AI 味) is always its own pass, run with [technical-editing.md](technical-editing.md) after the content is checked.

## New article

1. **Analyse.** Read original code and project documents. Trace the relevant entrypoint, prerequisites, normal path, branches, errors, and termination. Choose the reader's question, document type, and supported scope.
2. **Draft and check sources.** Draft using [writing.md](writing.md). Before touching expression, check every claim against evidence, including actors, defaults, precedence, failures, and declared versus implemented behavior. Return unsupported content to analysis or drafting.
3. **Edit expression.** Load [technical-editing.md](technical-editing.md) and revise expression within the supported draft, protecting technical facts and structure.
4. **Recheck facts.** Compare the edited candidate with the draft and recheck affected claims against original sources. Revert expression drift. Fix content defects in analysis or drafting and repeat the affected checks.

The article is complete when its content is supported, its structure suits the reader, its technical meaning survived editing, and each source association can be explained. A source link alone does not establish support. When necessary evidence is missing, keep the gap and the candidate.

## Update article

1. **Analyse the change.** Read changed sources and trace affected callers, configuration consumers, and shared contracts, using original project documents as declarations where appropriate. Widen the analysis if the impact cannot be bounded.
2. **Compare.** Check the existing article's affected assertions against current evidence. Classify each as a semantic change, a reference-only change, previously incorrect content, or a change with no documented impact.
3. **Update content.** Update affected content, examples, conditions, and references. Make necessary outline or anchor changes here and fix incoming navigation and card bindings. Review the corrected candidate against sources before editing expression.
4. **Edit expression locally.** Apply technical editing only to changed passages and the context needed to understand them. Unrelated valid text stays byte-identical.
5. **Recheck.** Check the content update and the expression changes separately: original evidence, protected literals, conditions, references, and affected card meanings. Return the checked candidate and its actual change scope.

Reuse an article when reliable evidence shows its content and references still apply and its output ownership is intact; keep its content date. Source verification metadata can change without a knowledge-content revision. Previous partial coverage, unknown source changes, or unverifiable output edits rule out the no-change shortcut.

Classify module updates before choosing pages to edit. An internal mechanism change with unchanged responsibilities and external contracts may touch only the module's main design or relevant topics. Changed interfaces, state ownership, dependencies, or backbone interactions also require checking the overall design, participating modules, and the principal cross-module flow; rewrite those pages only where their content or references are actually affected.

## Return paths

| Finding | Return to |
|---|---|
| Wrong fact, missing prerequisite, unsupported claim, or unclear source | Analysis and drafting |
| Mixed reader purposes, needed section moves, title changes, or page splits | Planning or drafting; repair incoming references |
| Changed literal, qualifier, limit, negation, or certainty during editing | Revert that expression change and recheck evidence |
| Conflicting or unavailable source | The workflow's coverage and validation decision |
| No readability defect | Keep the passage unchanged |

Review notes go in attempt records or candidate notes, not into the article; reader-relevant limitations go next to the affected claims. No stage needs separate user approval.

## Cards and figures in the lifecycle

Verify each card's `definition` and `project_usage` against their own evidence and the affected articles during analysis and drafting. Expression editing covers Markdown only by default and leaves card identity, fields, source links, and article bindings untouched.

Plan figure uses before drafting and follow [diagrams.md](diagrams.md) for the semantic list, drawing, and checks. Expression editing preserves figure and list identities and meaningful literals. An article whose required figure is unfinished stays a candidate.
