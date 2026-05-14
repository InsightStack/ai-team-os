# PRD: [Feature name]

> One-line summary. What ships, for whom.

## Goal
A single sentence. The user-visible change this delivers. If you need more than one sentence, the goal isn't tight enough.

## Context

### Problem
Free text. Who hits this, what they're trying to do, where they get stuck today, and the workaround they use now. Name the persona inline (role + relevant context). Two short paragraphs max.

### Customer Evidence
3-5 direct quotes from InsightStack. Each: speaker role + company, quote, link to the source insight or pain point.

> *"Quote text here."*
> Role, Company. [source](insightstack-link)

**Evidence span:** `<n>` distinct customers across `<m>` accounts. Surfaced via InsightStack query: `<exact query string or tag set>`. *(An agent updating this PRD can re-run this query against the InsightStack MCP to refresh quotes.)*

### Outcome
**User outcome:** What changes for the user once this ships. Behavioral, not feature-shaped.

**North star metric:** The one number that tells us this worked. Baseline + target.

**Leading indicator** *(optional):* Earlier signal we'll see before the north star moves.

**Guardrail** *(optional):* What we won't regress.

## Approach
2-4 sentences on the "what." Enough for an AI coding agent to start without re-deriving the design. Reference existing patterns in the codebase by path where relevant.

**Done when:**
- Observable, verifiable conditions. Each one checkable by running the product or querying data.

### AI Behavior *(include only if the feature involves model-driven behavior)*
- **Model:** which Claude model and why.
- **Inputs / context:** what we pass in, what we don't.
- **Expected behavior:** what good output looks like, with one example.
- **Failure modes & fallback:** what we do when the model is wrong, slow, or unavailable.
- **Eval:** how we'll know it's working in production (spot-check cadence, eval set, or metric).

## Non-goals
- Things a reasonable reader might assume are in scope but aren't. One sentence each.

## Project Structure
Ships as a Linear project. The skill creates milestones and issues automatically.

**M1: [Milestone name]**
One-line description of what's done at this checkpoint.
- Issue title. One-line description.
- Issue title. One-line description.

**M2: [Milestone name]**
One-line description.
- Issue title. One-line description.
- Issue title. One-line description.

*(After Linear creation, milestone descriptions are backfilled with issue identifiers, e.g. `Issues: INS-99, INS-101, INS-106`.)*

Issues discovered during execution get added in Linear directly, not back-ported here.

## Open Questions

**Open:**
- [ ] Question text. *(blocking: yes/no)*

**Resolved:**
- [x] ~~Question text~~. Resolution: brief answer. *(YYYY-MM-DD)*
