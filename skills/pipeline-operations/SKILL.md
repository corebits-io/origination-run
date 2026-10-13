---
name: pipeline-operations
description: "Run the deal pipeline after the first touches go out: log every reply and call in the owner's own words, classify replies, move stages, surface what is overdue, produce the weekly read that names the constraint, and decide which upstream move refills the top of the funnel. Triggers on: pipeline, update the pipeline, log this call, what needs follow up, who owes me a reply, overdue, weekly summary, where are we, classify this reply, deal status, the owner replied."
---

# Pipeline Operations

The memory of the search. Every conversation, every stage change, every next
action, in one file somebody can actually read on a Monday.

Proprietary deals are lost to forgotten follow-ups far more often than to losing
bidders. The owner who said "call me in the spring" and never got the call sells
to whoever did.

**Read first:** `references/pipeline-stages.md` for the stages, the reply
classes, the probabilities and the shape of the daily and weekly views. This
skill is the procedure around them.

---

## Step 0 — Load

1. `MANDATE.md` for the buyer identity, the size box and the deal target
2. `pipeline.csv`, created from `templates/pipeline.csv` if absent
3. `targets.csv` and `outreach.csv`, which are where the row came from
4. `suppression.csv`, which this skill writes to

One row per **conversation**, not per company. A broker taking over an owner
thread is a new row, because it is a new conversation with its own state.

---

## Step 1 — Logging a reply

When the user forwards a reply or describes a call, capture:

- **What was actually said**, in the owner's words where the words matter
- **Any number discussed, and who said it.** An owner's "I would want at least
  8x" is their statement, not a valuation, and it goes in
  `valuation_discussed` attributed to them
- What they asked for, and what was promised, by when
- NDA status and anything confidentiality touches
- The next action and its date

Then classify it per `references/pipeline-stages.md`, move the stage, and set a
next action with a date.

### Note discipline

Notes get read back later, sometimes by partners, lenders or counsel, and
occasionally by the owner if a thread gets forwarded.

- **Facts, not interpretation.** "Said revenue is around $9M" not "doing well"
- Never speculate about an owner's health, family, finances or motives
- **Quote commitments exactly.** "I will think about it" is not "interested in
  our LOI"
- Assume every note could be read back to the person in it, because in some
  jurisdictions they have the legal right to ask

---

## Step 2 — The three replies that get mishandled

**"Not right now."** It is a real maybe, and it is only useful with a date
attached. Turn what they said into a date — "after tax season" becomes a date —
and set the revisit. A `dormant` row with no date is a row nobody will ever call
again.

**"Talk to my broker."** Information, not a rejection. Route to the named person
as a new row. If it happens three times in a batch, that is a policy decision
about brokered processes to make once, not thirty individual judgment calls.

**A bounce.** A dead route. Mark it dead and never try a variant. A guessed
address after a bounce is how a sending domain dies, and the row was worth more
than that.

---

## Step 3 — Suppression is immediate

A `do-not-contact` reply writes to `suppression.csv` **in the same action** as
the pipeline update. Scope `all`, permanent, no revisit date, and the pipeline
row closes as `not-selling` with the opt-out flag set.

Then check the queue: cancel every scheduled follow-up for that company, and say
that it has been done.

A reply of any class cancels the rest of that company's sequence. Say that out
loud when you log it, because the most common mechanical failure in outreach is
a follow-up arriving after a reply.

---

## Step 4 — The daily view

On request, or whenever the user asks what needs doing. **Lead with overdue.**
That is the entire point of the view.

Overdue, due today, awaiting their reply, dormant revisits this month, and then
the list of rows in an active stage with no next action — because those are
conversations already lost that nobody has noticed yet.

---

## Step 5 — The weekly read

Funnel, movement, conversion, constraint, overdue, needs-you. The shape is in
`references/pipeline-stages.md`.

Two rules about it.

**Name the constraint.** A summary that does not say what is blocking the search
is a status report, not a useful one. The constraint is almost always top of
funnel, and saying so when there is one live LOI on the table is the most useful
unwelcome sentence available.

**Do not inflate probability.** The weighted view exists to stop the user
feeling finished. A signed LOI is not a deal, and diligence kills more deals than
negotiation does.

---

## Step 6 — The loop back into the run

This is what makes the pipeline part of the system rather than a spreadsheet at
the end of it.

When the weekly read says top of funnel is the constraint, there are four moves,
cheapest first:

1. **Re-read signals on the WATCH pile.** Hiring signals expire at 90 days, so a
   three-month-old ranking has a stale timing column and some of those rows are
   PRIORITY now. Run `signal-detection` on the top of the WATCH pile
2. **Route and draft for the top WATCH rows.** They fit. They always fitted
3. **Run depth 2 on the remaining depth 1 survivors.** The run stopped at the
   cap, not at the end of the list
4. **Enumerate again.** New geography, adjacent segment, new source tier

Say which one, with the row counts to back it. A search that only ever reaches
for option 4 is throwing away the research it already paid for, every quarter.

---

## Step 7 — Writing changes

### 🚧 HARD GATE — before writing

Show every proposed change: new rows, stage transitions, closures with reasons,
and anything written to `suppression.csv`.

Flag any stage jump that skips `nda-signed` before an IOI. Flag any `closed`
row, and confirm signing **and** funding actually happened before writing it.

Get approval. Then write, and update `updated_date` on every touched row.

---

## Notes

- **Update it the same day.** A pipeline reconstructed from memory on Friday is
  fiction
- **The overdue list is the most valuable output.** Show it first, every time
- **Never delete a row.** Close it with a reason. Over a multi-year search the
  history is the value, and the row you closed in March is the conversation you
  reopen in two years
- **Never mark `closed` before signing and funding.** Not at LOI, not at a
  handshake
- **Watch for stalls.** Anything in `in-dialogue` or later for more than 30 days
  with no movement is stuck. Say so, and say what would unstick it
- **If the user exports to a real CRM**, keep `pipeline.csv` as the source of
  truth and export from it. Two-way sync between a file and a CRM goes wrong
  quietly
