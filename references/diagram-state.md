# Figure protocol and collection state

## Versions and paths

The current manifest, attempt record, and workflow description use protocol `2.0`. Figure semantic lists use `1.0`; terminology cards and optional configuration keep their independent `1.0` contracts. The skill release remains `0.1.0`. There is no legacy-library migration or conversion. Refuse unsupported state without overwriting it.

Each figure ID is `d_<uuid>` obtained from a host UUID tool. Reuse it for the same logical figure across updates. Node, relation and group IDs are nonempty stable local slugs, unique across those three collections. Evidence keys are stable local slugs in a separate namespace. Do not derive identity from a timestamp, line number, label or layout. Figure titles and labels follow the document language.

| Field or artifact | Path base and constraints |
|---|---|
| Official SVG | Project-root relative, exactly `docs/assets/km/<semantic-lowercase-hyphen-name>.svg` |
| Semantic list | Project-root relative, exactly `docs/official/.cards/diagrams/<figure_id>.json` |
| `owner_article`, `article_paths`, plan article uses | Document-root relative, flat Markdown paths under `docs/official/` |
| Evidence `path` | Project-root-relative original source or a consulted authoritative URL, resolving in manifest `sources` |
| SVG candidates/recovery copies | `docs/assets/km/.staging/<run_id>/`; fresh run paths only |
| JSON candidates, plans and review receipts | `docs/official/.cards/runs/<run_id>/` |

SVG references in Markdown are article-relative, normally `../assets/km/<name>.svg`. Do not mix this base with JSON path fields. Reject `..` escapes, external symlinks, collisions, and authority granted by arbitrary state paths. Reserve the SVG output subtree for generation and exclude it and `.cards/` candidates from factual input. Check unowned existing content as a conflict, not as permission to overwrite. Original assets elsewhere remain evidence and read-only.

## Semantic list 1.0

Required top-level fields are `schema_version`, `id`, `title`, `type`, `view`, `nodes`, `relations`, and `evidence`. Optional `groups` contains semantic boundaries, not visual layout. Reject unknown fields and unsupported enum values rather than silently interpreting them.

- `type`: `architecture`, `flowchart`, `sequence`, `state`, `data_flow`, `er`, `deployment`, or `dependency`.
- `view`: `implementation` or `target`. Configuration declarations belong in a clearly captioned implementation view; their evidence kind stays declaration. Do not represent them as runtime observations.
- Node: `id`, `label`, `role`, nonempty `evidence_refs`; optional `group_id` and `properties` as defined by the selected type.
- Relation: `id`, `from`, `to`, `kind`, nonempty `evidence_refs`; optional `label`, `condition`, and type-specific `properties`. Endpoints must resolve to nodes, including legitimate self-transitions. All relation semantics need support.
- Group: `id`, `label`, `kind`, nonempty `evidence_refs`; optional `parent_id`. Group nesting must be acyclic and resolve; every node's group must exist.
- `evidence`: object keyed by local evidence ID. Each value has `path`, `locator` (a supported symbol, config key, section or observed artifact position), `kind`, and `supports` (what this source establishes). Optional `lines` is a current navigation hint, not identity. Kinds are `static_implementation`, `original_declaration`, `inference`, `runtime_observation`. Explain an inference's basis in `supports`; a runtime observation needs actual observed original evidence. Generated lists/images/prose cannot support an engineering assertion on their own.

Every `evidence_refs` value must resolve, with original evidence supporting all associated properties. Unavailable evidence stays a truthful gap; an entry's presence is not support. A node or relation can share an evidence entry. Labels, locators, support explanations, guards and string properties are nonempty strings when present; references are arrays of unique IDs. Optional properties are omitted when not applicable; do not guess values. Required unknown facts return to reading or remain pending. Purely decorative legends, masks and path bends do not belong in the list.

Example shape only, not project evidence:

```json
{
  "schema_version": "1.0",
  "id": "d_00000000-0000-4000-8000-000000000001",
  "title": "Example dependency",
  "type": "dependency",
  "view": "implementation",
  "nodes": [
    {"id": "consumer", "label": "Consumer", "role": "module", "evidence_refs": ["source"]},
    {"id": "provider", "label": "Provider", "role": "module", "evidence_refs": ["source"]}
  ],
  "relations": [
    {"id": "uses", "from": "consumer", "to": "provider", "kind": "depends_on", "evidence_refs": ["source"]}
  ],
  "evidence": {
    "source": {"path": "example/consumer.py", "locator": "Consumer.run", "kind": "static_implementation", "supports": "The original declaration and call establish these modules and this dependency."}
  }
}
```

No coordinates, styling, hashes, verification timestamps or environment versions belong in this list. SVG groups use stable `data-*` IDs from the list and XML IDs prefixed with the figure ID; title, description and marker IDs are prefixed too.

## Manifest 2.0 additions

Keep the document/card/source/batch contracts in [library-state.md](library-state.md). Add required `figures: {}` even when no figure is applicable. Each figure-keyed record has:

| Field | Contract |
|---|---|
| `svg_path`, `semantic_path` | The project-root-relative paths above |
| `owner_article` | One actual article, included in `article_paths` |
| `article_paths` | All current image uses, sorted and unique; nonempty |
| `source_paths` | Union of original evidence paths, resolving in `sources` |
| `verified_in` | Existing batch with actual checks for this figure |
| `content_hashes` | `svg` and `semantic`, each `{algorithm, value}` from an actual tool over exact delivered bytes |

Document records add `figure_ids`, exactly matching their image uses. Figure ID, list ID, paths, reverse article bindings, source sets and hashes must agree. Both figure paths join managed ownership only within fixed roots. Do not interpret other JSON as term cards. Configuration cannot change these roots.

Optional `retained_figures` records track already-owned SVG/list files removed from active use but deliberately kept for continuation/recovery. Each record has figure `id`, `svg_path`, `semantic_path`, actual `content_hashes`, `reason`, and `retained_in` batch. They grant no active publication or evidence status, have no active image uses, and cannot duplicate an active path. Establish the record before dropping active ownership. Recovery candidates are recorded in attempts, not silently adopted. If removing files instead, first verify ownership, applicable current/historical references, and recovery material; record actual removals in the attempt. Never clean originals or `local/`.

## Run plan and attempts 2.0

Retain `.cards/runs/<run_id>/diagram-plan.json` when work is pending/deferred or needed for review. Its `figures` array records `id`, `type`, `view`, planned paths, `owner_article`, `uses` (`article`, `required`, `reason`, `trigger`, `evidence_refs`), and `pending`. A shared figure is required if any use is required. Triggers are `module_relationships`, `complex_interactions`, `business_states`, or `reader_need`; reasons must be source-grounded. Unknown recognition or required semantic facts are source/required work, not optional decoration. Link the plan in attempt `candidate_paths` when retained; recheck it on continuation.

Attempts retain the normal fields and add `deferred_figures` (array, empty when none). Each deferred record has `id`, `reason`, available candidate paths, and `remaining_work`. Keep these separate from required/source `pending`. Include retained SVG copies and actual written/removed paths in the existing write record.

Checks have `name`, `method`, `result`, `evidence`, plus `required` (boolean), `scope` (`official_collection` or `candidate`) and optional `figure_ids`. Mark a check required from the plan before its result is known. A candidate failure remains failed even when that optional figure is excluded. Required official checks determine overall validation. Unfinished required work prevents confirmation; deferring an optional drawing cannot conceal unread evidence or incomplete necessary prose.

Rendering check evidence identifies viewer/tool, actually observed environment, article paths, figure hashes, inspected results and available captured-artifact paths. Reuse names an existing check and applicable conditions, and is recorded as reuse rather than a fabricated fresh rendering. Do not invent unavailable versions or artifacts.

## Delivery and continuation

Plan all articles, cards, semantic lists, SVGs, active/retained records and retirements as one collection. Recheck critical source and managed hashes immediately before writing. Optional figures can be excluded only after repairing all uses and ensuring the remaining prose and official checks are complete. Preserve their candidate checks and deferred plan. Otherwise retain candidates and the confirmed collection.

Verify actual written bytes and associations, then write the manifest last. Interrupted writes record the actual mixed set and never claim a successful revision; inspect it first on repeat invocation. Use trustworthy recovery material if available. This is not a multi-file transaction, locking service, automatic rollback or legacy migration.
