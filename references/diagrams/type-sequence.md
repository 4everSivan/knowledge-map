# Sequence

Show ordered interaction between actors. Keep time top-down and actors on lifelines. Scope one complete scenario or a clearly labelled conditional variant.

## Semantic fields

Node roles: `actor`, `service`, `store`, `external`. Relation kinds: `sync_call`, `return`, `async_message`. Every relation has properties `order` (unique positive integer within the figure); optional `scenario` and `repeat` strings describe source-supported branching or repetition. Optional `condition` preserves the guard. No node properties or groups. These ordered semantic records are not layout coordinates.

## Draw and check

Calls use solid filled arrowheads, returns dashed filled arrowheads, async messages dashed open arrowheads. Include a legend when needed. Use activation intervals only when supported and actually relevant. Label conditional/loop regions with their scenario and guard; split deep or conflicting branches rather than pretending alternative messages all run in sequence. Self-calls stay on their actor. Check that every arrow's order, direction and mode match its record, and that returns do not appear to be independent requests. Prefer at most five lifelines per view; use a backbone and separate exceptional scenarios when necessary.
