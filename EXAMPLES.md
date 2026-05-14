# Examples

These are example snippets so you can see what filled-in content looks like. **Do not ship these in your live OS.** Delete this file once you've replaced the placeholders with your real content.

The names below (Acme Co, Northwind, etc.) are placeholders. Every quote is fabricated.

---

## Example 1: A customer summary

`customers/acme-co/summary.md`

```markdown
# Acme Co

EXAMPLE: fabricated for illustration. Replace with a real customer.

**Segment:** mid-market SaaS, 200-500 employees.
**Contract:** $80k ARR, signed 2026-01-12, renewal 2027-01-12.
**Primary contact:** Jane Doe, VP Product (jane@acme.co).
**Secondary contacts:** Marco Lee, Engineering Lead. Priya Shah, Customer Success.
**Last touchpoint:** Quarterly review, 2026-04-22. Notes in `transcripts/2026-04-22-qbr.md`.

## Current state

On-track. Using two of our three main features. Has asked about CSV export twice in the last quarter.

## What they care about

1. Reducing manual data entry across their support and product teams.
2. Compliance reporting for their next SOC 2 audit.
3. Faster onboarding for new hires (currently 2 weeks of shadowing).

## Open threads

- CSV export request, see `transcripts/2026-04-22-qbr.md` and pain point in our feedback tool.
- Pricing conversation deferred until renewal cycle.
```

---

## Example 2: A team rituals entry

`team/rituals.md` (partial)

```markdown
# Rituals

EXAMPLE entries. Replace with your team's actual rhythm.

## Monday: weekly focus

10am-10:30am. Everyone shares the one thing they're trying to land this week and the one thing they need help with. No status reports.

## Wednesday: customer sync

11am-12pm. Two customer touchpoints from the prior week, summarized in five minutes each. Recorded summaries land in `customers/<customer>/transcripts/`.

## Friday: retro

3pm-3:45pm. What worked, what didn't, one experiment for next week. Notes land in `team/retros/<date>.md`.

## Monthly: strategy review

First Tuesday of the month. Re-read `knowledge/strategy.md`. Confirm or revise.
```

---

## Example 3: A PRD opening

`knowledge/prds/csv-import.md` (first three sections only)

```markdown
# PRD: CSV import for Acme Workflows

> Lets workflow admins bulk-import customer records from a CSV file instead of typing them one at a time.

## Goal

Workflow admins can populate a new workflow's customer list in under five minutes, regardless of how many customers they have.

## Context

### Problem

EXAMPLE: fabricated for illustration. Replace with your real problem statement.

Workflow admins at mid-market customers (200-500 employees) frequently set up workflows for groups of 50-500 customers at a time. Today they type each customer in one by one via the web UI. This takes 30-60 minutes per workflow and admins describe it as "the part where I question whether I should automate myself out of this job." The workaround is asking engineering for a one-off SQL import, which engineering is sick of.

### Customer Evidence

EXAMPLE: fabricated quotes. Replace with real quotes from your customer feedback source.

> *"The first hour of every new workflow is just typing names. There has to be a CSV button somewhere I'm missing, right?"*
> Jane Doe, VP Product, Acme Co. [example-source-link]

> *"We have 280 reps. I'm not setting up 280 records by hand. I asked engineering to write a script. They said no."*
> Marco Lee, RevOps Lead, Northwind. [example-source-link]

**Evidence span:** 2 distinct customers across 2 accounts. *(Replace with real numbers from your customer feedback source.)*
```

---

## When you're done

Delete this file. Once your placeholders are real content, `EXAMPLES.md` is dead weight.
