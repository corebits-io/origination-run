---
name: signal-detection
description: "Find the dated, sourced, quotable reason to call a company this quarter across four signal families - leadership and succession, financing, growth, hiring - quoted verbatim with a working URL, aged against a per-family recency window, and rated honestly, with Not found as the normal answer. Triggers on: find signals, timing signals, why call now, succession signals, is the owner retiring, financing signals, trigger events, depth 3, what changed at this company."
---

# Signal Detection

Depth 3. Fit tells you whether a company belongs in the mandate. A signal tells
you why this quarter. They are kept separate on purpose, and PRIORITY requires
both.

This is also the only research in the run whose output goes **verbatim into a
letter to a human being**. That is why the evidence standard here is the
strictest in the package, and why the audit re-checks it at the source URL before
anything is drafted.

**Read first:** `references/evidence-rules.md` — sections 3, 5, 6, 7 and 8;
`MANDATE.md` section 9 for how this buyer ranks the four families.

---

## Step 0 — Preconditions

1. Only rows at `depth` = `2` that survived ownership and economics are in scope
2. Mandate section 9 has the family ranking and the "noise" line. Read the noise
   line twice: in the sample mandate it says trade vacancies are noise, which
   removes the most common false positive in the segment before you start
3. The recency windows from `references/evidence-rules.md`

---

## Step 1 — Search the four families, in the mandate's order

For each row, look for one thing worth saying. Not five.

| Family | Where it actually turns up |
|---|---|
| **Leadership and succession** | Trade press interviews, anniversary pieces, the register (officer appointments and resignations, with dates), association newsletters, award write-ups, obituaries, the company's own "our story" page where it is dated |
| **Financing** | UCC filings and equivalents, new lender of record, refinancing announcements, property transfers and sale-leasebacks, grant and bond registers, local business journals |
| **Growth** | New depot or branch announcements, permit filings, fleet or capacity additions, named contract awards, procurement portals, the company's own news page |
| **Hiring** | Their own careers page, a first controller or CFO or GM posting, senior roles in a new geography |

The two sources people forget: **the register, read for dates** — an officer
resignation in March is a leadership signal with Tier 1 evidence — and **the
trade association newsletter**, which prints exactly the kind of interview that
produces a usable quote.

---

## Step 2 — Capture it properly or not at all

Each signal gets five fields and all five are mandatory:

| Field | Standard |
|---|---|
| `signal` | **The words, verbatim.** Never a paraphrase inside quotation marks |
| `signal_family` | leadership / financing / growth / hiring |
| `signal_source` | A working URL to the page the words are on. Not a domain, not a search result |
| `evidence_date` | `YYYY-MM-DD`. No date means `Not found` |
| `signal_strength` | high / medium / low / `Not found`, per the test below |

If the source says *"we are exploring options for the next phase"*, that is the
quote. Writing *"the founder is looking to sell"* is a fabrication, and it is the
specific kind that ends up in a letter to the founder and gets read aloud back
to you.

Where the signal is a filing rather than a quote, the `signal` field carries the
fact and the filing reference: *"Officer resignation filed 2026-03-11: two of
four shareholders removed from the register."*

---

## Step 3 — Rate it honestly

| Strength | Test |
|---|---|
| **high** | Tier 1 or 2, inside the window, and about a **decision** rather than an atmosphere. Quotable to the owner without embarrassment |
| **medium** | Tier 1-3, inside the window, real but indirect. A first controller hire with no stated reason |
| **low** | Inside the window but thin: one posting, a small headcount move, a vague line |
| `Not found` | Nothing sourced and dated |

Then age it against its family window: hiring 90 days, financing 12 months,
growth 12 months, leadership 24 months. Outside the window, hiring expires
entirely and the others downgrade one level.

**One signal per row, the best one.** Extras go in `notes`. Stacking five weak
signals is how a WATCH becomes a PRIORITY it has not earned, and the owner can
tell when a letter is built on a job posting.

---

## Step 4 — The things that are not signals

- **A founder being sixty-four.** Age is not a signal. A founder saying there is
  nobody in the family to take it on is
- **Anything from a person's private life.** Health, family, divorce, estate
  filings, wealth. Out of scope even where technically public, and in a letter it
  is unforgivable
- **Trade vacancies.** These companies are always hiring tradespeople
- **A rebrand, a new website, a LinkedIn post about a team day out**
- **An undated page that says something interesting.** Tier 4, so `Not found`
- **Your own inference from a cluster of weak facts.** "Three signs point to"
  is not a signal, it is a theory, and it belongs in `notes` if anywhere

---

## Step 5 — Batches of 20 to 30

Report between batches: families found, strength distribution, and the
`Not found` count stated plainly rather than apologized for.

Write after each batch, set `depth` = `3`.

**Expect `Not found` on most rows.** In the sample run, 196 of 524 researched
rows had a dated signal, which is 37%. If a batch comes back with a signal on
every row, signals are being invented or over-rated, and the right response is to
re-read the strength tests rather than to be pleased.

---

## Step 6 — The gate

### 🚧 HARD GATE

Show:

- Signal counts by family and strength
- The `Not found` count and share
- **Every `high` signal in full**, with its quote, URL and date, because these
  are the rows that will become letters
- Any signal you rated `medium` that the mandate's section 9 ranking would
  promote, flagged for the user to read
- Any row where the only available signal was out of scope — age, private life,
  trade vacancies — recorded as `Not found` with a note saying why

Get approval before ranking.

---

## Step 7 — Report

```
SIGNAL DETECTION COMPLETE — 2026-10-09
524 rows researched in 21 batches

With a dated signal      196   (37%)
Not found                328   (63%)   ← the normal result

By family
  leadership              61   ranked 1 in this mandate
  financing               48
  growth                  59
  hiring                  28

By strength
  high                    41   all Tier 1 or 2, all in window, all quoted
  medium                  83
  low                     72   ← these are WATCH rows, not PRIORITY rows

Rejected during research
  age-only inference      34   recorded as Not found
  trade vacancies only    57   noise per mandate section 9
  undated page            22   Tier 4
  private-life material    3   out of scope, not recorded anywhere

Notable
  14 of the 41 high signals are officer changes read straight off the
  register. Free, Tier 1, dated, and nobody else reads them.

Next: fit-ranking on all 2,140 rows.
```

---

## Notes

- **Quote or nothing.** This is the one error class in the package that reaches
  an owner, which is why the audit verifies PRIORITY signals at their URL and the
  drafting step refuses to quote a page that no longer says it
- **No signal is not a failure of research.** It is the condition of most good
  private companies. Half the best conversations in the sample mandate came from
  rows with no signal at all, which is why they stay on the list as WATCH
- **A signal never changes the fit verdict.** It changes timing only
- **Re-read signals on the WATCH pile every quarter.** Hiring expires at 90 days,
  so a three-month-old ranking has a stale timing column, and a signals re-read
  is the cheapest way to refill the top of the funnel. See
  `references/pipeline-stages.md`
