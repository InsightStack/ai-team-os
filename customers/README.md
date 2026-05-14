# Customers

One folder per customer. Each customer folder has a short summary, a contacts file, and a transcripts subfolder for the full record of calls.

## Doc index

- `_customer-template/`: copy this folder when you add a new customer. Rename to the customer's name in kebab-case (e.g., `acme-co/`).
- `<customer-name>/summary.md`: segment, contract, contacts, current state, last touchpoint.
- `<customer-name>/contacts.md`: key people and how to reach them.
- `<customer-name>/transcripts/README.md`: index of full call transcripts. Transcripts themselves are markdown or text files in the same folder.

## The summaries-first principle

When you ask Claude about a customer, it should be able to answer from the `summary.md` alone in 80% of cases. Transcripts get loaded only when a question demands them.

This is by design. Loading every transcript every time would burn context for no benefit. Keep summaries current and tight (under 100 lines per customer). When a transcript reveals something that should be in the summary, move it.

## How to add a customer

1. Copy the `_customer-template/` folder.
2. Rename it to the customer's name in lowercase with hyphens.
3. Fill in `summary.md` and `contacts.md`.
4. Add the customer to any team-level lists (forecast, account health, etc.) that live elsewhere.

You can also ask Cowork to do this for you:

```
Add a new customer to customers/. Name: Acme Co. Segment: mid-market SaaS.
Contract: $80k ARR. Primary contact: jane@acme.co.
```

## How to add a transcript

Save the transcript (recording summary, meeting notes, or full text) into the customer's `transcripts/` folder. Use a date-prefixed filename: `2026-04-22-qbr.md`. Then add a one-line entry to `transcripts/README.md` so the file is discoverable.

If the transcript changes anything in `summary.md` (new contact, churn risk, new ask), update the summary in the same edit.
