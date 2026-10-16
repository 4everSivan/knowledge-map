# Static engineering figure style

Start from [the SVG base](../../assets/diagrams/base.svg). Resolve title, description, figure-prefixed IDs and content; the empty template is not a finished figure. Use Chinese labels by default while preserving actual identifier spelling.

Use a light opaque background (`#ffffff`), ink (`#243247`), secondary ink (`#516176`), border (`#768397`), and one focal accent (`#a13b22`). Color is emphasis, not the only carrier of meaning. Use distinct shape, text or line treatment for meaningful differences. Prefer hairlines, modest corners and whitespace; no shadows or decorative effects. Prefer one or two focal items.

Use local system sans fonts with Chinese fallbacks, as in the template. Technical literals may use local monospace, with a CJK fallback. Do not fetch or embed remote fonts. Start labels near 16px, subordinate text near 14px, then actually inspect them at the intended Markdown width. These are starting sizes, not proof of readability. Wrap with explicit `tspan` lines or increase boxes; do not shrink away necessary conditions.

Align structural geometry to a 4px grid when practical. Aim for at most nine engineering nodes and twelve relations in one view; sequence diagrams preferably use at most five actors. These are split prompts, not authority to remove necessary semantics. Prefer an overview plus bounded detail, with disclosed entry/exit and scope.

Route off-axis connectors orthogonally, with rounded elbows and separate attach points. Keep labels clear of connectors and use opaque label masks. Offset shared routes; mark unavoidable crossings clearly without suggesting a junction. Route around unrelated nodes. Paint zones first, connectors next and nodes/text last, checking that masks do not hide later nodes. A semantic relation's group contains its actual connector and label.

## SVG subset and mapping

Use standalone XML SVG with positive `viewBox` dimensions and local style. Root `role="img"` and `aria-labelledby` resolve to a first-child `title` and following `desc`; both describe the subject and meaning. All XML IDs are figure-prefixed and unique. Include a scope/target/configuration caption in the article and image when it affects interpretation.

Allowed elements: `svg`, `title`, `desc`, `defs`, `style`, `g`, `rect`, `circle`, `ellipse`, `line`, `polyline`, `polygon`, `path`, `text`, `tspan`, and `marker`. Use local `url(#id)` only for marker references; no external URLs, imports, links, images, scripts, event attributes, `foreignObject`, embedded HTML, animation or executable CSS. No XML entities/DOCTYPE. Keep geometry in attributes; no hidden, off-canvas or scripted engineering content. Put each engineering element in one group with its matching `data-node-id`, `data-relation-id`, or `data-group-id`. Grouping zones are not extra semantic nodes.

Check resolving markers and accessible names, unique IDs, finite geometry, visible arrow endpoints, labels, masks and borders. XML validity alone does not establish paint bounds or meaning. Inspect the SVG and actual Markdown rendering, including Chinese and the article's normal width. Keep essential explanations in prose and meaningful image alt text; no viewer-specific HTML layout is required in the document.
