# Metrics framework

{{REPLACE: your metrics tree. The one number that matters, the leading indicators that move first, and the guardrails you won't regress.}}

**Last meaningful update:** {{YYYY-MM-DD}}

## North star

{{The single number you optimize for. One line. Plus current baseline and target.}}

**Current baseline:** {{value}} ({{as of date}})
**Target:** {{value}} ({{by date}})

## Leading indicators

Metrics that move before the north star does. Track these weekly.

| Metric | Definition | Why it leads | Where it's measured |
|---|---|---|---|
| {{Name}} | {{One-sentence definition}} | {{One sentence}} | {{Dashboard or query}} |
| {{Name}} | {{Definition}} | {{One sentence}} | {{Where}} |

## Guardrails

Metrics we don't want to regress, even if doing so would move the north star.

| Metric | Why it matters | Threshold |
|---|---|---|
| {{Name}} | {{One sentence}} | {{e.g., below X is concerning, below Y is escalation}} |

## How this connects to strategy

Every priority in `strategy/README.md` should map to a metric here. If it doesn't, either the priority isn't measurable or the framework is missing something.

For the underlying SQL and dashboards, see `../analytics/`.
