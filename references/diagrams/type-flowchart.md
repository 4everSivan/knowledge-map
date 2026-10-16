# Flowchart

Show decision/control paths, not messages over time or data lineage. Limit each figure to an explicit scenario, with its starting condition, outcomes and applicable error paths.

## Semantic fields

Node roles: `entry`, `action`, `decision`, `exit`. Relation kind: `flow`. Every outgoing decision relation has a nonempty `condition` supported by source. No type properties or semantic groups.

## Draw and check

Use rounded start/end, rectangular actions and diamond decisions. Label every decision exit; do not rely on position or color for yes/no. Explicitly represent merge points only if they have engineering meaning; geometric join points are decoration. Preserve condition negation, bounds, else paths and termination. Prefer top-down control flow, with returns routed outside other nodes. Split tangled branches into a main view and bounded details with stated entry/exit. Never turn an unknown failure path into a success exit.
