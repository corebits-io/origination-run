# What a Finished Run Looks Like

> **Every company, person, quote, URL and number on this page is invented.** This
> is a shape, not data. It exists so you know exactly what you are getting before
> you install anything.
>
> The run is Kestrel Lane Capital against the worked mandate in
> `templates/MANDATE-example.md`: commercial electrical contracting and building
> systems integration, four Southeast states, $8-60M revenue, founder or family
> owned, one platform and three add-ons wanted this year.
>
> It took about fourteen hours of working time over six working days, and roughly
> sixty percent of that was depth 2.

---

## The funnel, which is the actual product

```
ORIGINATION RUN — SE-ELEC-Q4                    started 2026-10-02
Mandate: Kestrel Lane Capital                   finished 2026-10-11
Rubric:  rubric-SE-ELEC-Q4-2026-10-09.md        approved before ranking

depth 0   enumerated            2,417 pulled → 2,140 after dedupe
depth 1   desk screened         2,140   →    792 carried    1,348 dropped
depth 2   ownership + size        792   →    524 carried      268 dropped
depth 3   signals                 524   →    196 with a dated signal
depth 4   ranked                2,140   →    PRIORITY 31  WATCH 494  PASS 1,615
depth 5   routed                   31   →     28 live, 26 routed, 3 of them warm
depth 6   drafted                  23   →     21 messages, 2 refused
depth 7   queued                   21   →      0 sent

Caps     enumeration 2,000 | depth 2 cap 800 (not reached)
         20 first touches per sender per week | 5 per metro per week
```

Read it right to left. Twenty-one letters worth writing and three introductions
worth making, and it took two thousand one hundred and forty companies to find
them. Two thousand enumerated is a coverage claim. Two thousand contacted would
have been a mistake.

---

## Depth 0 — where the two thousand came from

```
Georgia licence roster          complete pull 1,840 → 612 in scope
Tennessee licence roster        complete pull       → 441
Alabama licence roster          CAPPED at 500 per query. Pulled per county.
                                2 counties still returned exactly 500 and are
                                incomplete. ~180 rows estimated missing  ← gap
South Carolina roster           complete pull       → 305
2 state registries              status + officers on 1,790 rows, 41 new
3 association directories       488 members, 206 in scope, 37 new
5 installer locators            264 in geography, 61 new
NECA exhibitor 2024-26          212 contractors, 74 in geography, 18 new
2 procurement award portals     award history on 341 rows, 9 new
User database export 2025       190 rows, 171 already present, 19 new

Enumerated                      2,417
After dedupe                    2,140   (277 merges: 183 name variants,
                                         61 branches, 33 holding/operating)
Cross-found in 2+ sources       1,027   (48%)
Single source only              1,113   ← 94 roster-only, the proprietary end

domain present                  1,604 / 2,140   536 have no website at all
employee_count present            912 / 2,140
```

**Bias statement, as written at the gate.** This list leans toward licensed
operators, which is the segment definition, and toward association members and
exhibitors, which over-represents larger and more outward-facing firms. The
forty-year-old company that joined nothing and advertises nowhere appears only
via the rosters, which is why the rosters went first and why the Alabama cap is
the most important line in the log.

The bought list is the quiet lesson here. A hundred and ninety rows, a hundred
and seventy-one of which the licence rosters already had.

---

## Depth 1 — the cheap pass, and what it refused to do

```
Carried forward         792   (37%)   inside the 30-45% band

Dropped               1,348
  segment               611   residential-led 402, wholesale 94,
                              staffing 61, out-of-scope specialty 54
  licence               389   none found 214, inactive 98, under 10 years 77
  geography             218   outside the four states
  defunct                97   dissolved, expired, no operations
  public                 24   listed, or subsidiary of a listed parent
  suppression             9   2 opt-outs, 4 Calder subcontractors,
                              3 cold-only relationships

Arguable drops           17   recorded by name for the audit. 11 are
                              licence-address-is-a-registered-agent cases

NOT dropped at this depth
  no website            198 of the 792 carried
  no headcount          402 of the 792 carried

Free enrichment on the carried rows
  licence issue date    792 / 792
  entity status         764 / 792
  verified award floor  188 / 792   ← a real revenue floor, before a single
                                      estimate was made
```

Those 198 carried rows with no website are not a data quality problem. They are
the reason this list is worth more than a database export.

---

## Depth 2 — the expensive pass, and the line that pays for the run

```
792 researched in 32 batches. Carried forward 524.

Dropped                 268
  sponsor-owned         161   ← 37 of these still describe themselves as
                                family owned or independent on their own site
  verified outside box   61   filed accounts or disclosed award totals only
  corporate subsidiary   28
  public parent           6
  defunct discovered     12

Ownership of the 524
  founder-owned         243   Tier 1: 198   Tier 2: 45
  family-owned          171   Tier 1: 121   Tier 2: 50
  management/partner     61
  ESOP                   14   capped at WATCH per mandate section 7
  Not found              35   capped at WATCH, never dropped

Sponsor rate            161 of 792 = 20%. The map predicted 20-25%.

Size of the 524
  verified               58   estimate high 149   medium 221   low 71
  Not found              25
  Outside the box on an estimate   44   ← all WATCH, none dropped
  Inside on a verified floor       31   ← the free award history did this

Role
  platform               87
  add-on                298   Calder 171, Pembury 127, every one named
  Not found             139   capped at WATCH
```

**The thirty-seven.** Companies a sponsor already owns that still say "family
owned since 1981" on their own about page. Each one is a letter that does not get
written to an owner who sold three years ago, and that letter is the kind that
gets forwarded to the new owner with a comment attached.

---

## Depth 3 — signals

```
524 researched. 196 with a dated signal (37%). 328 Not found (63%).

By family     leadership 61   financing 48   growth 59   hiring 28
By strength   high 41   medium 83   low 72

Rejected during research
  age-only inference     34   recorded as Not found
  trade vacancies only   57   noise per mandate section 9
  undated page           22   Tier 4
  private-life material   3   out of scope, not recorded anywhere

Notable: 14 of the 41 high signals are officer changes read straight off
the register. Free, Tier 1, dated, and nobody else reads them.
```

Sixty-three percent with no signal is the honest result. A list where every row
has a signal has invented some.

---

## Depth 4 — the ranked list

```
Before the audit     PRIORITY 34   WATCH 490   PASS 1,616
After the audit      PRIORITY 31   WATCH 494   PASS 1,615

PRIORITY as a share of researched rows    5.9%   inside the 4-8% band
```

### Six of the thirty-one PRIORITY rows

| # | Company | HQ | Rev est | EBITDA est | Owner | Role | Signal |
|---|---|---|---|---|---|---|---|
| 1 | Northline Electric | Chattanooga, TN | $19-24M | $1.6-2.7M | Founder | platform | Owner, 63, said neither child went into the trade (trade press, 2026-06-14) |
| 2 | Hollis Electric | Macon, GA | $11-14M | $0.9-1.6M | Family, 2nd gen | add-on → Calder | None. Licence held since 1986, same officers since 1994 |
| 3 | Brightwell Electric | Huntsville, AL | $14-17M | $1.2-2.0M | Founder | add-on → Calder | First controller hired (own careers page, 2026-09-02) |
| 4 | Sandoval Power Systems | Columbia, SC | $22-27M | $1.9-3.1M | Family | platform | Service now half of revenue, no successor named (trade press, 2026-06-02) |
| 5 | Pennington Controls | Knoxville, TN | $9-11M | $0.8-1.3M | Management | add-on → Pembury | Two of four shareholders left the register (filing, 2026-03-11) |
| 6 | Caldbeck Electric | Birmingham, AL | $12-15M | $1.0-1.7M | Founder | add-on → Pembury | New $7.5M facility, new lender of record (UCC, 2026-05-20) |

Row 2 has no signal at all and is still PRIORITY, because the mandate ranks
licence tenure and clean second-generation ownership highly and the rubric lets
a Tier 1 ownership picture carry a row. Row 6 is the one the audit later checks
twice, because a new lender can mean a sponsor is already circling.

### One row, fully expanded

```
company              Northline Electric
domain               northlineelectric.example
hq_location          Chattanooga, TN
sector / segment     Commercial electrical / contract-recurring service

ownership_type       founder-owned
ownership_evidence   Tier 1 — Tennessee SOS filings list the same sole officer
                     since 1991 incorporation, no share transfers on record.
                     Cross-checked against about page dated 2026-02
evidence_tier        1
sponsor_screen       clear — screened against the 4 sponsor platforms named in
                     the map, no trade press 36mo, no UCC filings naming a
                     fund entity, register resolves to one named individual

year_founded         1991
employee_count       118   (LinkedIn 2026-09, cross-checked against 114
                     stated in a 2026-06 trade piece)

est_revenue          $19-24M
                     (estimate: 118 staff x $165-210k sector-typical revenue
                     per head, NECA 2025 southeast survey; headcount firm,
                     two independent sources. Cross-check: $16.4M floor
                     implied by disclosed 2024-25 municipal and state awards)
est_ebitda           $1.6-2.7M
                     (estimate: 8-11% sector-typical margin from map segment
                     economics applied to the revenue range; both unverified)
financial_confidence high   (two methods agree within 14%)

fit_role             platform
fit_role_reason      Upper half of the size box. Named general manager and
                     named service manager, neither a family member. Service
                     and maintenance stated at 48% of revenue in the 2026-06
                     piece. No Kestrel platform within 110 miles

verdict              PRIORITY
fit_reason           Clean on every exclusion; founder-owned at Tier 1;
                     estimate midpoint inside the box; platform role decided
                     with second-tier management evidenced; all four testable
                     must-haves met; high-strength leadership signal four
                     months old, inside the 24-month window

signal               "I'm 63. My daughter is a physician and my son went into
                     software. At some point this business needs an owner who
                     isn't me."
signal_family        leadership
signal_source        https://example-tradepress.test/northline-35-years
evidence_date        2026-06-14
signal_strength      high   (Tier 2, the owner on the record, 4 months old,
                     about a decision rather than an atmosphere)

owner_name           M. Vance
owner_title          President and sole officer
owner_evidence       Tier 1 — named as sole officer on the TN SOS filing 1991
                     to present; same name on the master licence record
contact_route        published email, on their own contact page
route_status         published

source               Tennessee electrical contractor licence roster (complete
                     pull 2026-10-02); cross-found in IEC member directory and
                     2025 + 2026 NECA exhibitor lists
batch                D2-04 / D6-01

NOT KNOWN            Margin is a sector benchmark, not theirs. No accounts
                     filed. Customer concentration unknown. Whether the named
                     GM would stay post-transaction is unknown and material
                     to the platform case. The 48% service figure is the
                     owner's own statement, not verified.
```

The `NOT KNOWN` block is on every PRIORITY row. It is the difference between a
brief and a sales pitch to yourself.

---

## Why rows did not make PRIORITY

```
WATCH — 494
  fits, no signal found                268
  fits, signal strength low             72
  estimate outside the size box         44
  ownership Not found                   35
  fits, signal below the recency window 31
  size Not found                        25
  role not decidable                    19

PASS — 1,615
  segment             611
  licence             389
  geography           216
  sponsor-owned       162   ← 37 still market themselves as family owned
  defunct             109
  economics            61   verified figures only
  corporate            28
  public               24
  suppression           9
  process               6   retained banker, per mandate section 8
```

Two hundred and sixty-eight rows fit the mandate and have no trigger. They are
not failures, they are next quarter's pipeline, and a signals re-read is the
cheapest thing this system can do.

---

## The audit

```
AUDIT — 2026-10-10

1. PRIORITY signals verified at source        10 of 31 checked
     confirmed at the URL                      9
     page no longer says it                    1  ← Marchmont Electric.
                                                  Downgraded to Not found,
                                                  row to WATCH.

2. Depth 1 drops re-checked                   30 random rows
     correctly dropped                        28
     wrong                                     2  ← Dunbar Systems: licence
                                                  address is a registered
                                                  agent, operations are in
                                                  Chattanooga. Restored.
                                                  Trenholm Building Systems:
                                                  dropped on segment, is a
                                                  licensed integrator inside
                                                  the EDGE block. Restored.

3. Researched PASS re-checked                 20 random rows
     correctly excluded                       19
     wrong                                     1  ← Verity Power, excluded on
                                                  a low-confidence $7.4M
                                                  estimate against an $8M
                                                  floor. Hard rule 2 says
                                                  WATCH. Corrected.

4. Keep pile re-screened for sponsors         525 rows
     new sponsor hits                          2  ← Calderwood Systems and
                                                  Pike Electrical, both
                                                  announced after our capture.
                                                  Both to PASS.

5. Distribution                               inside band

Net: 6 corrections, every one in the direction the rubric requires.
```

An audit that catches nothing on a two-thousand-row list has usually not run.
The two restored depth 1 drops are the reason part 2 exists: both were deleted
for free, in the cheapest step, and nothing downstream would ever have looked at
them again.

---

## Depth 5 — routes

```
31 PRIORITY rows in scope

Flagged out during routing    3
  Severn Electrical               sold since capture, announced 2026-10-06
  Kessler Electric                owner died 2026-04, register confirms
  Trevose Electrical              retained banker on a live process. Mandate
                                  section 8: do not go around. Letter to the
                                  banker offered instead

Live rows                    28   owner identified 26, no owner 2

Routes       warm-path         3   operating partner knows all three
             published email  12
             verified email    5
             form-or-phone     6   letters
             not-found         2
             guessed           0   ← by design. Nothing is ever guessed

Draftable                    26   3 introductions + 17 email + 6 letters
```

---

## Depth 6 — two of the twenty-one drafts, in full

### Email, to a row with a quoted signal

> **Subject:** Northline Electric
>
> Mr Vance, my name is Ray Okoye. I ran a 200-person electrical contractor in
> Birmingham for eleven years and sold it in 2019. I now buy electrical and
> building systems businesses in the Southeast with my own fund, and we hold
> them. We are not brokers.
>
> You told the trade press in June that service contracts are now about half the
> work and that neither of your children went into the trade. That is the part I
> would want to talk about. Not the numbers.
>
> Would you be open to a short call in the next few weeks, whenever suits you?
>
> If the timing is wrong, no reply is needed and I will not keep writing.
>
> Ray Okoye
> Kestrel Lane
> 1 Example Plaza, Suite 400, Atlanta, GA 30309

```
104 words. Sender chosen because the licence sentence is the strongest true
thing available to this mandate. Personalization from signal + signal_source,
re-confirmed at the URL on 2026-10-11.
```

### Letter, to a row with no signal at all

> Dear Mr Hollis,
>
> My name is Ray Okoye. I ran an electrical contracting business in Birmingham
> for eleven years, about the size yours is now, and sold it in 2019. I now buy
> and hold electrical and building systems companies in the Southeast with my own
> fund. We are not brokers and we are not raising money.
>
> I am writing because of what your licence record shows. Hollis Electric has
> held the same master licence since 1986 and the same two officers since 1994,
> which in this trade usually means a company that has been run carefully and
> has never had to be sold.
>
> I am not asking you to sell anything. I am asking whether you would spend half
> an hour on the phone with somebody who has done the job, so that if you ever
> do think about what happens next, you already know one buyer who is not a
> broker and not a fund with a clock on it.
>
> If you would rather not, no reply is needed and I will not write again.
>
> Yours sincerely,
> Ray Okoye

```
210 words. No signal existed on this row. The specificity came from a free
Tier 1 licence record instead, which is what depth 1 collected at no cost.
```

### And the two refusals

```
Avondale Electrical    The signal page had been rewritten since capture and
                       the quote could not be re-confirmed. No letter until
                       there is a signal that still exists.

Caldbeck Electric      The only personalization available was the owner's age,
                       from a press photo caption. Out of scope. Research the
                       licence history instead and come back.

Overlap check          highest pair 31%, two letters that both lean on licence
                       tenure. Under the 40% threshold, both kept.
```

---

## Depth 7 — the queue

```
21 approved drafts. 0 sent.

Week of 2026-10-13     14 first touches
  R. Okoye   10   6 email, 4 letters
             Atlanta 3, Birmingham 2, Chattanooga 2, Knoxville 2, Columbia 1
  J. Hallam   4   4 email
             Atlanta 2, Nashville 2
             → Atlanta is at 5 for the week, exactly on the cap. Nothing else
               from Atlanta goes out before the 20th

Week of 2026-10-20      7 first touches, plus 14 follow-ups scheduled
Week of 2026-10-27     21 follow-ups scheduled

Every follow-up conditional on no reply. A reply cancels the rest of that
company's sequence immediately, whatever it says.

Introductions, not queued    3   R. Okoye to make personally
Held for signal expiry       1   Brightwell, hiring signal expires 2026-11-02,
                                 moved into week one
Suppression re-check         passed, 0 matches, 2 near-matches cleared by hand
```

---

## What you actually do with it

Twenty-one letters to write, three introductions to make, and a pipeline that
starts the day the first one goes out. Then the WATCH pile, which is four
hundred and ninety-four companies that fit the mandate and are waiting for a
trigger, and which costs almost nothing to re-read next quarter.

And one line nobody asked for: thirty-seven companies in this segment are
already sponsor-owned while still calling themselves family owned. That is the
kind of thing you only find out by doing the whole population rather than the
part somebody sold you.
