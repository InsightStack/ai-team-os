# Team OS navigation

This is the navigation hub for the team's shared knowledge folder. When working with this OS, traverse the structure below to find what you need. Each folder has its own `README.md` doc index that lists what lives there.

## Doc index

- `team/README.md`: team roster, onboarding, rituals.
- `customers/README.md`: per-customer summaries and contacts. Read summaries first; load full transcripts only when needed.
- `knowledge/README.md`: strategy, competitive intel, user research, metrics framework, optional PRD drafts.
- `analytics/README.md`: metric definitions, dashboards, saved queries, playbooks, business reviews.
- `.claude/skills/`: shared skills. See the Skills section below for the full list and exact paths.

## Skills

Shared skills shipped with this OS. In Cowork chat, invoke a skill by asking for it in plain language, for example "run the prd skill" (the slash-command UX requires a plugin and isn't wired up yet; Cowork registers slash commands from installed plugins only, not from this workspace's `.claude/skills/`). In Claude Code CLI, `/<name>` works directly. The slash form below is the skill's identifier, not a typeable shortcut. Read the linked `SKILL.md` for the full spec.

- `/prd`: [.claude/skills/prd/SKILL.md](.claude/skills/prd/SKILL.md). Author a PRD and export it to Linear as a project with milestones and issues.
- `/hydrate-knowledge`: [.claude/skills/hydrate-knowledge/SKILL.md](.claude/skills/hydrate-knowledge/SKILL.md). Bootstrap this Team OS from connected tools (Drive, Gmail, Calendar, Slack, etc.).

Note for Claude: `.claude/` is a dot-prefixed directory. `Glob` and most globbers skip hidden paths by default, so `.claude/**` queries return nothing even when the files exist. To enumerate skills, use `ls -la .claude/skills/` or `find .claude/skills -name SKILL.md` via Bash. To read one, open its `SKILL.md` path directly with the `Read` tool; do not try to discover it via `Glob` first.

When adding a new skill under `.claude/skills/<name>/`, append one bullet to this section pointing at its `SKILL.md`. The list above is the canonical index.

## Team roster

{{TBD: ask Claude to run the hydrate-knowledge skill, or edit `team/roster.md` directly.}}

## Communication channels

{{TBD: Slack channels, group threads, or other primary comms. Ask Claude to run the hydrate-knowledge skill, or edit here directly.}}

## Style rules (apply to all writing produced for this OS)

- Plain language, terse, direct.
- No em dashes. Use commas, periods, semicolons, or colons.
- No emojis unless the user explicitly asks.
- Cite sources when making product claims. Mark gaps as `{{TBD}}` rather than guessing.
- Wait for explicit user approval before writing to external systems (Linear, Slack, etc.).

## When in doubt

If a question spans multiple folders, start at the relevant folder's `README.md`. If the answer isn't there, the doc index is stale: update it.
