# Per-article authoring

Apply this lifecycle inside each topic batch. The outer workflow owns project scope, collection checks, and official delivery. A finished article remains a candidate until those checks pass.

## New article

1. Read original code and project documents. Trace the relevant entrypoint, prerequisites, normal path, branches, errors, and termination. Choose the reader's question, document type, and supported scope.
2. Draft using [writing.md](writing.md). Check claims against evidence before editing expression, including actors, defaults, precedence, failures, and declared versus implemented behavior. Return unsupported content to reading or drafting.
3. Load [technical-editing.md](technical-editing.md). Revise expression within the supported draft while protecting technical facts and structure.
4. Compare the edited candidate with the draft and recheck affected claims against original sources. Revert expression drift. Correct content defects in reading or drafting and repeat the affected checks.

The completion condition is supported content, suitable structure, preserved technical meaning, and source associations that can be explained. A source link alone does not establish support. If necessary evidence is missing, preserve the gap and candidate rather than claiming completion.

## Update article

1. Read changed sources and trace affected callers, configuration consumers, and shared contracts. Use original project documents as declarations where appropriate. Broaden the analysis if the impact cannot be bounded.
2. Compare the existing article's affected assertions with current evidence. Classify semantic changes, reference-only changes, previously incorrect content, and changes with no documented impact. Existing generated prose is a comparison input, not a factual source.
3. Update affected content, examples, conditions, and references. Handle necessary outline or anchor changes here and fix incoming navigation and card bindings. Review the corrected candidate against sources before style work.
4. Apply technical editing only to changed passages and the context needed to understand them. Keep unrelated valid text unchanged; do not rewrite the whole page for stylistic consistency.
5. Check the content update and the subsequent expression changes separately. Recheck original evidence, protected literals, conditions, references, and affected card meanings. Return a checked candidate and actual change scope.

Reuse an article when reliable evidence establishes that its content and references remain applicable and output ownership is intact. Preserve its content date. Source verification metadata can change without a knowledge-content revision. Previous partial coverage, unknown source changes, or unverifiable output modifications prevent a no-change shortcut.

## Return paths and boundaries

| Finding | Return to |
|---|---|
| Wrong fact, missing prerequisite, unsupported claim, or unclear source | Evidence analysis and content drafting |
| Mixed reader purposes, needed section moves, title changes, or page splits | Planning or drafting; repair incoming references |
| Changed literal, qualifier, limit, negation, or certainty during editing | Revert that expression change and recheck evidence |
| Conflicting or unavailable source | Coverage and validation decision in the outer workflow |
| No readability defect | Keep the passage unchanged |

Keep review notes in attempt records or candidate notes, not as repetitive process narration in the article. Reader-relevant limitations belong near the affected claims. Do not add per-stage user approvals.

For cards, verify `definition` and `project_usage` against their respective evidence and affected articles. The default v0.1 style pass covers Markdown only; do not use prose editing to mutate card identity, fields, source links, or article bindings. Necessary card content updates belong in the topic's evidence and drafting work.
