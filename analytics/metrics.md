# Metrics

{{REPLACE: definitions for the metrics your team uses. One section per feature or product area. Cross-link to dashboards and queries.}}

The metrics tree (north star, leading indicators, guardrails) lives in `../knowledge/metrics-framework.md`. This file is the per-feature breakdown.

## Conventions

- Each metric gets: name, one-line definition, computation, source, and owner.
- If two people would compute the metric differently from your definition, tighten it.
- Cross-link to the query in `queries/` and the dashboard in `dashboards.md`.

## {{Feature area 1}}

### {{Metric name}}

- **Definition:** {{One sentence}}
- **Computation:** {{Formula or SQL pointer}}
- **Source:** {{Data warehouse table, event name, or system of record}}
- **Owner:** {{Name}}
- **Dashboard:** {{Link in `dashboards.md`}}
- **Query:** `queries/{{filename}}.sql`

### {{Metric name}}

{{Same shape.}}

## {{Feature area 2}}

{{Same shape.}}
