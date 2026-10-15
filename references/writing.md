# Production document writing

## Library and page form

Write Chinese prose by default. Put official Markdown directly in `docs/official/`. Use semantic Chinese filenames without ordering prefixes, dates, or revision labels. Keep actual product names and identifiers. `README.md` is the navigation exception; use it as the reader's entrypoint, grouped by actual reader tasks rather than source directories. Generate only applicable pages.

Use one H1 per page, followed by a short introduction and any scope that affects understanding. Use continuous heading levels, usually H2 and H3, without section numbers or decorative icons. The H1 and filename must describe the same topic. Task headings use actions; concept headings name the concept. Keep stable filenames across ordinary updates.

Use a normal Markdown link table of contents for long pages when useful. Do not use `[TOC]`, theme-specific components, or HTML layout. For lasting section references use an explicit stable anchor, such as `<a id="retry-policy"></a>`, and verify it exists. If an explicit anchor is unnecessary or unsupported, bind the whole article rather than guessing a renderer's slug.

Keep one meaningful last-update date per article. Change it only when content or references change substantively, not whenever a scan runs. Keep run IDs, coverage counts, hashes, and verification timestamps in `.cards/`. Link related reading when it helps the reader continue; do not manufacture previous/next sequences.

## Choose and trim an outline

These are choices, not mandatory files or empty chapter templates. Pick the reader's purpose, then omit topics without applicable evidence. Split pages only when reader tasks or scale justify it.

| Document type | Suggested progression |
|---|---|
| Overall system design | Purpose; boundary and external interactions; structure; module collaboration; key scenarios; data and state; constraints |
| Module design | Responsibilities and limits; interfaces and dependencies; internal structure; mechanisms; failures and constraints |
| Internal workflow | Entrypoint and trigger; participants; normal path; branches and states; errors, shutdown, and recovery |
| Operation guide | Goal; applicable conditions and preparation; ordered actions; result checks; failure handling |
| Quick start | Expected outcome; minimum preparation; one complete supported experience; completion check; next reading |
| Configuration or API reference | Scope; common rules; consistent entries; examples; constraints and errors |
| Troubleshooting | Symptom; evidence gathering; distinguish causes; supported treatment; recovery check |
| Glossary | Domain or concept groups; meaning; project context; boundaries and related reading |

Configuration entries describe actual name, type, default, allowed values, precedence, and activation timing as applicable. API entries describe actual inputs, outputs, errors, and constraints. Do not invent missing defaults. Explain shared rules once. Separate mechanisms such as service startup flow from human operations such as starting a service.

## Prose and Markdown elements

State the needed conclusion or relationship early, then explain reasons, boundaries, and exceptions. Use concrete actors and direct verbs. Keep terms consistent instead of varying technical synonyms. Explain abbreviations only when the expansion is supported.

| Element | Use |
|---|---|
| Paragraph | Connected explanation of responsibility, causality, or boundary |
| Unordered list | Parallel roles, conditions, or independent notes |
| Ordered list | Actions whose order matters; include position and checks when needed |
| Table | Comparable parameters, fields, or conditions; move long prose outside cells |
| Fenced block | Actual code, commands, configuration, or output; label the language and explain context |
| Inline code | Identifiers, paths, arguments, and enumerations |
| Quote with a label | A useful note or concrete risk; put prerequisites before the affected action |
| Diagram | Relationships, sequences, or states that become clearer visually |

Keep commands grounded in actual project entrypoints or original operating instructions. Explain placeholders and never fill them with real secrets. Label expected output as expected; observed output requires an actual run and its environment. Writing instructions does not authorize running the project's service, deployment, tests, or external operations.

Mermaid can help readers whose viewer supports it. Preserve the important relationships in surrounding prose and do not require a renderer or website. Use diagrams only when they improve understanding.

## Evidence and limitations

Explain behavior first, then add short source notes near the supported group of claims. Use original project paths, symbols, explicit document anchors, or consulted authoritative URLs. A source list without a support relationship is insufficient.

Markdown links are relative to the current article. A link from an official page to a root-level source therefore needs the corresponding relative path, whereas a card's `sources.path` is project-root relative. Do not mix these bases. Line numbers aid current navigation but are not identities.

Distinguish static implementation, original document declarations, inference, runtime observations, and human acceptance. Never infer historical design motives from current code. Preserve relevant uncertainty and disagreements near the claim. Unread material is not evidence of absence. Missing information should have a concrete reason and effect, not empty chapters or repeated placeholders.

Keep repeated explanations focused on the page's context and link to the principal explanation. Render terminology naturally in a glossary rather than exposing JSON management fields. Check names, shared contracts, sources, and card meanings across pages before official delivery.
