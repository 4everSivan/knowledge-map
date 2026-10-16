# Entity relationships

Show logical entities and supported relationships. This type is not a claim of physical tables, SQL constraints or enforced foreign keys.

## Semantic fields

Node role: `entity`; optional properties `fields` is an array of objects with required `name` and optional `type` and `key` (`identifier` or `reference`). All shown fields need evidence. Relation kind: `association`; properties require `from_cardinality` and `to_cardinality` from `1`, `0..1`, `0..*`, `1..*`, or `unknown`. Unknown means explicitly not established, never an inferred many-side. No groups.

## Draw and check

Use entity headings and only relevant fields. Put cardinality beside each endpoint with a clear reading direction. Explain unknowns in the caption; required unresolved facts prevent complete scope. Do not infer uniqueness or nullability from one example. Distinguish domain declarations from implementation constraints. Avoid treating an ORM association or API field as proof of a database-enforced FK. Split by domain and retain cross-view references rather than omitting relationships silently.
