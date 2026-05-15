# Knowledge

Strategy, research, and reference material. The "why" behind what the team builds.

## Doc index

- `strategy/README.md`: current strategic priorities and the reasoning behind them. One file per priority deep-dive or quarterly refresh as needed.
- `competition/README.md`: who you're up against, what they do well, and what wedge you're driving. One file per competitor for deep dives.
- `user-research/README.md`: research synthesis, personas, and recurring patterns from customer conversations. One file per discrete study.
- `metrics-framework.md`: your metrics tree. North star, leading indicators, guardrails.
- `prds/README.md`: optional. Where PRD drafts live if you want a local markdown trail. The `/prd` skill exports to Linear by default.

## When to add a doc here

If it's evergreen reference material the team revisits, it goes here. Examples:

- A new strategic priority → update `strategy/README.md`, or add a `<priority-slug>.md` deep dive in `strategy/`.
- A new competitor or a meaningful shift in an existing one → update the table in `competition/README.md`, or add a `<competitor-slug>.md` profile.
- A pattern from research interviews → update `user-research/README.md`, or add a `{{YYYY-MM}}-<topic>.md` study writeup.
- A new metric definition → update `metrics-framework.md` and cross-link from `analytics/metrics.md`.

If it's about a specific customer, it lives in `customers/`. If it's a number or query, it lives in `analytics/`.

## Style

Strategy and competitive intel rot fast. Date the last meaningful update at the top of each file. If a file hasn't been touched in six months, the owner should re-read and either confirm or update.
