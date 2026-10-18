# Library state and delivery

This reference owns the state vocabulary, paths and exclusions, configuration, manifest and attempt protocols, coverage and validation status, reuse, conflicts, and delivery.

## State vocabulary

| Term | Meaning |
|---|---|
| Confirmed collection | The official outputs recorded by the current manifest; replaced only by a complete, checked delivery |
| Managed output | A path the manifest owns: a document key, a card path, or a validated active or retained figure pair |
| Candidate | A new or revised output that has not passed collection checks; kept in run paths when retained |
| Retained | Candidates, recovery copies, or figure files deliberately kept for continuation or recovery; they carry no evidence or publication status |
| Pending | Declared scope, modules, topics, or required figures not yet finished; blocks complete coverage |
| Deferred | An optional figure deliberately left out of the official collection under the conditions in diagrams.md; not pending source scope |
| Partial | `coverage_status` when declared scope is not fully addressed |
| Stale | A card whose support is missing, conflicting, or uncheckable |
| Retired | A card whose concept current evidence shows is no longer used; identity and history are kept |

## Scope and paths

The fixed output root is `docs/official/`; official Markdown is flat, with `README.md` as navigation. Every generated JSON file is under `.cards/`. Cards are directly `.cards/k_<uuid>.json`. Reserve `.cards/manifest.json`, optional `.cards/config.json`, and `.cards/last_attempt.json` for their stated purposes.

Read original first-party code, configuration, tests, and project documents. Exclude the whole output subtree and `docs/assets/km/`, including staging and retained generation material, from factual input. Original assets outside the generated roots remain input; inspect unowned occupied output paths as conflicts. Also exclude VCS internals, dependencies, build products, caches, backups, obvious secrets, and symlinks outside the target. The rest of `docs/` stays in scope. Inspect uncommitted and relevant untracked files; a non-Git project is supported through actual file reading and comparison.

No-change decisions require reliable evidence about current sources, effective configuration, workflow rules, and managed outputs; an unchanged commit, timestamp, or run record alone is insufficient. An architecture or coverage inventory is not deep source analysis.

## Optional configuration

Initial use requires no configuration file. If `.cards/config.json` exists, read it as preferences, not factual evidence. Protocol `schema_version` is `1.0`. Supported preferences are:

- `source_roots`: project-root-relative scope paths, default `["."]`.
- `exclude`: additional project-root-relative paths or patterns, default `[]`; interpret using existing host search capabilities and explain actual exclusions.
- `document_language`: default `zh-CN`; filenames and output paths retain this skill's fixed contract unless the user explicitly changes that contract.
- `writing_preferences`: a string array, default `[]`, subordinate to facts and technical invariants.

Keep defaults in `effective_config` without creating a configuration file. Reject malformed, unknown, or unsupported settings before applying them. Preferences cannot expand access outside the project, override source exclusions protecting secrets, change ownership, or authorize commands. Explain a narrowed scope accurately; do not call it whole-project coverage.

## Manifest protocol 2.0

The confirmed manifest records the last confirmed collection. Update it last after writes and checks. The following is a structural example with empty collections, not evidence of a successful run:

```json
{
  "schema_version": "2.0",
  "skill_version": "0.1.0",
  "workflow_version": "2.0",
  "project": {"name": "example-project"},
  "library_revision": 1,
  "effective_config": {
    "source_roots": ["."], "exclude": [],
    "document_language": "zh-CN", "writing_preferences": []
  },
  "coverage": {"status": "complete", "scope": ["."], "reviewed_paths": [], "excluded": [], "pending": []},
  "documents": {},
  "cards": {},
  "figures": {},
  "sources": {},
  "verification_batches": {}
}
```

| Field | Contract |
|---|---|
| `project` | Actual project name and optional safe identity information; no credential-bearing remote URLs |
| `library_revision` | Positive integer, incremented only when confirmed knowledge content or its references change |
| `coverage` | Actual declared scope, reviewed paths, exclusions with reasons, and pending work; confirmed collection requires `complete` and no pending scope |
| `documents` | Object keyed by document-root-relative Markdown path; each record has `source_paths`, derived `card_ids`, derived `figure_ids`, and `verified_in` |
| `cards` | Object keyed by stable card ID; each record has `path`, `source_paths`, `verified_in`, and optional `issues` |
| `figures` | Stable figure IDs and their SVG/list paths, article uses, source paths, actual hashes and checks under [diagram-state.md](diagram-state.md) |
| `sources` | Object keyed by project-root-relative original source path or consulted URL; each record has `kind`, `available`, and `last_read_in` |
| `verification_batches` | Object keyed by actual run ID; each batch has `checked_at`, `reviewed_paths`, and actual `checks` |

Ownership is limited to `documents` keys, `cards[*].path`, validated active/retained figure pairs under [diagram-state.md](diagram-state.md), and recognized state files. These paths must stay within their stated document, card or figure roots; state cannot grant authority over arbitrary project paths. Document `card_ids` must agree with cards' article bindings. Card and document source paths must resolve in `sources`, and verification references must resolve in `verification_batches`. A delivered collection needs `README.md` and the actual applicable content, not just an empty manifest.

Records can include `content_hash: {algorithm, value}` only when an actual tool computed that hash for the specific current content. Use a known supported algorithm such as `sha256`, and preserve what was hashed. Source availability can be false for recorded historical evidence; expose current evidence gaps. Retain batches referenced by current records; full snapshot history is not required.

Verification metadata can advance when content remains unchanged, without changing the knowledge revision or article dates. Keep content hashes independent of volatile attempt timestamps. Do not treat configuration, attempt records, or retained candidates changing as knowledge changes by themselves. If workflow or preferences changed, reassess their effect rather than automatically rewriting everything.

## Coverage and attempt protocol 2.0

Keep `coverage_status` (`complete` or `partial`) separate from `validation_status` (`passed`, `failed`, or `not_run`). Complete means the declared scope was actually addressed, not necessarily the whole project. Passed means the listed required checks were performed and passed, not production runtime acceptance or deterministic AI correctness.

Write `.cards/last_attempt.json` with `schema_version` set to `2.0`, `run_id`, actual `started_at`, both statuses, `published` (boolean), `reviewed_paths`, `excluded`, `pending`, `conflicts`, `candidate_paths`, `written_paths`, and `checks`, plus `deferred_figures` (empty when none). Official-collection checks and candidate checks follow diagram-state.md, including required/optional scope. Each check records `name`, `method`, `result` (`passed`, `failed`, or `not_run`), and actual `evidence`. Timestamps and IDs come from host observations or clearly identified host run context.

The attempt record may change on a no-change run. It describes work done and is not the confirmed manifest. Unknown or incompatible state versions are conflicts: leave them untouched. This release has no migration or legacy conversion. Term cards/configuration use their own 1.0 contracts, not the manifest version.

When retention is needed, put Markdown candidates and available recovery copies under `.staging/<run_id>/` and JSON candidates or review records under `.cards/runs/<run_id>/`. Use fresh unoccupied run paths; create them only when needed. Pending records should identify completed topics, unread or unfinished scope, reasons, actual writes, and candidate entrypoints. Do not silently clean retained run data.

For unfinished module work, retain `.cards/runs/<run_id>/document-plan.json` and include its path in `candidate_paths`. The working plan has `modules` records with `name`, `responsibility`, `source_paths`, `main_article`, `topic_articles`, and `pending`; `cross_module_articles` records with `path`, participating `modules`, and `source_paths`; and `recognition_pending` for unresolved source or boundary questions. Article paths are document-root relative. These are retained planning notes, not new module identities or an executable state machine; no new manifest fields are required.

On continuation, read that plan as prior working state, recheck its original evidence, and reconcile it with actual candidates and remaining scope. A missing main design, unfinished necessary topic, or unresolved recognition gap prevents complete coverage. Do not rebuild the plan only from existing output files or omit unfinished work. Apply current requirements on repeat invocations of this protocol.

Retain diagram plans, SVG/JSON candidates and trusted recovery material using [diagram-state.md](diagram-state.md).

## Reuse, conflicts, and publication

1. Recover an interrupted attempt before using a no-change shortcut. Compare actual files with the prior manifest and write record, since the old confirmed set may no longer be intact.
2. Compare each managed output with a reliable prior baseline, such as its recorded tool hash, an actual version-history original, or a retained confirmed copy. A timestamp or regenerated plausible text does not prove the file lacks external edits. Without a reliable comparison, preserve existing files and report the uncertainty before replacement.
3. An unowned target path, unknown state file, or externally modified managed output blocks formal replacement for the whole attempted collection. Do not absorb those edits as new project evidence, invent a manual-merge workflow, or silently switch output roots. Preserve candidates if useful.
4. Require complete coverage, passed required checks, and no known blocking conflicts before replacement. Immediately before writing, reinspect critical original sources and recheck managed outputs' ownership and hashes; changed input returns to impact analysis. Continuous changes or inadequate tools leave the run incomplete.
5. Write only the planned new unoccupied or verified managed targets. If obsolete managed files must be removed, verify ownership, the reason, and repaired incoming references first; preserve card identities and historical evidence under their freshness rules. Original project assets are read-only for this task.
6. Recheck written files and their associations, then update the confirmed manifest. Set `published` true only when actual content delivery occurred and the intended confirmed set is consistent. A verified no-change run has `published` false.
7. If writes fail or are interrupted, stop further replacement and record actual written and pending paths. Do not advance the manifest to a successful revision. On the next invocation inspect the mixed set and continue or restore only from a trustworthy available original.

No lock, filesystem snapshot, atomic multi-file transaction, automatic rollback, complete secret detector, or universal concurrent-write detector is provided. Use available host capabilities as actual evidence without claiming those guarantees. If the attempt record itself cannot be written safely, report that limitation directly.
