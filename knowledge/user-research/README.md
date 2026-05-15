# User research

Research synthesis, personas, and recurring patterns from customer conversations. Lives as a folder so individual studies (interview rounds, surveys, diary studies) can each get their own writeup file.

**Last meaningful update:** {{YYYY-MM-DD}}

## Doc index

- `README.md` (this file): personas, recurring patterns, and open research questions.
- `_study-template.md`: copy this when writing up a discrete research study.
- `{{YYYY-MM}}-{{topic}}.md`: one file per study (e.g., `2026-04-activation-interviews.md`).

## Personas

### {{Primary persona name}}

- **Role:** {{Job title}}
- **What they're trying to do:** {{One sentence}}
- **Where they get stuck today:** {{One sentence}}
- **What "success" looks like for them:** {{One sentence}}
- **Where you've seen this:** {{Link to customer summaries or feedback sources}}

### {{Secondary persona name}}

- **Role:** {{Job title}}
- **What they're trying to do:** {{One sentence}}
- **Where they get stuck today:** {{One sentence}}
- **What "success" looks like for them:** {{One sentence}}

## Recurring patterns

{{Patterns that show up across multiple research conversations. Two or three bullet points. Each pattern should reference the customers or quotes that support it.}}

## Open research questions

{{Things you don't know yet but want to. One line each, with the kind of conversation or data that would answer them.}}

## When to add a study writeup

After a focused round of interviews or a survey with a discrete question. The rule of thumb: if findings will inform a decision the team cites later, write it up. If it was an exploratory chat, the customer transcript itself is enough.

Copy `_study-template.md`, name it `{{YYYY-MM}}-{{topic}}.md`, and add a one-line entry to the doc index above.

When a study reveals a finding that changes personas or recurring patterns, edit this README in the same commit.

## Style

Every pattern claim should cite the customer summaries or transcripts that back it. "Customers want X" with no source is opinion. Link to `../../customers/<customer-name>/transcripts/<file>.md` or to an InsightStack insight.
