---
name: hydrate-knowledge
description: Bootstrap a new Team OS using whatever the user has connected. Reads from Drive, Gmail, Calendar, Slack, and any other available MCPs to pre-fill the root CLAUDE.md, knowledge/strategy/README.md, knowledge/competition/README.md, and team/roster.md. Optionally fetches a product homepage URL. Finishes with a short interview to confirm and fill gaps. Triggers when the user says "hydrate my Team OS," "bootstrap this OS," "fill in the template," or runs /hydrate-knowledge with or without a URL.
---

# Hydrate Knowledge Skill

## What this skill does

Bootstraps placeholder content in this Team OS into real content. Reads whatever MCPs the user has connected, optionally fetches a product URL, then runs a short interview to confirm pre-filled values and fill gaps. Writes to four target files (plus a conditional fifth) only after the user approves the full draft.

## Non-negotiables (apply throughout)

- **Never fabricate.** If a field is unknown, write the literal string `{{TBD}}`. Do not invent.
- **Never read an MCP source the user did not approve.** Step 2 is the explicit per-source opt-in.
- **Pre-fills are drafts, not commitments.** Show the user every value before write.
- **Graceful degradation.** If an MCP probe fails, note "X not connected" in the source summary and continue. Never block the whole skill on one missing connector.
- **No em dashes.** Plain language. Inherits style from the root `CLAUDE.md`.

## When not to use this skill

- Routine updates to OS content after initial setup (use direct chat: "update customers/README.md to add Acme").
- Adding a single new doc to an already-hydrated OS (use direct chat).
- Authoring a PRD (use `/prd`).

## Inputs

- Optional: a single URL passed alongside the trigger (product homepage or public docs site).
- Required during the workflow: user's chat answers confirming sources and field values.
- Probed: whatever MCPs are connected.

## Outputs

- Updated root `CLAUDE.md`: team roster section, doc index confirmation, communication channels filled or marked `{{TBD}}`.
- Filled `knowledge/strategy/README.md`.
- Filled `knowledge/competition/README.md`.
- Filled `team/roster.md`.
- (Conditional, only if InsightStack MCP is connected and the user approves) a "What we're hearing" pointer seeded in `customers/README.md`.
- A summary report at the end listing sources used, fields filled, fields left as `{{TBD}}`, and the recommended next step.

## Prerequisites

None hard. Skill works in interview-only fallback if nothing is connected. Best results with at least Drive and Calendar connected. If InsightStack is connected, the `customers/README.md` seed is included.

## Required workflow

Follow these steps in order.

### Step 1: Probe

Try one cheap call against each candidate MCP to detect what's available:

- Drive: `list_recent_files` (limit 1)
- Calendar: `list_calendars`
- Gmail: `list_labels`
- Slack: `slack_search_channels` with a generic term
- InsightStack: `list_pain_points` (limit 1)
- Linear: `list_teams` (limit 1)
- Notion / Jira: equivalent list call

Mark each connector as `available` or `unavailable`. Probe failures are not errors. Continue.

### Step 2: Plan

Tell the user exactly which MCPs you found and ask for per-source approval:

> "I can see you have [Drive, Calendar, Slack, InsightStack] connected. I'll use them to pre-fill your OS. Want me to skip any of these? Default: use all available."

Wait for confirmation. If the user passed a URL with the trigger, also confirm whether to fetch it.

List the queries you'll run against each approved source before running them. The user should know what you're about to read.

### Step 3: Read

Execute the approved MCP reads in this order. For each, surface top candidates and let the user pick what's relevant. Never read everything blindly.

- **Drive:** search for files matching `OKR`, `strategy`, `vision`, `product brief`, `competitive`, `roadmap`. Show top 5 candidates per category. User picks. Read selected files. Synthesize into draft text for `knowledge/strategy/README.md` and `knowledge/competition/README.md`.
- **Calendar:** list recurring events from the last 30 days. Cluster attendees from 1-on-1s and team standups into a draft team roster. Surface the list.
- **Gmail (if approved):** search recent threads for `strategy`, `OKR`, or `competitive` in subject lines. Offer to read the top 2 or 3 most relevant. Use for additional context only, do not write directly from emails.
- **Slack (if approved):** list the user's primary channels and members. Use channel names as comms-channel pointers in root `CLAUDE.md`. Cross-check team roster.
- **InsightStack (if approved):** pull the top 5 pain points and 3 latest insights. Use for the `customers/README.md` "What we're hearing" seed.
- **Linear / Notion / Jira (if approved):** list active projects. Use names as inputs for `knowledge/prds/README.md` pointer text.

### Step 4: URL fetch (conditional)

If the user passed a URL in Step 0 and approved it in Step 2, run `WebFetch` on it. Extract product name, one-line description, target audience.

If the page returns junk (JS-heavy SPA, empty body, error), note "URL fetch returned no useful content" and continue with what you have.

### Step 5: Interview for gaps

Ask the user to confirm pre-filled values and fill anything the sources didn't cover. Walk one field at a time and react to each answer:

1. Confirm product name and one-line pitch. If pre-filled from the URL, just ask "correct?"
2. Confirm or ask for top 3 strategic priorities for the next 6 months.
3. Confirm or ask for top 2 or 3 competitors.
4. Confirm or ask for the team roster: names, roles, and primary handles in Slack/Linear/etc.
5. Confirm or ask for primary communication channels (Slack channels, group threads).
6. Ask for primary customer segment in one sentence.

If the user can't or won't answer a question, mark the field `{{TBD}}` and move on. Don't push.

### Step 6: Draft and confirm

Show the user the complete draft of what will be written to each target file. Use clear file headers:

> Here's what I'll write to each file. Reply "approve" to write, or tell me what to change.
>
> **root CLAUDE.md**: [draft of team roster section and comms channels]
>
> **knowledge/strategy/README.md**: [full draft]
>
> **knowledge/competition/README.md**: [full draft]
>
> **team/roster.md**: [full draft]
>
> **customers/README.md**: [the conditional InsightStack seed, only if applicable]

Wait for explicit approval before any write. Iterate on requested changes.

### Step 7: Write

After approval, write the files. Use `Edit` to replace placeholders in existing files. Use `Write` only if a target file does not yet exist. Use the literal string `{{TBD}}` for any field the user didn't fill.

### Step 8: Summary

Tell the user:

- Which sources were used (and which were skipped).
- Which fields were filled.
- Which fields are `{{TBD}}` (and a one-line suggestion for how to fill each later).
- The recommended next step: either "Run `/prd` to draft your first PRD" or "Add your first customer to `customers/` by copying `customers/_customer-template/`."

## Style rules

- Plain language. No em dashes. No emojis.
- Terse drafts. If you can cut a sentence, cut it.
- Cite sources inline when relevant. Example: "Strategic priority 1 (from your Q2 OKR doc in Drive)."
- Never fabricate. `{{TBD}}` is always an option.

## Tools used

- MCP reads (conditional on availability and user approval):
  - Drive: `search_files`, `read_file_content`
  - Calendar: `list_calendars`, `list_events`
  - Gmail: `search_threads`, `get_thread`
  - Slack: `slack_search_channels`, `slack_search_users`
  - InsightStack: `list_pain_points`, `list_insights`
  - Linear / Notion / Jira: equivalent project-list calls
- `WebFetch` (conditional, URL mode only)
- `Read` to check current placeholder content before overwriting
- `Edit` to replace placeholders in existing files
- `Write` only when a target file doesn't yet exist

## Anti-patterns to avoid

- Reading from MCPs without per-source approval in Step 2.
- Running through the workflow without showing the final draft. Always pause for approval before write.
- Filling unknown fields with plausible inventions. Use `{{TBD}}`.
- Writing to files outside the five known targets.
- Blocking the entire skill because one MCP is missing. Degrade gracefully.
- Treating a noisy URL fetch as authoritative. If the page is junk, say so and rely on the interview.

## Example trigger phrases

- "Hydrate my Team OS."
- "Bootstrap this OS."
- "Fill in the template for me."
- "/hydrate-knowledge"
- "/hydrate-knowledge https://myproduct.com"
