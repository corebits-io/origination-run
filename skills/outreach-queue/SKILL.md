---
name: outreach-queue
description: "Stage approved drafts into a send queue a human works through by hand - sender capacity, per-metro caps, the suppression re-check, send-after dates, follow-up scheduling and the export - without ever sending anything itself. Triggers on: stage the outreach, build the queue, schedule the sequence, who do I send this week, sender capacity, suppression check, export the queue, sequence the follow ups, depth 7."
---

# Outreach Queue

Depth 7. Approved drafts become a week-by-week queue that one person can work
through and follow up properly.

This skill exists because the research made it possible to contact hundreds of
owners and doing so would be the worst use of the work. The queue is where
volume gets converted back into a human pace.

**Read first:** `references/outreach-rules.md` part 1 (volume discipline) and
`references/compliance.md` section 7.

---

## Step 0 — What may be queued

Only rows with an **approved** draft in `outreach.csv` and a route of
`warm-path`, `verified`, `published` or `form-or-phone`.

Never queued, under any circumstances:

- A row with `route_status` of `inferred-DO-NOT-USE`, `linkedin-only` without a
  senior sender, or `not-found`
- A row on `suppression.csv` in any scope
- A draft still at `status` = `draft`, which means a human has not read it
- A second person at a company already in the queue
- A row whose company has been sold since capture

---

## Step 1 — The suppression re-check

Run it again here, against `suppression.csv`, even though depth 1 already did and
routing already did. Three times is not excessive: the list grows during the run,
every opt-out from the last batch landed on it, and the cost of getting this
wrong is contacting somebody who has explicitly asked not to be contacted.

Match on company, domain and owner name, and flag near-matches for a human
rather than resolving them. Then record the check in the log with the date and
the row count.

---

## Step 2 — The caps

| Cap | Source | Default |
|---|---|---|
| First touches per sender per week | mandate section 11 | 20 |
| Companies in one metro per week | `references/outreach-rules.md` | 5 |
| Contacts per company | the rules | 1 |
| Live conversations at once | mandate section 10 | the real constraint |
| Touches per company before stopping | the rules | 3, then dormant |

**The caps hold even when there are more approved drafts than capacity.** Extra
drafts wait a week. Nothing is sent to fill a quota, and a queue that empties in
one week is a queue nobody can follow up.

The metro cap is the one people argue with. It is there because the owners in one
metro and one trade sit on the same association board, use the same bonding
agent, and forward things to each other.

---

## Step 3 — Order the queue

Within the caps, order by:

1. **Signal family rank** from mandate section 9, then signal strength. A
   leadership signal four months old is worth sending this week; a growth signal
   can wait a fortnight
2. **Signal expiry.** A hiring signal expires at 90 days. If it will be stale
   before the queue reaches it, either move it up or drop the quote and rewrite
   the opener
3. **Role**, per the mandate's stated priority for the year
4. **Letters early.** Post takes days to land and weeks to be read

Then set `send_after` on every message. A date, not a position in a list, so the
queue can be worked through on a Monday without recalculating anything.

---

## Step 4 — Schedule the follow-ups

Three touches over four to six weeks, per company:

| Touch | Timing | Condition |
|---|---|---|
| 1 | `send_after` | — |
| 2 | 8-12 days after touch 1 | No reply, and no suppression event |
| 3 | 14-18 days after touch 2 | No reply, and no suppression event |
| then | dormant, with a revisit date | — |

Every follow-up is **conditional on no reply**. A reply cancels the rest of the
sequence immediately, whatever its class, and the conversation moves to the
pipeline. A queue that keeps sending after a reply is the single most damaging
mechanical failure available in outreach, and it is the normal behaviour of most
sending tools unless somebody turns it off.

Stage the follow-ups as `scheduled` rather than approved. A human reads them
again in context before they go, because by then the owner may have said
something that makes the drafted follow-up wrong.

---

## Step 5 — The handover

Produce the queue in three forms, because different people work differently:

**In chat**, grouped by sender and week, each entry showing company, owner,
channel, send-after date, and the subject line.

**In `outreach.csv`**, with `status` = `approved` and the `send_after` dates set.

**As an export**, if the user wants to send from their own tool: one CSV with
exactly the columns that tool needs, and a warning written into the handover that
the tool's own follow-up automation must be switched off, because the reply
condition in step 4 lives here and not there.

### 🚧 HARD GATE

Show the full queue, sender by sender, week by week, with the caps stated and the
suppression re-check recorded. Get approval. Then write.

---

## Step 6 — Report

```
QUEUE STAGED — 2026-10-11
21 approved drafts. 0 sent. Nothing in this package sends.

Suppression re-check     passed. 9 rows on the list, 0 matches in the queue,
                         2 near-matches flagged for a human (similar company
                         names, different companies, both cleared)

Week of 2026-10-13       14 first touches
  R. Okoye     10   6 email, 4 letters
               metros: Atlanta 3, Birmingham 2, Chattanooga 2,
                       Knoxville 2, Columbia 1
  J. Hallam     4   4 email
               metros: Atlanta 2, Nashville 2
               → Atlanta is at 5 for the week, exactly on the cap.
                 Nothing else from Atlanta goes out before the 20th.

Week of 2026-10-20        7 first touches
  R. Okoye      5   3 email, 2 letters
  J. Hallam     2   2 email
  Follow-up 1  14 scheduled, conditional on no reply

Week of 2026-10-27
  Follow-up 1   7 scheduled
  Follow-up 2  14 scheduled

Introductions, not queued     3   R. Okoye to make personally
Held for capacity             0
Held for signal expiry        1   ← Brightwell, hiring signal expires
                                    2026-11-02. Moved to week one.

Pipeline seeded          28 live rows at identified, 21 moving to contacted
                         as the human sends them, 3 as introductions
```

---

## Step 7 — After a human sends

The human sends. Then they tell you what they sent, and you:

- Set `status` = `sent` and `sent_date` in `outreach.csv`
- Set `outreach_status` = `sent` on the target row
- Move the pipeline row to `contacted` with the date and channel
- Set the next action and its date

Nothing moves to `sent` because it was scheduled. It moves because a human said
it went.

---

## Notes

- **There is no send step.** No integration, no API key, no automation hook. A
  language model, two thousand named owners and a regulated activity should not
  share a send button, and the first time that goes wrong it goes wrong at volume
- **A reply cancels the sequence.** Always, immediately, whatever the reply says
- **An opt-out is permanent**, on every channel, with no clever workaround and no
  revisit date
- **The caps are the point.** A user who asks to lift them is asking to spend the
  research on a worse outcome, and the honest answer is the arithmetic from
  intake: twelve conversations is the constraint, not the queue
- **Verify addresses before the first send of a batch.** Published addresses go
  stale, and the domain is worth protecting
