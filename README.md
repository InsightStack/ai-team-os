# AI Team OS

A shared knowledge folder your product team can drop into Google Drive, point Claude Cowork at, and use as the foundation for AI-assisted work.

Inspired by [Hannah Stulberg's Team OS pattern](https://github.com/in-the-weeds-hannah-stulberg/team-os-example-repo) and [Ayushman Jain's Product Management Claude Workspace](https://github.com/aupsy/Product-Management-Claude-Workspace-template), adapted for [Claude Cowork](https://claude.com/product/cowork) so non-developers can use it without touching a terminal.

## What this is

A folder structure plus two starter skills. The folders hold your team's shared context (strategy, customers, analytics, team rituals). The skills are reusable prompts Claude can run on top of that context.

When your whole team uses the same folder, Claude can answer questions, draft documents, and run recurring work without anyone re-explaining how your company operates. The folder is the memory. The skills are the workflows.

## Who this is for

Heads of Product and Product Managers who:

- Want their team to use AI more effectively but don't want to write code.
- Have Google Drive and Claude Cowork (or are willing to set them up).
- Are tired of being the bottleneck for context every time a teammate asks Claude something.

You do not need to be technical. The setup guide assumes you have never opened a terminal.

## 30-minute setup

1. Download this folder.
2. Place it in your shared Google Drive.
3. Install Claude Desktop and create a Cowork Project pointing at the folder.
4. Ask Claude to run the hydrate-knowledge skill to fill the placeholders with your real content.

Full walkthrough in [SETUP.md](./SETUP.md). Defines every term on first use.

## What's in this folder

```
team/         Onboarding, rituals, who's on the team.
customers/    One folder per customer with summaries and contacts.
knowledge/    Strategy, competitive intel, research, metrics framework.
analytics/    Metrics definitions, dashboards, saved queries, playbooks.
.claude/      Shared skills your team can use in Cowork.
```

Plus:

- `README.md` (this file)
- `CLAUDE.md`: the navigation hub Claude reads to understand the folder structure. Paste its contents into Cowork's folder-instructions panel during setup.
- `SETUP.md`: the 30-minute walkthrough.
- `MAINTENANCE.md`: how to keep the OS clean as your team adds things.
- `EXAMPLES.md`: clearly-labeled example snippets so you can see what filled-in content looks like. Delete this file once you replace the placeholders.

Every folder has its own `README.md` describing what lives there and how to use it. These per-folder READMEs are your **doc indexes**: they tell Claude (and your teammates) where to find what.

## The two starter skills

A **skill** is a reusable prompt Claude runs when you ask for it by name. Skills give Claude a consistent workflow for recurring tasks. In Cowork chat, invoke a skill by saying something like "run the prd skill" or one of its trigger phrases.

This template ships with two:

- **hydrate-knowledge**: runs once during setup. Reads whatever you have connected (Drive, Calendar, Gmail, Slack, etc.) and fills the placeholders in your OS with real content. You confirm every value before anything is written.
- **prd**: drafts a tight, evidence-backed PRD and exports it to Linear as a project with milestones and issues.

### About the prd skill

The example skill `prd` is built around two specific tools: [InsightStack](https://insightstack.com) for customer evidence and [Linear](https://linear.app) for shipping. We left it whole on purpose, a complete skill teaches more than a stripped-down one. If you don't use those tools, you can either swap the MCP calls for your equivalents, or use this skill as a shape to copy when writing your own.

[MAINTENANCE.md](./MAINTENANCE.md) walks through how to add your own skills.

## Sharing with your team

Once the folder is in your shared Drive, teammates with sync access can create their own Cowork Projects pointing at the same folder. Updates anyone makes show up for everyone else.

Treat the folder like a living document. When a customer signs, add them to `customers/`. When strategy shifts, update `knowledge/strategy.md`. When a feature ships, the `MAINTENANCE.md` rule is: the feature is not done until the OS reflects it.

## Credit

Built on the work of two people:

- **Hannah Stulberg** for the Team OS pattern: root `CLAUDE.md` + `.claude/` shared assets + per-folder doc indexes. [team-os-example-repo](https://github.com/in-the-weeds-hannah-stulberg/team-os-example-repo).
- **Ayushman Jain** for the PM-workspace shape: flat functional folders (team, customers, knowledge, analytics) and the hydrate-knowledge bootstrap idea. [Product-Management-Claude-Workspace-template](https://github.com/aupsy/Product-Management-Claude-Workspace-template).

This template adapts both for Claude Cowork.

Licensed under [CC BY-NC 4.0](./LICENSE).
