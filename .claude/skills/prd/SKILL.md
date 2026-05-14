---
name: prd
description: Author a PRD for an InsightStack feature, then export it as a Linear project with milestones and issues. Triggers when the user wants to "write a PRD", "draft a PRD", "create a PRD", "start a PRD for X", "turn this idea into a PRD", or scope a new feature for engineering. Pulls customer evidence from InsightStack MCP and creates the project, milestones, and issues via the Linear MCP. Tailored to InsightStack's 2-person team and Aakash Gupta-inspired brevity.
---

# PRD Authoring Skill

## What this skill does
Walks the user through writing a tight, evidence-backed PRD for InsightStack, then ships it to Linear as a project with milestones and known issues. The PRD draft lives in chat (and optionally on disk); Linear is the source of truth once exported.

Target length: 1-2 pages rendered. Shorter is better, as long as an AI coding agent has enough context to work autonomously.

## Non-negotiables (apply throughout)
- **No em dashes.** Use commas, periods, semicolons, or colons.
- **No fabricated customer evidence.** If InsightStack returns nothing, say so plainly.
- **No fabricated metrics.** If there's no baseline, write "baseline TBD."
- **Read code before drafting Approach.** Never claim how the system works from filenames or grep summaries alone.
- **Wait for explicit user approval before writing to Linear.**

## When not to use this skill
- Quick one-off Linear issues that don't need a PRD or project structure.
- Internal docs, runbooks, or design notes (use `doc-coauthoring` instead).
- Sub-tasks inside an existing Linear project (add issues directly).
- Bug fixes or small enhancements that don't span multiple milestones.

## Inputs
- A feature idea, problem statement, or rough scope from the user.
- (Optional) An existing draft, doc, or Linear issue to start from.

## Outputs
- A completed PRD in markdown, following `TEMPLATE.md` in this skill's directory.
- A Linear project with the PRD as the description, ordered milestones (M1, M2, ...), and seed issues attached to each milestone.

## Prerequisites
- InsightStack MCP connected (tools prefixed `mcp__insightstack__*`).
- Linear MCP connected (tools prefixed for Linear: `list_teams`, `save_project`, `save_milestone`, `save_issue`, etc.).
- Read access to the codebase for cross-referencing existing patterns.

If either MCP is missing, pause and tell the user which one needs to be connected before continuing.

## Required workflow

Follow these steps in order. Do not skip steps. Confirm with the user before any Linear write.

### Step 0: Load the template
Read `~/.claude/skills/prd/TEMPLATE.md`. This is the canonical structure. Do not invent sections.

### Step 1: Frame the feature
Ask the user for:
1. Working title for the feature.
2. One-sentence pitch (what ships, for whom).
3. Whether this is a net-new feature or an extension of existing work. If extension, ask for the related Linear project or codebase area.

If the user hands you an existing doc or rough notes, parse those first and only ask for what's missing.

### Step 2: Problem and persona
Draft the **Problem** section in 1-2 short paragraphs based on what the user told you. Name the persona inline (role + relevant context, e.g., "Head of Product evaluating InsightStack on a demo call").

Show the draft. Ask: "Does this capture the right user and the right pain?" Iterate until the user signs off.

### Step 3: Customer evidence
Pull supporting quotes from InsightStack.

1. Derive a query or tag set from the problem text. Examples: keyword search via `search_feedback`, pain-point list via `list_pain_points`, recent transcripts via `list_transcripts`, saved insights via `list_insights`.
2. Show the user the query you ran and the candidate quotes (5-10 max). Let the user pick 3-5.
3. For each selected quote, capture: speaker role + company, exact quote text, link to the source insight or pain point in InsightStack.
4. Compute the **Evidence span** line: number of distinct customers, number of accounts, and the exact query string used. Phrase the query so an agent updating the PRD later can re-run it without guessing.

**If the query returns nothing,** warn the user: "No InsightStack evidence found for `<query>`. The PRD will note this gap." Continue without quotes; mark the Customer Evidence block as "No supporting evidence at draft time. Re-run query `<x>` after next sync."

### Step 4: Outcome and metrics
Ask the user:
1. What changes for the user once this ships? (User outcome, behavioral, not feature-shaped.)
2. What single number tells us this worked? (North star, with current baseline if known and target.)
3. (Optional) Earlier signal we'd see first? (Leading indicator.)
4. (Optional) What we won't regress? (Guardrail.)

If the user can't name a north star, push back once: "Without a north star metric, we can't tell if this worked. Want to skip the metric, or pick a proxy?" Don't fabricate one.

### Step 5: Approach and Done When

**First, ground in the codebase.** Before drafting Approach, read the actual files this PRD will touch. Do not draft from grep summaries or filenames alone. Open the files. The goal is to make every claim in Approach and Done When verifiable against real code.

Concretely:
- Identify the files most likely affected (auth handler, route, data model, UI entry point, config). Use `Glob` and `Grep` to locate; then `Read` the files in full or in the relevant range.
- Capture the current shape: function signatures, types, auth model, transport, persistence, instrumentation already present. Note line numbers for citation.
- For any claim you're about to write ("respect user role permissions," "preserve API-key path," "wire into analytics"), confirm the underlying mechanism exists in the code. If it doesn't, the claim is wrong or it's a real design decision that belongs in Open Questions.
- Surface real design decisions to the user before drafting. Reality almost always reveals at least one unspecified question (permission model, keying strategy, persistence, schema). Flag these explicitly rather than papering over them.

Only after this read pass, draft 2-4 sentences on the "what." Reference codebase paths and line numbers where relevant (e.g., `apps/web/src/foo.ts:42`). The goal is enough context for an AI coding agent to start without re-deriving the design.

Then list 3-6 **Done when** bullets: observable, verifiable conditions checkable by running the product or querying data. Each bullet should match real code paths or real artifacts the agent will produce. No internal milestones here, those go in Project Structure.

**Anti-pattern**: drafting Approach from the user's framing alone, then only checking the code at export time. By then the milestones inherit the wrong assumptions and need rework. Read first, draft second.

### Step 6: AI Behavior (conditional)
Ask: "Does this feature involve AI/model-driven behavior?"

If yes, fill the AI Behavior sub-section: model choice, inputs/context, expected behavior with one example, failure modes and fallback, eval approach.

If no, omit the sub-section entirely. Do not leave a placeholder.

### Step 7: Non-goals
Ask the user to name 2-5 things a reasonable reader might assume are in scope but aren't. Push for specificity. "Not doing X yet" is fine; "general performance work" is too vague.

### Step 8: Project Structure
Propose 1-3 milestones using the `M1: <name>` format. For each milestone:
- One-line description of what's done at the checkpoint.
- 2-5 seed issues, each with a title and one-line description.

**Issues must be vertical slices.** Each issue should be independently shippable as a single PR. Concretely:
- One issue, one PR, one merge. No issue depends on another being merged in the same milestone before it can ship.
- Avoid splitting one logical change into "design + implement" sub-issues unless the design output is a real artifact (a decision doc, a schema migration plan).
- If issue A only makes sense after issue B merges, consider whether they should be one issue.
- Combine "emit" and "wire" or "schema + populate" when they ship together or not at all.
- Long-running design decisions belong in Open Questions, not as issues.

After drafting milestones, scan each issue and ask: "Could a developer pick this up cold, ship a single PR, and have it land cleanly without other in-flight work?" If no, restructure.

Iterate with the user. Keep milestone count low (2-3 is typical for InsightStack's pace). If the user proposes more than 4, ask whether some can be deferred to a follow-up project.

### Step 9: Open Questions
Throughout drafting, capture unresolved questions in the Open Questions section. Mark each as blocking or non-blocking. Try to resolve blocking questions before export by asking the user directly. Move resolved questions to the Resolved log with the answer and date (use today's date from the environment context).

### Step 10: Final review
Render the full PRD. Verify:
- Length is 1-2 pages.
- No em dashes anywhere (replace with commas, periods, semicolons, or colons).
- No emojis.
- All template sections present (AI Behavior optional).
- Customer Evidence block has either quotes + Evidence span line, or the "no evidence" warning.

**Then run two structural checks before asking to export:**

1. **Vertical slice check.** Re-run the rules from Step 8 against the final issue list. Combine over-split issues; flag hidden dependencies.

2. **Alignment check.** Build a short table mapping every element of Problem, Customer Evidence, and Outcome to the specific Approach element or Done-when bullet that addresses it. Then scan for:
   - Approach work with no upstream Problem/Evidence/Outcome anchor (scope creep).
   - Problem or Outcome elements with no downstream Approach coverage (gap).
   - Customer Evidence quotes that don't actually support the chosen direction (overclaim).
   Report the table to the user with an honest verdict, including any gaps you found. Do not paper over weak alignment.

Show the draft and ask: "Ready to export to Linear, or any edits first?"

### Step 11: Linear export
Only after the user explicitly approves, create the Linear project.

1. Resolve the InsightStack team. Default to team key `INS`. Confirm with the user if multiple teams are returned.
2. Call `save_project` with:
   - `name`: feature name from Step 1.
   - `summary`: the one-line pitch.
   - `description`: the full PRD markdown (Goal through Open Questions).
   - `team`: resolved team ID.
3. For each milestone in order, call `save_milestone` with the project ID, name (e.g., `M1: Demo-ready signup`), and description (the one-line description from Step 8).
4. For each seed issue, call `save_issue` with the project ID, milestone ID, title, and description (one-line + any specifics from drafting).
5. After all issues are created, update each milestone's description to append `Issues: INS-XX, INS-YY, INS-ZZ` matching the existing project convention.
6. Return the project URL to the user.

If any Linear call fails, stop and report which step failed. Do not retry destructively.

## Style rules (non-negotiable)
- **No em dashes.** Use commas, periods, semicolons, or colons. Applies to PRD body, Linear project description, milestone descriptions, and issue descriptions.
- **No emojis** unless the user explicitly asks.
- **Terse.** Lee prefers tight prose. State the result, skip preamble.
- **No fabricated evidence.** If InsightStack has no supporting quotes, say so plainly in the PRD.
- **No fabricated metrics.** If there's no baseline, write "baseline TBD" rather than inventing a number.
- **Aakash Gupta-inspired brevity, not bureaucracy.** Skip risks, rollout, and decision logs (those happen in 1-on-1s with James).

## Tools used
- `Read` for `TEMPLATE.md` and codebase references.
- InsightStack MCP: `search_feedback`, `list_pain_points`, `list_insights`, `get_insight`, `list_transcripts`, `get_transcript`.
- Linear MCP: `list_teams`, `save_project`, `save_milestone`, `save_issue`, `list_issue_statuses` (if needed for default state).
- `Write` (optional) to save a local PRD draft to `.claude/prd-drafts/<slug>.md` if the user wants a working copy before export.

## Anti-patterns to avoid
- Drafting Approach or Project Structure from filenames and grep summaries instead of reading the actual code. Always read the files this PRD will touch before claiming how the system works.
- Asking for everything upfront. Walk section by section so the user reacts to concrete drafts.
- Letting the PRD balloon past 2 pages. If it's getting long, ask what can be cut or deferred to a follow-up project.
- Creating the Linear project before the user approves the final draft.
- Filling the AI Behavior section when the feature has no model-driven behavior.
- Reusing a feature branch or existing project for unrelated work. Each PRD is a new Linear project.

## Example trigger phrases
- "Write a PRD for adding a CSV import to InsightStack."
- "Draft a PRD for the new dashboard."
- "Turn this idea into a PRD: [paragraph]."
- "Start a PRD, the goal is to let users tag transcripts in bulk."
