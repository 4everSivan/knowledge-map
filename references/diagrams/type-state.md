# State

Show one named subject's business states or evidenced object/resource lifecycle and permitted transitions. States can be encoded by fields or conditions rather than an enum. Distinguish them from execution steps, inter-actor messages and result codes that are not stored states.

## Semantic fields

Node roles: `initial`, `state`, `terminal`. Relation kind: `transition`; properties require `event` (nonempty string), optionally `action` (string). Use `condition` for an applicable guard; omit it only when no guard is supported or needed. No node properties or groups.

## Draw and check

Use labelled state boxes, a marked initial state and clearly distinguished terminal states. Label transitions as event, guard and applicable action. Preserve retry, cancellation, error and recovery semantics where present in the scoped behavior. Self-transitions need actual support. Do not merge states with different allowed operations just because labels seem similar. Avoid invented transitions to make all states reachable. Split complicated sublifecycles with explicit scope; review the full logical set even when split across views.
