# Analytics

Metric definitions, dashboards, saved queries, playbooks, and periodic business reviews.

## Doc index

- `metrics.md`: metric definitions tied to features. The "what" each metric means and how it's computed.
- `dashboards.md`: links to live dashboards.
- `queries/README.md`: saved SQL or query snippets organized by feature area.
- `playbooks/README.md`: how-to guides for recurring analyses ("how to debug a drop in activation," "how to read the weekly cohort chart").
- `business-reviews/README.md`: periodic reviews (weekly, monthly, quarterly).

## When to add here

A new metric, dashboard, query, or analysis playbook goes here. Things that don't go here:

- A customer-specific data pull → goes in that customer's folder under `customers/`.
- A strategic interpretation of metrics → goes in `knowledge/strategy.md` or a relevant doc.
- The metrics tree itself (north star + leading indicators + guardrails) lives in `knowledge/metrics-framework.md`. Cross-link from `metrics.md` here, don't duplicate.

## Style

Keep metric definitions short and unambiguous. If two people on the team would compute a metric differently from your definition, the definition is too loose.
