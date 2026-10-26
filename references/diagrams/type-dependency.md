# Dependency

Show consumers depending on providers, including shared dependencies or cycles where relevant. This view may be a simple graph; do not require invented fan-in or a cycle to justify it.

## Semantic fields

Node roles: `module`, `package`, `service`, `external`. Relation kind: `depends_on`, directed from consumer to provider. Use common `condition` for an applicable conditional dependency; no type-specific relation properties. Optional node property: `version` (supported string). No groups.

## Draw and check

Use ranked rows or columns with a declared direction. Route feedback edges outside the primary stack and label actual cycles. Fan-in counts, if displayed, must be computed from the scoped relations, not invented. Distinguish build/import dependencies from runtime calls in the caption and evidence. Do not make each file a business module. State aggregation and omitted detail, explaining necessary dependencies here or through in-page references; a clipped or unshown cycle is not an acyclic graph. Prefer one clear focus, but preserve all necessary scoped dependencies across overview/detail views.
