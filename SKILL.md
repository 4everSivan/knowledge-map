---
name: km
description: Generate or refresh a source-grounded project knowledge library with Chinese Markdown and reusable terminology cards. Use when the user invokes $km, requests /km in a compatible host, or asks to build or update production knowledge documents from project code and original documentation.
metadata:
  version: "0.1.0"
---

# Project knowledge library

Use [workflow.yaml](workflow.yaml) as the ordered procedure. It is an instruction document for the host AI, not an executable workflow engine. Follow the target project's applicable rules and use the host's existing search, file, comparison, and editing tools. Do not install an engine, generate helper scripts, or require another skill.

Resolve the target from the user's requested project, otherwise the current project directory. Resolve this skill's resource paths relative to this file, not the target directory. If the target cannot be identified, ask for its location before writing.

The user repeats the same invocation for initial generation and updates. Infer the appropriate path from actual sources and existing library state; do not make the user run internal phases.

## Output contract

- Put official Markdown directly in `docs/official/`, using Chinese semantic filenames and titles without numeric prefixes. The navigation exception is `README.md`.
- Put every generated JSON file under `docs/official/.cards/`, including lean term cards, the manifest, and attempt records. Keep temporary Markdown candidates under `.staging/<run_id>/` only when needed.
- Explain professional terms, abbreviations, and project-specific names in cards. Keep `definition` separate from `project_usage`; associate articles through `articles` and original evidence through `sources`.
- Build the overall architecture first, then read and draft by topic. Within each article, check content, edit expression, and recheck facts. For updates, edit changed passages and necessary context only; reuse valid unchanged documents.
- Treat generated content as output and comparison material, never independent evidence of project behavior. Preserve original assets and known conflicting outputs. Partial coverage or failed checks cannot replace the confirmed library.

## Resources

Read each reference at the workflow stage that uses it:

- [Library state](references/library-state.md): paths, configuration, ownership, coverage, manifest, recovery, and delivery.
- [Writing rules](references/writing.md): Chinese filenames, reader-oriented outlines, Markdown, and source presentation.
- [Authoring](references/authoring.md): new and updated articles, completion conditions, and return paths.
- [Technical editing](references/technical-editing.md): expression-only revision after content review.
- [Knowledge cards](references/knowledge-cards.md): term identity, JSON fields, evidence, articles, and freshness.

Report actual coverage, changes, checks, conflicts, and the document entrypoint. A host recognizing this skill as `km` can expose its supported invocation syntax; this file does not itself register a slash command.
