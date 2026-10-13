# Pipeline Stages, Reply Classes and the Loop Back to Sourcing

Proprietary deals are lost to forgotten follow-ups far more often than to losing
bidders. The owner who said "call me in the spring" and never got the call sells
to whoever did.

One row per **conversation**, not per company. A broker taking over an owner
thread is a new row, because it is a new conversation with its own state.

---

## Stages

| Stage | Meaning | Must have |
|---|---|---|
| `identified` | On the ranked list, not contacted | a verdict |
| `qualified` | PRIORITY or promoted WATCH, with a route | a route, a sender |
| `contacted` | First touch sent by a human | date, channel |
| `in-dialogue` | The owner is talking | **next action and date** |
| `nda-signed` | Confidentiality in place | `nda_status`, date |
| `ioi-sent` | Indication of interest delivered | range, date |
| `loi-sent` | Letter of intent delivered | terms summary, expiry |
| `diligence` | Under LOI, in diligence | workstream list |
| `closed` | Completed | date. **Only after signing and funding** |
| `passed` | You declined | reason |
| `not-selling` | The owner declined, final | reason, opt-out flag if any |
| `dormant` | Parked, real future potential | **a revisit date** |

### Rules

1. **Every row in an active stage needs a `next_action` and a
   `next_action_date`.** No exceptions. A conversation with no next action is one
   you have already lost, you just do not know yet
2. **Do-not-contact is permanent.** It goes in `suppression.csv` as well as the
   pipeline row, and it is never revisited on any channel
3. **`dormant` needs a real revisit date**, taken from what the owner actually
   said. "After tax season" becomes a date
4. **Never delete a row.** Close it with a reason. Over a multi-year search the
   history is the value
5. **Log the touch the day it happens.** A pipeline reconstructed from memory on
   Friday is fiction

---

## Reply classes

| `reply_class` | What it means | What happens |
|---|---|---|
| `interested-now` | Wants to talk | Stage to `in-dialogue`, next action within 48 hours |
| `interested-not-now` | A real maybe with a time attached | `dormant` with the date they gave |
| `wants-info` | Asking who you are, what you buy | Answer plainly. Still `in-dialogue` |
| `referred-to-intermediary` | "Talk to my broker" or "my accountant handles this" | Respect it. Route to the named person, new row |
| `in-process` | Already in a live sale process | Follow the mandate. If it says do not go around a retained banker, write to the banker |
| `not-selling` | A clear no | Close as `not-selling`. No further touches in this sequence |
| `do-not-contact` | Asked to be left alone | **Suppression, permanent, all channels.** Close the row |
| `wrong-person` | Not the owner, or cannot sell | Back to depth 5. Do not re-send a first touch to the same company for 90 days |
| `bounce` | Undeliverable | Mark the route dead. Never try a guessed variant |
| `no-reply` | Nothing after the sequence ended | `dormant`, revisit in 6 to 12 months |

Three of these are the ones people get wrong. A polite "not right now" is not
interest, and recording it as `interested-not-now` without a date is how a
pipeline fills with rows nobody will ever call again. "Talk to my broker" is
information, not a rejection, and if it keeps happening the right response is a
policy decision about brokered processes, not thirty individual judgment calls.
And a bounce is a dead route, never an invitation to try `firstname@` instead.

---

## Probability

Coarse and honest. Precision here is false precision.

| Stage | Realistic |
|---|---|
| `contacted` | 1% |
| `in-dialogue` | 5% |
| `nda-signed` | 15% |
| `ioi-sent` | 25% |
| `loi-sent` | 45% |
| `diligence` | 65% |
| `closed` | 100% |

**A signed LOI is not a deal.** Diligence kills more deals than negotiation
does, and one live LOI is the most common reason a firm stops doing top-of-funnel
work and has nothing six months later.

---

## The daily view

Lead with what is overdue. That is the entire point of it.

```
TODAY — 2026-11-09

Overdue (3)
  Ridgeline Electric     promised the buyer one-pager 4 days ago, not sent
  Calderwood Systems     follow-up was due 2026-11-05
  Tarrant Controls       call was 6 days ago, no recap sent

Due today (2)
  Hallam Power           send the NDA draft they asked for
  Brightwell Electric    owner said "call after the trade show", it ended Friday

Awaiting their reply (5)
  ...

Dormant revisits this month (2)
  Vance Mechanical       owner said "after my season ends in September"

2 rows in an active stage have no next action:
  Marchmont, Dunbar Systems    set one or close them
```

---

## The weekly read

Funnel, movement, conversion, and then the one line that matters.

```
PIPELINE — week ending 2026-11-06
Mandate: commercial electrical and building systems, GA/TN/AL/SC

Funnel            identified   2,140
                  qualified       28
                  contacted       21
                  in-dialogue      4
                  nda-signed       1
                  ioi-sent         0
                  dormant          6   nearest revisit January (2 rows)
                  not-selling      5   1 opt-out, permanent
                  passed           1

Movement          +2 in-dialogue, +1 nda-signed, +3 dormant with dates set

Conversion        contacted → in-dialogue    17%
                  in-dialogue → nda-signed   25%

Constraint        Top of funnel. 21 contacted is not a pipeline. At this
                  conversion, one closed deal needs roughly 300 contacted.
                  There are 494 WATCH rows researched and unqueued; the
                  cheapest next move is a signals re-read on the top 150,
                  not another enumeration run.

Overdue           3
Needs you         Dunbar Systems: owner asked what we would pay. Policy call.
```

**Name the constraint.** A summary that does not say what is actually blocking
the search is a status report, not a useful one.

---

## The loop back into the run

This is what makes the pipeline part of the system rather than a spreadsheet at
the end of it. When the weekly read says top of funnel is the constraint, there
are four moves, in ascending order of cost:

1. **Re-read signals on the WATCH pile.** Hiring signals expire at 90 days, so a
   three-month-old ranking has a stale timing column and some of those rows are
   PRIORITY now. Cheapest move available, and the most commonly skipped
2. **Route and draft for the top WATCH rows.** They fit. They always fitted
3. **Run depth 2 on the rest of the depth 1 survivors.** The run stopped at the
   cap, not at the end of the list
4. **Enumerate again** — a new geography, an adjacent segment, a new source
   tier. The most expensive move, and the first one everybody reaches for

A pipeline that only ever triggers option 4 is a sign that the first run's
research is being thrown away every quarter.
