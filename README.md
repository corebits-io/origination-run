# The Origination Run

Type one command. Two thousand off-market companies get enumerated, screened,
researched, ranked and routed, and what comes out the far end is twenty or so
letters to owners that are actually worth writing.

Eleven skills, five agents, one command and a state file that lets a six-day run
survive being interrupted.

Built for PE funds, family offices, search funds, independent sponsors, holdcos
and corporate development teams that want proprietary deal flow without a
ten-person origination desk.

Runs on [Claude Code](https://www.anthropic.com/claude-code) and local files.
No database, no API keys, no signups.

---

## 👉 Start here: [SETUP.md](./SETUP.md)

Twenty minutes from zero to a run in flight. Every step in plain English.

Want to see the end product first?
**[samples/sample-run.md](./samples/sample-run.md)** is a complete finished run,
invented end to end — the funnel, the audit, two of the actual letters — so you
know exactly what you are getting before you install anything.

---

## Came from the LinkedIn post? — this is the system

### One command

Fill in one file, then type:

```
/originate
```

That is the whole interface. It runs five steps across seven phases, stops at
every phase boundary to show you its work, and **picks up where it left off** if
you close the laptop, run out of day, or come back on Thursday.

| The post said | The system does |
|---|---|
| **1.** Finds companies across industries, geographies and EBITDA ranges | Enumerates the whole population from licence rosters, registries, association directories, installer locators, exhibitor lists and award records — the sources bought lists never cover |
| **2.** Researches founder ownership, leadership and decision-makers | Establishes ownership from filings and registers with an evidence tier on every claim, then finds the person who can actually sell and an honest route to them |
| **3.** Detects acquisition signals: growth, funding, ownership changes | Four signal families, quoted verbatim, sourced to a working URL, dated, and aged against a per-family recency window |
| **4.** Ranks businesses by buy-box fit, ownership signals and relevance | PRIORITY / WATCH / PASS against a rubric you approve before a single row is ranked, then a five-part audit that hunts its own false negatives |
| **5.** Builds your outreach pipeline | The person, the route, the first touch and two follow-ups, a queue inside sender and per-metro caps, and a pipeline that starts the day you send |

### The honest version of "2,000 targets"

```
depth 0   enumerated          2,140
depth 1   desk screened       2,140   →   792 carried,  1,348 dropped
depth 2   ownership + size      792   →   524 carried,    268 dropped
depth 3   signals               524   →   196 with a dated signal
depth 4   ranked              2,140   →   PRIORITY 31, WATCH 494, PASS 1,615
depth 5   routed                 31   →    26 with a route, 3 of them warm
depth 6   drafted                23   →    21 messages, 2 refused
depth 7   queued                 21   →     0 sent
```

Read it right to left. **Two thousand enumerated is a coverage claim. Two
thousand contacted is a mistake** — the kind that ends with an owner forwarding
your email to one of your own portfolio company's customers.

The funnel is the product. Research depth is **earned**: a row only gets the
expensive research if it survived the free screen, which is what makes two
thousand rows affordable in the first place.

---

## The eleven skills

| Skill | What it does |
|---|---|
| `origination-intake` | Checks the mandate can be run against, rewrites untestable must-haves into tests, and does the funnel arithmetic backwards from the conversations you can actually hold. Runs a principal-buyer gate that has no override |
| `segment-mapping` | Maps the segment the mandate implies: boundary, fragmentation, the segment economics every later estimate depends on, the typical owner, who is already consolidating, where the companies are findable. Ends with a verdict that is sometimes "do not source this segment" |
| `population-sourcing` | Enumerates the whole population, one source at a time, with a ledger per pull, honest cap reporting, dedupe at scale, and a coverage log that names what the pull missed |
| `desk-screening` | The free pass over every row. Drops on facts that are **false**, never on facts that are **absent** |
| `ownership-and-size` | Who actually owns it, the four-part sponsor screen, labeled revenue and EBITDA ranges for companies that publish nothing, and the platform or add-on call |
| `signal-detection` | The four families — leadership, financing, growth, hiring — quoted, sourced, dated, aged, rated |
| `fit-ranking` | Builds a rubric from your mandate, gets it approved before ranking a single row, ranks every row identically, then audits itself |
| `owner-contact-routing` | The person who can actually sell, and a route that reaches them. Never a guessed email address |
| `owner-outreach-drafting` | A first touch and two follow-ups, short and plain, specific from the researched row. Refuses to write where there is nothing true to say |
| `outreach-queue` | Sender capacity, per-metro caps, the suppression re-check, send-after dates, follow-ups conditional on no reply |
| `pipeline-operations` | Every reply logged in the owner's words, overdue surfaced first, the weekly read that names the constraint |

Install, then run `/skills` to see all eleven.

## The five agents

| Agent | Owns |
|---|---|
| `origination-sourcer` | depths 0-1. Mandate, map, population, screen |
| `target-analyst` | depths 2-3. Ownership, sponsor screen, size, role, signals |
| `fit-ranker` | depth 4. Rubric, ranking, audit |
| `outreach-builder` | depths 5-7. Routes, drafts, queue. Sends nothing |
| `pipeline-keeper` | the pipeline, from the first touch onward |

Install, then run `/agents` to see all five.

> Both lists are the same system. The agents run the skills.

---

## What every row comes back with

| Field | What it holds |
|---|---|
| `depth` | how far this row got, 0 to 7, and therefore what it cost |
| `source` | specific enough that somebody else could re-run the pull |
| `screen_result`, `screen_reason` | carried or dropped at depth 1, and on which free verified fact |
| `ownership_type`, `ownership_evidence`, `evidence_tier` | who owns it, what establishes that, how good the evidence is |
| `sponsor_screen` | the four checks that catch a company already bought but still marketing itself as family owned |
| `est_revenue`, `est_ebitda`, `financial_confidence` | a range, labeled an estimate, with its method and inputs in the same cell |
| `fit_role`, `fit_role_reason` | platform or add-on, and for an add-on, the named platform it attaches to |
| `signal`, `signal_source`, `evidence_date`, `signal_strength` | the reason to call this quarter, quoted verbatim, with a working URL and a date |
| `verdict`, `fit_reason`, `excluded_by` | PRIORITY / WATCH / PASS, and the rules that fired |
| `owner_name`, `owner_title`, `owner_evidence` | the person who can actually sell, and what proves it |
| `contact_route`, `route_status` | how you reach them, and how confident that is. Never a guess |
| `outreach_status`, `batch` | where it sits in the queue |

**Three verdicts, not a score out of 100.** A number between 1 and 100 invites an
argument about whether a 71 beats a 68 and tells nobody what to do on Monday.

**PRIORITY** — strong mandate fit, and a dated reason to engage now
**WATCH** — fits the thesis, needs a better trigger or a missing fact
**PASS** — wrong ownership, economics, geography or strategic fit

---

## The rules that make it trustworthy

Any system can return two thousand ranked rows. These are the rules that decide
whether the ranking means anything.

- **Unknown is not failed.** `Not found` revenue is not a failed size test.
  Ranking gaps as negatives systematically deletes the least-marketed companies,
  which is to say the proprietary ones
- **Drop on facts that are false, never on facts that are absent.** No website,
  no headcount, no LinkedIn page, no founding year: all carry forward. This is the
  single most expensive rule to break, and the cheapest step is where it happens
- **Estimates are labeled, and the label travels with the number.** A labeled
  estimate outside your size box makes a row WATCH, never a drop. Only a verified
  figure excludes on economics
- **Sponsor-owned is always PASS.** The screen runs on every row, including the
  obviously founder-owned ones, because companies keep the family-owned language
  for years after a sale. The sample run found 37 of them
- **Signals are quoted verbatim or they do not exist.** "We are exploring options
  for the next phase" is a quote. "The founder is looking to sell" is a
  fabrication, and it is the kind that ends up in a letter to the founder
- **Nothing about a person's private life**, in the research, in the notes, or in
  an opener. Age, health, family, wealth: out
- **No guessed email addresses.** Not once, not for the best row on the list.
  `not-found` is a real answer
- **The volume that made the research work would ruin the outreach.** Twenty
  first touches per sender per week, five companies per metro per week, one
  contact per company, and a batch overlap check that rewrites two letters if they
  share more than 40% of their sentences
- **The audit runs every time and gets reported whether or not it is clean** —
  including thirty random re-checks of the cheap drops, which is where the real
  false negatives live
- **Nothing is deleted.** A PASS carries the rule that excluded it, so the same
  company is not rediscovered and re-researched in six months

---

## What this deliberately does not do

**It does not send anything.** There is no send step, no integration, no
automation hook. It drafts, checks, and stages a queue with dates on it. A human
reads it and sends it by hand.

That is a design decision, not a missing feature. An automatic send loop attached
to a language model, a list of two thousand named owners and a regulated activity
is a bad idea in every jurisdiction, and the first time it goes wrong it goes
wrong at volume.

It also will not research on behalf of a fee-based intermediary. If you earn
transaction-based compensation for arranging a purchase somebody else makes, the
intake skill stops and tells you to talk to securities counsel. That gate has no
override.

---

## Repo contents

- [`SETUP.md`](./SETUP.md) — the full setup guide, start here
- [`commands/`](./commands/) — `/originate` and `/run-status`
- [`skills/`](./skills/) — the eleven skills Claude Code reads
- [`agents/`](./agents/) — the five subagents
- [`references/`](./references/) — the run protocol, the ranking rubric, the
  evidence and estimation rules, the outreach rules, compliance, pipeline stages,
  and where the companies actually are
- [`templates/`](./templates/) — the mandate template, a fully worked example
  mandate, and the five CSVs the run writes to
- [`samples/`](./samples/) — a complete finished run, so you can see the output
  before you install

---

## A word on the research

Everything here runs on public sources: registers, licence rosters, filings,
procurement awards, trade press, association directories, and what companies
publish about themselves.

Nothing in this package scrapes behind a login that forbids it, pretends to be
somebody it is not, guesses an email address, or records anything about an
owner's private life. If a fact is only obtainable by deception, the fact is
`Not found`.

By the end of a run you hold a file naming real people and their businesses. The
package treats that as what it is: personal data, collected for the rows you will
actually contact, kept out of version control, and deleted on request. None of
which is legal advice, and
[`references/compliance.md`](./references/compliance.md) says so more carefully.

---

Free and MIT licensed. Built by [Corebits](https://corebits.io).
