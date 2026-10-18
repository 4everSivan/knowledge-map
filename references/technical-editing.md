# Technical prose editing

This is the expression-editing (去 AI 味) pass of the per-article lifecycle in [authoring.md](authoring.md). It always runs as its own pass, after the content check and before the fact recheck.

## Purpose and inputs

Improve the readability of source-grounded technical prose. Use the project's approved document format and terminology. Keep the output language selected for the document; English instructions do not require English output.

The caller supplies the candidate, its inspected evidence, its document purpose, and the permitted edit scope. For updates, it also supplies the affected passages and relevant comparison with the existing document. Read needed context before editing. If evidence or scope is missing, return the gap to analysis or drafting.

## Authority and scope

- Review the draft against its evidence before changing its expression.
- For a new article, edit the supported draft within its agreed purpose. For an update, edit only the scope the caller supplies under [authoring.md](authoring.md#update-article); unaffected text stays as it is, and a review alone does not refresh the content date.
- Send factual or structural defects back to analysis or drafting, then restart expression editing from the corrected candidate. They are never repaired silently as style changes.

## Technical invariants

Preserve who acts, what triggers the action, prerequisites, scope, defaults, precedence, units, limits, exceptions, failures, state transitions, and recovery behavior. Preserve negation and the difference between possible, required, expected, implemented, and observed behavior.

Keep code blocks, inline code, formulas, commands, identifiers, precise values, placeholders, paths, link targets, explicit anchors, and quoted source text unchanged during this pass. Keep headings, section order, table structure, and ordered steps; heading punctuation and the fixed labels listed below may be normalized. Return any needed correction of those items to drafting.

Keep source attribution attached to the claims it supports. Do not turn design intentions into implementation claims, static source observations into runtime evidence, or incomplete coverage into verified absence. Leave uncertainty visible where it affects the reader.

For cards, the default scope is no edits. If the caller explicitly includes card prose, edit only `definition` and `project_usage` within the supplied scope and evidence. Preserve their distinct meanings. Leave all other fields, IDs, enumerations, source associations, article links, and JSON structure unchanged. Article prose does not replace original evidence for a card.

## Readability work

Identify a concrete reading problem before revising a passage. Prefer specific actors and direct verbs when the draft already establishes them. Remove empty repetition, unsupported promotional tone, and assistant-facing narration that does not help the document reader.

Keep necessary explanation and useful repetition across independently read reference entries. A clear summary, a parameter table, or a predictable procedure can be the right technical form. Do not replace technical terms with varied synonyms or remove meaningful qualifications for brevity.

Check the permitted passages against the professional presentation rules in [writing.md](writing.md#presentation). Diagnose these defects and route them as shown:

| Defect | Handling in this pass |
|---|---|
| Generation-process narration (“本轮”, “经分析”, “未读取到”, check results, samples) | Remove when the page's introduction or the library `README.md` already states the evidential basis; otherwise return to drafting to add that statement once |
| The same verification disclaimer repeated across paragraphs | Keep one statement at the claim or in the scope; remove repetitions that add no claim-specific condition |
| Colloquial, promotional, or first-person wording; exclamations; rhetorical questions | Rewrite as neutral declarative prose with the same meaning |
| Mixed labels (`来源：`, `实现依据：`, ad hoc callouts) or a misplaced update date | Normalize to `依据：`, `> **说明**：`, `> **注意**：`, and a final `最后更新：` line without changing link targets |
| Chinese punctuation, spacing, or inconsistent term naming | Apply the typography rules; keep identifiers byte-identical |
| H1 not matching the filename, missing introduction, figure-, table-, or link-only article, flat `README.md` list | Structural; return to drafting |

Work within paragraphs. Split or combine sentences when this clarifies an existing relationship without changing its meaning. If readability requires new evidence, a different outline, or reordered information, return that issue to drafting.

Aim for clear technical prose, not for sounding human: add no anecdotes, imagined outcomes, author persona, deliberate mistakes, or irregular rhythm, and use no word bans, deletion quotas, detector scores, or claims that the result is demonstrably human-written. If a passage has no actual expression problem, leave it unchanged.

## Editing sequence

1. Check the candidate against the inspected evidence. Identify unsupported claims and missing conditions before prose work; return those issues to analysis or drafting.
2. Locate the permitted passages and note the specific readability and presentation defects. Keep this working record separate from the reader's document.
3. Make the smallest useful expression changes while preserving the technical invariants.
4. Compare the edited candidate with the draft. Revert any expression change that alters an invariant or reaches beyond the allowed scope.
5. Recheck affected claims against their original evidence, including conditions and exceptions. Comparing two drafts alone cannot establish factual correctness. Return unresolved content issues to analysis or drafting.
6. Return the checked candidate, actual edit scope, and unresolved issues to the caller. Keep operational review notes out of the article unless they describe a limitation the reader needs.

Parsing and link checks establish structural results only; they do not prove semantic equivalence. Repeated passes by the same conversation are not independent review.

The workflow controls whole-library checks and delivery; a checked article candidate does not by itself authorize replacing the official collection.

## Provenance

This reference is independently worded for knowledge-map's confirmed editing authority, update scope, evidence rules, and output contracts. It draws on the upstream idea of diagnosing prose before making faithful local repairs; it does not translate or reproduce the upstream prompt bundle.

Consulted on 2026-10-15 at commit `59eafed6c9ebee0cce142e2ea54aab41014afbe9`:

- [de-AI-writing entrypoint](https://github.com/OUBIGFA/De-AI-Prompt-Enhancer-Writer-Booster-SKILL/blob/59eafed6c9ebee0cce142e2ea54aab41014afbe9/de-AI-writing/SKILL.md)
- [Faithful-rewrite guardrails](https://github.com/OUBIGFA/De-AI-Prompt-Enhancer-Writer-Booster-SKILL/blob/59eafed6c9ebee0cce142e2ea54aab41014afbe9/de-AI-writing/references/translation-guardrails.md)

This reference is maintained locally; nothing is fetched from upstream at runtime.
