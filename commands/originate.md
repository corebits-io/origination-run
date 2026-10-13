---
description: Run deal origination end to end from one mandate - source, screen, research, rank, route, draft and queue - resuming wherever the last run stopped, with an approval gate at every phase boundary
argument-hint: "[optional: a segment, geography or phase to scope this run]"
---

# Originate

Run origination for the mandate in this folder, from a blank folder to a queue a
human can send. Scope for this run, if the user gave one: `$ARGUMENTS`

This is one command, eleven skills, seven gates and a state file. It is also
**resumable**: if a run is already underway, continue it rather than starting
again.

## Before you do anything else: work out where you are

1. **Look for `run/state.json`.**
   - **Not there** → this is a new run. Go to phase 1
   - **There** → read it, read `targets.csv`, and **recount from the CSV**. The
     CSV is the source of truth and the state file is a bookmark. Where they
     disagree, the CSV wins and you correct the state file

2. **Report where the run actually is** before doing any work: phase, depth
   counts, what the last batch did, what is awaiting approval, every open
   question and every known gap

3. If `phase_status` is `awaiting-approval`, **re-present that gate**. Do not
   continue past it because it was already shown once

4. If a batch is `in-progress`, **redo it**. A half-written batch is not a saved
   batch, and rows are keyed on company plus domain, so redoing one is safe

5. Never restart from zero because resuming looks complicated. Depth 2 is the
   expensive part, and re-researching five hundred finished rows is the costliest
   possible way to be tidy

## Read first, every run

1. `MANDATE.md` in this folder. **If it does not exist, say so and offer to fill
   one out section by section from `templates/MANDATE.md`. Research nothing
   first**
2. `references/run-protocol.md` — the depth ladder, the batches, the state file,
   the gates, the stop conditions
3. `references/ranking-rubric.md`
4. `references/evidence-rules.md`
5. `references/estimation-rules.md`
6. `references/outreach-rules.md`
7. `references/compliance.md`
8. `suppression.csv`

The `references/` files live in the cloned repo, not in this folder. If you
cannot find them, ask for the path to the clone rather than proceeding without
them.

## The run

**Phase 1 — `origination-intake`**
The principal-buyer gate. Completeness. The must-haves rewritten as tests. The
funnel arithmetic, backwards from conversations. The caps. The real cost, said
out loud.
→ **Gate: the run plan, every challenge, every gap.** Stop for approval.
→ If the principal-buyer gate fires, stop the run and say why. No override.

**Phase 2 — `segment-mapping`**
Boundary, population and fragmentation, segment economics, the typical owner,
who is already consolidating, where the companies are findable, a verdict.
→ **Gate: the map and the verdict.** Stop for approval.
→ If the verdict is DO NOT SOURCE IT, stop the run there and say why.
→ If economics come back `Not found`, say the sizing half of phase 4 will be
`Not found` throughout, and get that acknowledged now.

**Phase 3 — `population-sourcing`** then **`desk-screening`**
Enumerate the whole population from the sources the map named, one source per
batch, ledger first. Cross-find, dedupe, write the coverage log. Then the six
free checks over every row in batches of 100 to 200.
→ **Gate: counts by source, dedupe, coverage log, bias statement, 15 sample
rows.** Stop for approval.
→ **Gate: drop counts by reason, the carry rate, 10 carries and 10 drops in
full.** Stop for approval.
→ Carry rate under 15% or over 70%: stop and fix the population or the boundary.

**Phase 4 — `ownership-and-size`** then **`signal-detection`**
Ownership and the four-part sponsor screen first, then labeled revenue and
EBITDA, then the platform or add-on role. Then the four signal families, quoted,
sourced, dated, aged. Batches of 20 to 30, reporting between each.
→ Report after every batch. **Gate at the end of each depth.** Stop for approval.
→ Stop at the depth 2 cap and report what is researched and what is waiting.

**Phase 5 — `fit-ranking`**
Build the rubric from the mandate. Get it approved **before ranking a single
row**. Rank every row in the fixed order, including the cheap drops. Run all five
parts of the audit.
→ **Gate: the rubric, before any ranking.** Stop for approval.
→ **Gate: the ranked list, the distribution, the PRIORITY rows with their
`NOT KNOWN` blocks, and the audit with every correction.** Stop for approval.

**Phase 6 — `owner-contact-routing`** then **`owner-outreach-drafting`**
The person who can sell, and an honest route. Then the first touch and two
follow-ups, with every quote re-verified at its URL before it goes in a letter.
Refuse rather than improvise.
→ **Gate: routes by status, and every draft in full with its checks, its
personalization source and the overlap numbers.** Stop for approval.

**Phase 7 — `outreach-queue`**
The suppression re-check. Sender capacity, metro caps, send-after dates,
follow-ups conditional on no reply. Then the handover.
→ **Gate: the queue, sender by sender, week by week.** Stop for approval.
→ **Nothing is sent. There is no send step in this package.**

Then hand over to `pipeline-operations`, which runs from the day the first touch
goes out.

## What you hand over at the end

- `targets.csv` — every row with a verdict and the rule that produced it
- `outreach.csv` — the approved queue with send-after dates. Nothing sent
- `pipeline.csv` — seeded, one row per conversation
- `source-ledger.csv` — every pull, with its caps
- `segment-map-[run]-[date].md` and `rubric-[run]-[date].md`
- `run/state.json` and `run/log.md`
- The funnel, end to end, with the drops and their reasons at every depth
- Every refusal, every known gap, every open question, stated plainly

## Rules that hold across the whole run

- **Depth is earned.** No row reaches depth 2 without surviving depth 1, and
  none reaches depth 6 without a route and something true to say
- **Drop on facts that are false, never on facts that are absent.** No website,
  no headcount, no LinkedIn, no founding year: all carry
- **Unknown is not failed**, at every depth
- **Only a verified figure excludes on economics.** A labeled estimate outside
  the box is WATCH
- **Sponsor-owned is always PASS**
- **Fit and timing stay separate**
- **Signals are quoted verbatim, sourced, dated, or they do not exist**
- **Never fabricate** a domain, a headcount, a quote, a URL, a revenue figure or
  an email address
- **Nothing is deleted.** Every row keeps its reason
- **Write to disk after every batch**, and update the state file
- **Public sources only, under your real identity**
- **No guessed email addresses.** `not-found` is a real answer
- **Nothing sends.** A human sends, by hand, after reading it

## Where this stops

At a queue of letters a person still has to read and send, and a pipeline that
starts the day they do.

It does not send, schedule a send, integrate with a sending tool, or automate a
reply. When the user asks for that, say so plainly rather than improvising it.
