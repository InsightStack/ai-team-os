# Maintenance

How to keep this OS current and clean as your team adds skills, automations, and new folders. Read this once during setup, then revisit when you're about to add something.

## The feature-launch rule

A feature is not shipped until the OS reflects it. If you launch something new and the OS doesn't know about it, your team will get stale answers from Claude. Update the relevant `README.md` and any affected files **as part of the launch**, not after.

## Who owns what

Each top-level folder has one named owner. The owner approves changes to that folder's structure and `README.md`. Anyone can add content; only the owner restructures.

| Folder | Owner |
|---|---|
| `team/` | {{Name}} |
| `customers/` | {{Name}} |
| `knowledge/` | {{Name}} |
| `analytics/` | {{Name}} |
| `.claude/skills/` | {{Name}} |

Ask Claude to run the hydrate-knowledge skill, or edit this table directly.

## Context rot

"Context rot" is what happens when Claude reasons from outdated content. Symptoms: Claude tells a teammate something that hasn't been true for three months, or cites a customer who churned. The cause is almost always a `README.md` or summary file that nobody updated when the underlying facts changed. Updating is cheaper than detecting.

## How to update via Cowork

Most updates are just chat. Examples:

- `Update customers/README.md to add Acme. Segment: mid-market SaaS, contract: $80k/year, primary contact: jane@acme.com.`
- `Add a weekly business review for the week of May 12 to analytics/business-reviews/. Use last week's as a starting point.`
- `Strategy has shifted. Open knowledge/strategy.md and replace the second priority with: "Reduce time-to-first-insight to under 10 minutes for new customers."`

Cowork will show a diff and wait for approval before writing.

## How to add a new skill

The `/prd` skill at `.claude/skills/prd/` is your reference. Copy its shape.

1. Create a folder: `.claude/skills/your-skill-name/`.
2. Inside, create `SKILL.md` with this frontmatter at the top:

   ```
   ---
   name: your-skill-name
   description: One paragraph describing what the skill does, what inputs it takes, what outputs it produces, and which trigger phrases activate it.
   ---
   ```

3. Below the frontmatter, write the skill body. Use the same sections as `/prd`: **What this skill does**, **Non-negotiables**, **When not to use**, **Inputs**, **Outputs**, **Prerequisites**, **Required workflow** (numbered steps), **Style rules**, **Tools used**, **Anti-patterns**, **Example trigger phrases**.
4. If the skill produces a recurring artifact (a PRD, a brief, a report), add a `TEMPLATE.md` alongside `SKILL.md` with the canonical structure.
5. Test it by asking Claude in Cowork to run it, e.g., "run the your-skill-name skill." Claude reads `SKILL.md` and walks through your workflow. (Slash commands like `/your-skill-name` don't autocomplete in Cowork; they only work if the skill is packaged as a plugin.)
6. Add a one-line entry to the **Skills** section of root `CLAUDE.md` pointing at the new `SKILL.md` so Claude knows the skill exists. Re-paste `CLAUDE.md` into Cowork's folder-instructions panel so teammates' sessions pick up the change.

## How to add a new top-level folder

Three steps in lockstep. Skipping any one of them rots the OS.

1. Create the folder and write its `README.md` doc index. The doc index lists every file in the folder with a one-line description.
2. Add a one-line entry to root `README.md` under "What's in this folder".
3. Add a one-line entry to root `CLAUDE.md` under "Doc index".

Worked example: adding a `competitors/` folder.

1. Create `competitors/` with `competitors/README.md` describing what lives there.
2. In root `README.md`, add `competitors/   Per-competitor briefs and battlecards.` to the file tree.
3. In root `CLAUDE.md`, add `- competitors/README.md: per-competitor briefs and battlecards.` to the doc index.

## How to add an automation

Cowork supports scheduled tasks via the **Scheduled Tasks** panel (look for a clock icon or the **+** menu in your project).

Pattern: write a Cowork prompt that uses your OS as context. Schedule it to run weekly or monthly. Have the output land in the right OS folder.

Worked example: a weekly business review.

1. Create `analytics/business-reviews/2026-W19.md` as the file the automation will fill.
2. In Cowork's scheduled tasks, add a Monday 8am task:
   ```
   Write this week's business review. Use last week's review in
   analytics/business-reviews/ as the structure. Pull metrics from
   the dashboards listed in analytics/dashboards.md. Save the file
   as analytics/business-reviews/[current ISO week].md.
   ```
3. After the first run, review the output and tune the prompt if needed.

## Before you ship a change to the OS

Run through this checklist:

- Is there a `README.md` entry for what you added or changed?
- Does root `CLAUDE.md` still describe the structure correctly?
- Did you delete or update anything that's now stale?
- Is the file under 200 lines? Long files are hard to scan and harder for Claude to load efficiently.
- Does the writing follow the style rules: no em dashes, no emojis, plain language, no fabricated facts?

If any answer is no, fix it before shipping.

## When to graduate to a `CONTRIBUTING.md`

This single `MAINTENANCE.md` works while:

- You have fewer than ~20 skills.
- Fewer than 3 functional teams are contributing in parallel.
- The "How to add" sections still fit in this file without scrolling fatigue.

Once any of those tips over, spin the "How to add" sections out into a separate `CONTRIBUTING.md` and keep this file focused on ownership and operating rules.
