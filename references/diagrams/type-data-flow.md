# Data flow

Show data origins, transformations, stores and destinations. An arrow means movement or derivation of data, not an implicit call or chronological control step.

## Semantic fields

Node roles: `source`, `process`, `store`, `sink`, `external`. Relation kinds: `transfers`, `derives`, `persists`. Each relation has properties `data` (nonempty string naming the actual payload or data category). Optional node property: `transformation` (supported string). Optional group kinds: `system_boundary`, `trust_boundary`.

## Draw and check

Keep a dominant lineage direction. Label data and transformations precisely; distinguish a write from a read and a copy from a new derived dataset. Show meaningful boundaries with evidence. Do not invent volumes, latency, retention or delivery guarantees. When multiple control steps move the same data, explain them in an appropriate flow/sequence view instead of overloading lineage arrows. Clarify omitted branches and link necessary detail.
