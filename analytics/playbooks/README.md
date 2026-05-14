# Playbooks

How-to guides for recurring analyses. The point: when activation drops, when retention slips, when a metric does something unexpected, someone on the team should be able to grab a playbook and run the same diagnostic the last person ran.

## Doc index

- `{{playbook-name}}.md`: one playbook per file. Examples: `diagnose-activation-drop.md`, `weekly-cohort-read.md`, `investigate-revenue-anomaly.md`.

## What goes in a playbook

- **When to use it:** the trigger that should make someone open this playbook.
- **Inputs you need:** which dashboards or queries to pull first.
- **Steps:** numbered, concrete. "Open dashboard X, look at column Y. If Y is below Z, go to step 4."
- **What you're looking for:** the patterns that distinguish a real issue from noise.
- **What to do when you find it:** who to tell, where to log the finding.

## When to add a playbook

After you've done the same investigation twice. Once is a one-off; twice means there's a pattern worth capturing.
