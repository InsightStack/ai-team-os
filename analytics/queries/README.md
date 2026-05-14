# Queries

Saved SQL or query snippets, organized by feature area. The point of this folder is that nobody on the team should rewrite a non-trivial query from scratch.

## Doc index

- `{{feature-area}}/`: one folder per feature area or product surface.
- `{{feature-area}}/{{query-name}}.sql`: one query per file. Filename matches what the query answers.

## How to add a query

1. Pick the right folder. If you don't see one, create it.
2. Filename in kebab-case, describing what the query answers: `weekly-active-users-by-plan.sql`, not `query-1.sql`.
3. Add a header comment to the SQL file: a one-line description, source warehouse, last-validated date, and the metric in `../metrics.md` it backs.

## How to use a query

Read the header comment first. If the last-validated date is stale, run a quick sanity check before relying on the result.

## When a query is wrong

Don't silently fix it. Update the file, change the last-validated date, and note what changed at the top. That way the next person knows what they're looking at.
