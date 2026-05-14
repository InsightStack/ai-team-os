# PRDs

Optional folder. Where PRD drafts live if your team wants a local markdown trail.

## How the `/prd` skill writes here

The `/prd` skill at `.claude/skills/prd/` defaults to exporting to Linear and keeping a local draft at `.claude/prd-drafts/<slug>.md` while in progress. If your team wants final PRDs in this folder too, ask Cowork to copy from `.claude/prd-drafts/` to `knowledge/prds/` when the PRD is approved.

## Doc index

- `<feature-slug>.md`: one PRD per feature.

## Filename format

`kebab-case-feature-name.md`. Match the Linear project slug if there is one.

## What good looks like

See `EXAMPLES.md` at the root for an example PRD opening. The full template the `/prd` skill follows lives in `.claude/skills/prd/TEMPLATE.md`.
