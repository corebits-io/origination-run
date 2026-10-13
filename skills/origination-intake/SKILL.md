---
name: origination-intake
description: "Check an acquisition mandate is complete enough to run at volume, run the principal-buyer gate, rewrite untestable must-haves into tests, and do the funnel arithmetic that sets the enumeration target, the deep-research cap and the weekly outreach ceiling before anything is sourced. Triggers on: start a run, originate, check my mandate, set up the origination run, how many companies should I enumerate, scope the run, intake, is my buy box ready."
---

# Origination Intake

The first job is not research. It is making sure the mandate can be run against,
and that the volume the user has in mind is the volume their calendar can
survive.

Two thousand enumerated companies is a coverage claim. Two thousand contacted
owners is a mistake. Intake is where that distinction gets made, in numbers, with
the user, before any money or time is spent.

**Read first:**
- `MANDATE.md` in the working folder. If it does not exist, offer to fill one out
  section by section from `templates/MANDATE.md`. **Research nothing first**
- `references/run-protocol.md` — sections 1, 2 and 7
- `references/compliance.md` — section 1

---

## Step 1 — The principal-buyer gate

Read mandate section 1 before anything else.

| Answer | What you do |
|---|---|
| Buying for their own account, no transaction-based compensation from a third party | Continue |
| Earns a success fee for arranging a purchase somebody else makes | **Stop the run.** Explain the broker-dealer question plainly, tell them to talk to securities counsel, and do not research or write to anybody on their behalf |
| `TBD` | **Stop and ask.** Do not assume the benign answer |

This gate has no override. If the user says it is fine, the answer does not
change. Say that once, without lecturing, and leave the run stopped.

Then check: is the capital status in section 1 consistent with what section 1
says they may claim in a message? A fund that is still raising cannot say
"committed capital". Flag the mismatch now, because by depth 6 it is a sentence
in a letter to an owner.

---

## Step 2 — Completeness check

Walk the mandate and report what is missing. These are the sections a run cannot
proceed without:

| Section | Needed for | If it is empty or `TBD` |
|---|---|---|
| 1 | the gate above | stop |
| 3 size box | the economics test | stop and fill it |
| 4 sectors and segments | the segment boundary | stop. "Business services" is not a segment |
| 5 geography | the free depth 1 drop | stop |
| 6 must-haves | the rubric | stop |
| 7 ownership types | the ownership test | stop |
| 2 named platforms | the add-on verdict | continue, but every add-on call will be `Not found`. Say so now |
| 8 suppression | the depth 1 check | continue, and warn that nothing is suppressed |
| 9 signal ranking | what promotes a row | continue with the default order: leadership, financing, growth, hiring |
| 10 volume | the caps | do the arithmetic in step 4 and propose the numbers |
| 11 senders | depth 6 | continue. Flag that no message can be drafted until it is filled |
| 12 channels and counsel | depth 6 and 7 | continue. Flag the same |

Report it as a list, not as a conversation. The user should see the whole gap at
once.

---

## Step 3 — Challenge the must-haves

A must-have that cannot be tested from a public source is not a must-have, it is
a hope, and it will quietly fail every row on the list.

For each one in section 6, write the test a researcher would actually run. Where
there is no test, propose a rewrite and get it agreed.

| What they wrote | What it becomes |
|---|---|
| "Strong management team" | "A named second-tier manager who is not the owner and not a family member, found on the team page, in the officer filings, or in trade press" |
| "Good reputation" | "No open regulatory action in the last 24 months, and a licence in good standing" |
| "Recurring revenue" | "Service, maintenance or contract revenue at or above X%, evidenced by an owner statement, service-agreement language on their own site, or a run of recurring awards" |
| "Growing" | A timing signal, not a must-have. Move it to section 9 |
| "Sophisticated systems" | Usually unknowable before a call. Drop it, or accept it as a question for the first conversation |

Then say the uncomfortable thing if it is true: **more than five must-haves and
nothing survives the rubric.** Three real requirements produce a list where the
survivors mean something. Offer the cut.

Also check for a must-have that is really an exclusion (it belongs in section 8)
and a must-have that is really a preference (it belongs in the ranking, not the
gate).

---

## Step 4 — The funnel arithmetic

Do this out loud, with the user, using mandate section 10. It is the most useful
five minutes in the whole run.

Work **backwards from conversations**:

```
Conversations you can hold at once                       from section 10
Reply rate on a good proprietary first touch             8-15%
First touches needed                                     conversations / rate
Share of PRIORITY rows that get a usable route           ~85%
PRIORITY rows needed                                     touches / 0.85
PRIORITY share of a properly screened list               4-8%
Rows needing depth 2 and 3                               PRIORITY needed / 0.06
Depth 1 survival in a tight segment                      30-45%
Enumeration target                                       depth 2 rows / 0.37
```

Then show the forward funnel with the numbers filled in, and set three caps:

- **Enumeration target** — what sourcing aims at
- **Depth 2 cap** — how many rows get the expensive research this month
- **Weekly first touches** — per sender, from section 11, and the metro cap from
  `references/outreach-rules.md`

**Say the real cost.** A two-thousand-row run is hours of Claude Code spread
over days, around sixty percent of it in depth 2. The user chooses that budget
now, not at hour two.

If the enumeration target in section 10 is far larger than the arithmetic needs,
say so and offer the smaller number with a tighter segment. A narrower segment at
half the volume beats a loose one at twice.

---

## Step 5 — Scope this run

One segment, one geography, one run. Two segments at once produce a list where
nothing is comparable and a rubric that fits neither.

Write the run plan:

```
RUN PLAN — SE-ELEC-Q4

Mandate            Kestrel Lane Capital, commercial electrical and building
                   systems integration, GA / TN / AL / SC
Buyer status       Principal, committed fund. Gate passed.
Size box           $8-60M revenue, $1.2-6M EBITDA. Real constraint: EBITDA floor
Must-haves         4, all rewritten as tests (see below)
Platforms named    2 — Calder (Atlanta), Pembury (Nashville). Add-on verdicts
                   are testable
Suppression        9 rows loaded: 2 opt-outs, 4 Calder subcontractors,
                   3 cold-only relationships

Funnel             12 conversations → ~100 first touches → ~120 PRIORITY
                   → ~800 researched → 2,000 enumerated
Caps               enumeration 2,000 | depth 2 cap 800 | 20 touches per sender
                   per week, 5 per metro per week
Cost               roughly 12-16 hours of working time over about 6 days,
                   ~60% in depth 2

Gaps to fix now    Section 11 sender capacity blank for R. Okoye
                   Section 12 postal address blank, needed before any email
Challenges         Must-have 3 "recurring revenue" rewritten as a 40% test
                   Must-have 5 "sophisticated systems" proposed for cutting
Open questions     Does the 90-mile add-on radius run from Nashville city or
                   the Pembury yard?
```

### 🚧 HARD GATE

Show the run plan, every challenge, every gap, and the funnel arithmetic. Get
approval before the segment map runs.

Then write `run/state.json` with the caps, the gate record and the open
questions, and open `run/log.md`.

---

## Step 6 — If the user already has a list

Common, and it changes the run.

Ask what it is and where it came from. Then:

- **Map their columns onto `templates/targets.csv`** and load the rows at depth
  0 with the source string recorded as what it actually is, including the
  provider name and the export date
- **Flag every email address on it as `inferred-DO-NOT-USE`** until independently
  verified. A purchased address is an unverified invention until proven otherwise
- **Load it as a cross-find, not as the spine.** A bought list carries the bias
  of whoever built it, and the whole point of the run is to find the companies
  that are not on it. Enumerate the rosters anyway, then let the overlap tell you
  how much of their list was already the well-marketed end of the market
- Say what the overlap means when you see it. If 90% of a bought list appears in
  the licence roster, the roster was always the better source. If 40% of it
  appears nowhere on a Tier 1 source, be suspicious of those rows rather than
  pleased with them

---

## Notes

- **Never research during intake.** Not one company. Intake is about the
  mandate, and a run that starts sourcing before the box is tested inherits
  every ambiguity in it
- **`TBD` is an answer that stops the run** on sections 1, 3, 4, 5, 6 and 7, and
  a flag on the rest
- **Do the arithmetic even when the user resists it.** The number that matters is
  the conversations, and a user who has not looked at that number is about to
  ask for four thousand rows
- **Record every challenge in `run/log.md`**, including the ones the user
  overruled. In six weeks, when a verdict is being argued about, the record of
  what was agreed is worth more than the verdict
