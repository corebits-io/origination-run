---
description: Where the origination run actually is - the funnel at every depth, what is awaiting approval, what is overdue in the pipeline, and the cheapest next move
argument-hint: "[optional: a depth or a phase to look at in detail]"
---

# Run status

Report where the run is. Do not do any research, do not continue the run, and do
not write anything. This command is read-only. Scope, if the user gave one:
`$ARGUMENTS`

## Read

1. `run/state.json`
2. `targets.csv` — and **recount from it**. The CSV is the source of truth, the
   state file is a bookmark. Report any disagreement between the two rather than
   quietly correcting it
3. `outreach.csv`, `pipeline.csv`, `source-ledger.csv`, `suppression.csv`
4. The last ten entries in `run/log.md`

If there is no state file and no `targets.csv`, say there is no run in this folder
and stop.

## Report, in this order

**1. The headline.** One line: which phase, running or waiting, and on what.

**2. The funnel**, counted from the CSV, depth by depth, with the drops and their
reasons at each depth. Show the verdict split if ranking has run.

**3. Awaiting you.** Every gate at `awaiting-approval`, and what approving it
would start. This is the most useful part of the output, so do not bury it.

**4. Overdue.** From `pipeline.csv`: anything past its `next_action_date`, every
active row with no next action at all, and this month's dormant revisits. Lead
with the ones where something was promised to an owner.

**5. The queue.** Approved and unsent by sender and week, with the caps stated.
Anything scheduled whose signal will expire before it is due to be sent.

**6. Budget.** Rows researched against the depth 2 cap. First touches sent this
week against capacity. How much of the screened population is still unresearched.

**7. Known gaps and open questions**, verbatim from the state file. Capped source
pulls especially: six weeks later nobody remembers.

**8. The cheapest next move**, with the row count behind it:

| If | Then |
|---|---|
| A gate is awaiting approval | Approve it. Nothing else matters until it moves |
| The pipeline has overdue actions | Those first. An owner is waiting on a promise |
| Top of funnel is the constraint and WATCH rows have stale signals | A signals re-read on the top WATCH rows. Cheapest refill there is |
| Top of funnel is the constraint and WATCH rows are current | Route and draft the top WATCH rows |
| The depth 2 cap stopped the run short | Depth 2 on the remaining screened rows |
| The screened population is exhausted | A new enumeration: new geography, adjacent segment, new source tier. The most expensive move, and the one everybody reaches for first |

## Keep it short

This is a standing-up report. The funnel, what is waiting, what is overdue, and
one recommendation. If the user wants a depth in detail, they will say so, and
`$ARGUMENTS` is where that arrives.
