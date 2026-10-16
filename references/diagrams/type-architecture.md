# Architecture

Show supported components and their responsibility, dependency or trust boundaries. Keep one dominant direction and distinguish external systems and stores. Do not imply runtime wiring from co-location of files.

## Semantic fields

Node roles: `actor`, `component`, `store`, `external`. Relation kinds: `calls`, `reads`, `writes`, `publishes`, `depends_on`. Optional node properties: `responsibility` (string). Group kinds: `layer`, `trust_boundary`, `system_boundary`; groups can nest through `parent_id` with original support. No other type properties.

## Draw and check

Use labelled zones behind components. Put connectors on distinct ports; route orthogonally around unrelated boxes. Draw actual direction and label contracts where meaningful. Briefly disclose abstraction scope and link to module details. Grouping is semantic and needs evidence, not just a way to fit a canvas. Split large views without hiding necessary modules or boundary crossings. Check that static design relationships are not described as observed operation.
