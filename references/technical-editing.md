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

Identify a concrete reading problem before revising a passage. Apply the [sentence construction rules](#sentence-construction) to the permitted prose. Remove empty repetition, unsupported promotional tone, and assistant-facing narration that does not help the document reader.

Keep necessary explanation and useful repetition across independently read reference entries. A clear summary, a parameter table, or a predictable procedure can be the right technical form. Do not replace technical terms with varied synonyms or remove meaningful qualifications for brevity.

Check the permitted passages against the professional presentation rules in [writing.md](writing.md#presentation). Diagnose these defects and route them as shown:

| Defect | Handling in this pass |
|---|---|
| Generation-process narration (“本轮”, “经分析”, “未读取到”, check results, samples) | Remove when the page's introduction or the library `README.md` already states the evidential basis; otherwise return to drafting to add that statement once |
| The same verification disclaimer repeated across paragraphs | Keep one statement at the claim or in the scope; remove repetitions that add no claim-specific condition |
| Colloquial, promotional, or first-person wording; exclamations; rhetorical questions | Rewrite as neutral declarative prose with the same meaning |
| Mixed note/risk labels or a misplaced update date | Normalize to `> **说明**：`, `> **注意**：` and a final `最后更新：` line without changing link targets |
| Local source-link lists, referrals to other documents, or an inapplicable bibliography | Return to drafting under writing.md; this expression-only pass cannot remove links, chapters or necessary context |
| Chinese punctuation, spacing, or inconsistent term naming | Apply the typography rules; keep identifiers byte-identical |
| H1 not matching the filename, missing introduction, figure-, table-, or link-only article, flat `README.md` list | Structural; return to drafting |
| A design explanation opens with mechanics without its need/purpose, goals have no supported constraint, or inputs and boundaries are mixed | Return to analysis or drafting under design-outlines.md; do not add motives or reorder paragraphs in this pass |

Work within paragraphs. Split or combine sentences when this clarifies an existing relationship without changing its meaning. If readability requires new evidence, a different outline, or reordered information, return that issue to drafting.

Aim for clear technical prose, not for sounding human: add no anecdotes, imagined outcomes, author persona, deliberate mistakes, or irregular rhythm, and use no word bans, deletion quotas, detector scores, or claims that the result is demonstrably human-written. If a passage has no actual expression problem, leave it unchanged.

Words such as “组织成”, “转为”, “装配”, “归一” or “交付” are cues to inspect the action and object, not forbidden words. Keep an exact technical term or meaningful transformation; simplify only an empty construction whose meaning is already established. Remove a vague “该设计/该模块” subject only when its referent can be made clear without guessing an actor. Add no explanatory metaphor absent from the supported draft.

<a id="sentence-construction"></a>

## Sentence construction

Edit sentences inside the existing paragraphs. Keep the content, headings, section boundaries and paragraph order; adding a heading or reorganizing the article belongs to drafting. These rules concern the article's prose, not its protected literals or quoted source text.

- **Subject and ownership.** Choose the subject by the sentence's focus: the actor, affected object or situation can lead. Make each action's actor and recipient clear, including when several actors appear. An omitted subject is fine when context resolves it; name the new actor when responsibility changes. Do not force every sentence into the same subject pattern or invent an unknown actor.
- **Verb and object.** Name the concrete action and what it acts on: “核对配置”, “拒绝请求”, “连接服务”, “创建记录”. Replace empty “进行/实现/完成/做了/开展” constructions and vague objects such as “强大功能/完善支持/做出保障” when the intended action and object are already established. Keep a verb when it carries technical meaning, such as “实现接口”; these examples are diagnostic cues, not banned words.
- **One matter, ordered actions.** Give each sentence one main matter and prefer short clauses to stacked modifiers. Closely related actions can form a comma-separated chain in their actual order. Split unrelated matters; when splitting, retain each condition's reach, exception and actor. Do not separate an action from the qualification that makes it true.
- **Condition before its action.** Put an existing trigger or prerequisite before the action it governs (“……时”, “若……”, “在……情况下”), followed by the action and supported result. Preserve timing, nesting and logical force: “仅当” is not interchangeable with “若”. A condition that governs only one action must not acquire wider scope. Leave an unconditional statement unconditional.
- **Direct negation.** State an established boundary with a direct negative predicate and its object: “不改动原文件”, “不重复提交请求”. Remove softening only when the meaning is already an unconditional boundary. Preserve genuine advice, uncertainty and quantifiers: “建议避免” is not a prohibition, “可能不” is not “不”, and “不保证成功” is not “保证失败”.
- **Voice.** Prefer the known actor's direct action when it makes responsibility clearer. An affected object can remain the subject; use a result-oriented passive when the actor cannot be identified. Do not manufacture an actor to eliminate passive voice or mechanically replace a natural object-focused sentence.
- **Supported outcome.** State the successful or failed output/state when it is already established in the checked draft. Keep the distinction between returning an error, retaining data, retrying and terminating; an action alone does not imply any of them. If a needed outcome or actor is absent or ambiguous, return to analysis or drafting, confirm the source and resume editing. Do not add a result, guarantee, cause or alternative branch merely to make the sentence feel complete, or require both success and failure in every sentence.
- **Neutral wording.** Remove promotional adjectives and empty degree claims (“大幅”, “显著”, “更加”, “强大”, “一站式”); state the supported action or measurable fact instead. Preserve meaningful quantities, comparisons, limits, terminology and proper names. Use declarative sentences without exclamations or rhetorical questions, and leave a clear sentence unchanged.

The following are illustrative editing cases, not claims about the target project. Each rewrite uses only the facts already present in its original; conditional variants state the extra evidence they require.

| Reading problem | Original | Faithful rewrite or return path |
|---|---|---|
| Responsibility changes mid-sentence | 调用方提交请求给队列，队列接收请求后由工作线程取出并进行执行。 | 调用方向队列提交请求，队列接收请求，工作线程取出并执行请求。 |
| Empty verb and vague modifier | 校验器提供强大的配置检查功能，对配置中的端口进行范围核对。 | 校验器核对配置中端口的取值范围。 |
| A necessary condition appears late | 调度器将任务加入队列，仅当队列未满时。 | 仅当队列未满时，调度器才将任务加入队列。不能改成“若队列未满，调度器就将任务加入队列”。 |
| The condition governs only the first action | 缓存可写时，工作线程写入缓存；无论缓存是否可写，工作线程都返回结果。 | 缓存可写时，工作线程写入缓存。无论缓存是否可写，工作线程都返回结果。不能把“返回结果”移入条件内。 |
| A known boundary is padded | 接口拒绝空请求，不接受空请求进入队列，尽量避免把空请求加入队列。 | 接口拒绝空请求，不将空请求加入队列。 |
| The result is buried in nominal phrases | 保存成功时，配置器完成新配置的启用；保存失败时，配置器进行旧配置的保留。 | 保存成功时，配置器启用新配置；保存失败时，配置器保留旧配置。 |
| The subject can naturally be omitted | 若队列已满，拒绝新请求。 | 上下文已明确拒绝者时保留原句；不能为了显式主语而猜测组件名。 |
| The outcome or actor is missing | 请求被处理。 | 返回分析或起草，确认谁对请求执行什么动作以及适用结果；不能直接改成“服务校验请求并返回成功”。 |

## Editing sequence

1. Check the candidate against the inspected evidence. Identify unsupported claims and missing conditions before prose work; return those issues to analysis or drafting.
2. Locate the permitted passages and note the specific readability and presentation defects. For a sentence defect, identify its actor, action, object, applicable condition and supported outcome; keep unknowns as gaps. Keep this working record separate from the reader's document.
3. Make the smallest useful expression changes under the sentence construction rules while preserving the technical invariants.
4. Compare the edited candidate with the draft: action ownership and objects, condition scope and logical force, ordering, negation, certainty and results, then protected literals and structure. Revert any expression change that alters an invariant or reaches beyond the allowed scope.
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
