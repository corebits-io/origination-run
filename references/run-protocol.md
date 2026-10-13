# The Run Protocol — Depth, Batches, State and Resume

This is the file that makes a 2,000-row run possible in one command. Everything
else in the package is research rules. This is the engineering.

Three problems have to be solved before volume means anything.

**The context problem.** Two thousand researched rows do not fit in a single
conversation. A run that tries to hold them all forgets the first four hundred,
and the forgetting is silent.

**The cost problem.** Researching ownership, size and signals properly takes
real work per company. Doing it to two thousand companies when a hundred and
ninety were ever going to be worth a letter is the expensive kind of thorough.

**The interruption problem.** A run that takes six working days will be
interrupted. A laptop sleeps, a context window compacts, a Tuesday happens. A
run that cannot resume is a run nobody finishes.

The answers are the depth ladder, the batch ledger and the state file.

---

## 1. The depth ladder

Every row carries a `depth`. Depth is **earned**: a row only gets the expensive
research if it survived the cheap screen.

| Depth | What happens | Runs on | Cost per row | Typical survival |
|---|---|---|---|---|
| **0** | Enumerated from a source, deduped, source string written | everything | near zero | 100% |
| **1** | Desk screen on free, verified facts only | every depth 0 row | very low | 30-45% |
| **2** | Ownership, the sponsor screen, labeled size estimate, platform or add-on role | depth 1 survivors | **high** | 60-70% |
| **3** | The four signal families, quoted, sourced, dated, aged | depth 2 survivors | high | 100% carried, ~35% with a signal |
| **4** | Rubric, ranking, audit | **every row, including the drops** | low | — |
| **5** | The person who can actually sell, and a route to them | PRIORITY rows only | medium | 80-90% |
| **6** | First touch and two follow-ups, drafted | routed rows with something true to say | medium | 85-95% |
| **7** | Staged into the queue and seeded into the pipeline | drafted rows | low | 100% |

The shape of a real run, from `samples/sample-run.md`:

```
depth 0   enumerated          2,140
depth 1   desk screened       2,140   →   792 carried,  1,348 dropped
depth 2   ownership + size      792   →   524 carried,    268 dropped
depth 3   signals               524   →   196 with a dated signal
depth 4   ranked              2,140   →   PRIORITY 31, WATCH 494, PASS 1,615
depth 5   routed                 31   →    28 live, 26 routed, 3 of those warm
depth 6   drafted                 23   →    21 messages, 2 refused
depth 7   queued                  21   →    0 sent. Nothing in this package sends
```

**Read that funnel in both directions.** Left to right it is what the run does.
Right to left it is what the run is for: twenty-one letters worth writing and
three introductions worth making, which took two thousand one hundred and forty
companies to find.

### The rule that keeps the funnel honest

> **A row is only dropped at depth 1 by a free fact that is verified.**

Depth 1 may drop on: a hard geography constraint, a segment boundary, a missing
or inactive licence where the mandate requires one, a public company, a dissolved
entity, a duplicate, or a name on the suppression list. All of those are
checkable at zero cost and either true or not true.

Depth 1 may **never** drop on: an estimated revenue, a headcount proxy, a thin
website, a missing website, no LinkedIn presence, an unrecorded founding year, or
anything else that is absent rather than false.

Breaking that rule is the single most expensive mistake available here, because
it deletes exactly the unmarketed, unaggregated, never-been-called companies the
whole exercise exists to find, and it does it silently in the cheapest step.

---

## 2. Work backwards from conversations

Enumeration is a coverage number. Conversations are the constraint. Do this
arithmetic at intake, before sourcing anything, using mandate section 10.

```
Conversations you can hold at once                        12
Realistic reply rate on a good proprietary first touch    8-15%
                                                          ↓
First touches needed to fill that                         ~100 over a quarter
Of PRIORITY rows, share that get a usable route           ~85%
                                                          ↓
PRIORITY rows needed                                      ~120 per quarter
PRIORITY share of a properly screened list                4-8%
                                                          ↓
Rows needing depth 2 and 3                                ~700-900
Depth 1 survival in a tight segment                       30-45%
                                                          ↓
Enumeration target                                        ~2,000
```

That is where the two thousand comes from. It is not a vanity number and it is
not a sending plan. **Two thousand enumerated is a coverage claim. Two thousand
contacted is a mistake**, and the kind that ends with an owner forwarding your
email to your own platform's largest customer.

If the arithmetic says the enumeration target the user wrote is far larger than
their conversation capacity needs, say so at intake and offer the smaller number.
A tighter segment beats a bigger list every time.

---

## 3. Batch sizes

Work in batches, write after each one, report between them. A two-hundred-row
pass with one report at the end is a pass nobody can correct mid-flight.

| Depth | Batch size | Report between batches |
|---|---|---|
| 0 | one source at a time | counts, cap detail, new vs duplicate |
| 1 | 100-200 rows | drop reasons by category, carry rate, 10 sample carries and 10 sample drops |
| 2 | 20-30 rows | ownership distribution, sponsor hits by name, verified vs estimated |
| 3 | 20-30 rows | signal families found, strength distribution, `Not found` count |
| 4 | the whole list, in the fixed rubric order | distribution, then the audit |
| 5 | 10-20 rows | route types, rows with no route |
| 6 | 5-10 messages | every draft in full, with its checks |
| 7 | one week of queue | the staged queue, sender by sender |

**Write to disk after every batch.** Not at the end of the depth. The state file
and the CSV are the run; the conversation is just where you are standing.

---

## 4. The state file

One file, `run/state.json`, written after every batch and every gate.

```json
{
  "run_id": "SE-ELEC-Q4",
  "mandate_file": "MANDATE.md",
  "started": "2026-10-02",
  "updated": "2026-10-11",
  "phase": "outreach-build",
  "phase_status": "awaiting-approval",
  "awaiting": "approval of outreach batch B01, 8 drafts",
  "caps": {
    "enumeration_target": 2000,
    "depth2_cap": 800,
    "priority_route_cap": 40,
    "first_touches_per_sender_per_week": 20
  },
  "depth_counts": {
    "0": 2140, "1": 2140, "2": 792, "3": 524,
    "4": 2140, "5": 31, "6": 28, "7": 23
  },
  "verdicts": { "PRIORITY": 31, "WATCH": 494, "PASS": 1615 },
  "batches": [
    { "id": "D2-07", "depth": 2, "rows": "151-175", "state": "done", "date": "2026-10-07" },
    { "id": "D2-08", "depth": 2, "rows": "176-200", "state": "done", "date": "2026-10-07" },
    { "id": "D6-01", "depth": 6, "rows": "8 drafts", "state": "awaiting-approval", "date": "2026-10-11" }
  ],
  "gates": [
    { "gate": "intake", "approved": true, "date": "2026-10-02" },
    { "gate": "market-map", "approved": true, "date": "2026-10-03" },
    { "gate": "sourcing", "approved": true, "date": "2026-10-04" },
    { "gate": "screen", "approved": true, "date": "2026-10-04" },
    { "gate": "rubric", "approved": true, "date": "2026-10-09" },
    { "gate": "ranking", "approved": true, "date": "2026-10-10" },
    { "gate": "outreach", "approved": false, "date": null }
  ],
  "open_questions": [
    "3 rows: licence address is a registered agent, operations may be in-state. User to confirm whether to re-screen.",
    "Pembury add-on radius: does the 90 miles run from Nashville city or the Pembury yard?"
  ],
  "known_gaps": [
    "Alabama roster capped at 500 per query, pulled per county, 2 counties still truncated, ~180 rows estimated missing."
  ]
}
```

Rules for the state file:

- **Write it after every batch.** It is the only thing standing between an
  interruption and a lost run
- `phase_status` is one of `running`, `awaiting-approval`, `blocked`, `done`
- Never move a gate to `approved: true` without the user actually approving it.
  The gate list is the audit trail of what a human agreed to
- `open_questions` carries anything the run could not decide. It gets read back
  at the next gate rather than quietly resolved
- `known_gaps` carries every capped source pull and every coverage hole, for the
  life of the run. A truncated pull looks exactly like a complete one six weeks
  later

---

## 5. Resume

`/originate` is one command whether it is starting a run or continuing one.

**On every invocation, in this order:**

1. Look for `run/state.json`. If there is none, this is a new run: go to intake
2. If there is one, read it, read `targets.csv`, and **recount from the CSV**.
   The CSV is the source of truth, the state file is the bookmark. Where they
   disagree, the CSV wins and the state file gets corrected
3. Report where the run actually is: phase, depth counts, what the last batch
   did, what is awaiting approval, every open question
4. If `phase_status` is `awaiting-approval`, re-present that gate. Do not
   continue past it because it was presented once already
5. If a batch is `in-progress`, redo it. A half-written batch is not a saved
   batch. Rows are keyed by company and domain, so redoing one is idempotent
6. Otherwise, pick up at the next batch in the ledger and carry on

**Never restart a run from zero because resuming looks complicated.** Depth 2 is
the expensive part and re-researching five hundred rows that were already done is
the costliest possible way to be tidy.

### After a context compaction

The conversation may lose the detail of what happened. The files do not. Re-read
`run/state.json`, `targets.csv` and the last entries in `run/log.md`, say plainly
what you have re-established and what you cannot, then carry on from the ledger.

### `run/log.md`

A human-readable append-only companion to the state file. One short entry per
batch and per gate: what ran, what it found, what the user approved, what
changed. This is what the Monday morning question gets answered from, and it is
what a partner reads instead of the state file.

---

## 6. The seven gates

One command, seven places it stops. Nothing writes to a CSV before its gate.

| # | Gate | What it shows | What approval means |
|---|---|---|---|
| 1 | **Intake** | the funnel arithmetic, the rewritten must-haves, the principal-buyer answer, the caps | the run plan is right |
| 2 | **Market map** | segment economics, who is consolidating, where the companies are findable, the verdict | source it, or do not |
| 3 | **Sourcing** | counts by source, the dedupe number, the coverage log and bias statement, 15 sample rows | the population is the right population |
| 4 | **Screen** | drop counts by reason, the carry rate, 10 carries and 10 drops in full | the cheap pass has not deleted the proprietary end of the list |
| 5 | **Rubric** | every criterion, the mandate section it came from, the test, the bucket effect | the ranking rules, **before any row is ranked** |
| 6 | **Ranking** | the distribution, the PRIORITY rows in full, the audit with every correction | the list |
| 7 | **Outreach** | every draft in full with its checks, the queue by sender and week | these messages may be sent by a human, by hand |

Plus a report between every batch inside depths 1, 2, 3, 5 and 6. Those are
reports, not gates: they do not need approval, they need to be seen.

**Gates are never batched up and presented together at the end.** The point of a
gate is that the work after it has not happened yet.

---

## 7. Stop conditions

The run stops and asks rather than carrying on, when:

| Condition | Why it matters |
|---|---|
| Depth 1 carry rate below 15% | The population is wrong, not the companies. Re-aim sourcing |
| Depth 1 carry rate above 70% | The segment boundary is loose. The screen is not screening |
| Sponsor-owned above 40% at depth 2 | The segment is consolidated. The map should have caught it. Worth stopping to reconsider the whole mandate |
| PRIORITY above 25% of ranked rows | The rubric is flattering the user |
| PRIORITY below 1% on a list over 500 | Usually the signals pass has not run, or there are too many must-haves |
| A source pull capped and not reruns | Record it in `known_gaps` and say so at the gate. Do not silently proceed |
| Fewer routes than the mandate needs | Say it. Do not fill the gap with guessed addresses |
| The depth 2 cap is reached | Stop. Report what is researched and what is waiting. Do not quietly spend another month of budget |

---

## 8. What the run costs, honestly

A two-thousand-row run is hours of Claude Code spread over days, not minutes.
The sample run took roughly fourteen hours of working time across six working
days, and about sixty percent of it was depth 2.

It replaces a job that takes an associate a month and produces a worse list,
because an associate gets bored at row four hundred and the system does not. But
telling somebody a single prompt returns two thousand researched companies in an
afternoon is a lie, and they will find out at hour two.

Say the real number at intake, along with the depth 2 cap, so the user chooses
the budget before it is spent instead of after.

---

## 9. Non-negotiables

- **Nothing is deleted.** A drop is a row with `screen_result` = `drop`, an
  `excluded_by` reason, and eventually a PASS verdict. Deleted rows get
  rediscovered and re-researched next quarter
- **Write after every batch**
- **The CSV is the source of truth.** The state file is a bookmark
- **Depth is earned, never granted.** No row reaches depth 2 without surviving
  depth 1, and no row reaches depth 6 without a route and something true to say
- **Unknown is not failed, at every depth**
- **Nothing sends.** Depth 7 stages a queue. A human sends it, by hand, after
  reading it
