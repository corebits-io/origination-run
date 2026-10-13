# Evidence Rules — Tiers, Dates, Quotes, and What `Not found` Means

Every fact this run writes gets used by a rubric that cannot tell the difference
between a sourced fact and a confident guess. So the grammar below is not
bookkeeping. It is the thing that stops a 2,000-row list from becoming 2,000
plausible sentences.

One rule above all the others:

> **`Not found` is a real answer, it is the most common one, and it is never a
> failed test.**

---

## 1. Evidence tiers

The same four tiers apply to ownership, to size, and to signals. Record the tier
in `evidence_tier`.

| Tier | What it is | Usable? |
|---|---|---|
| **1** | A filing, register entry, licence record, court record, UCC or security filing, or an official award notice | Yes, strongest |
| **2** | The company or the person saying it on the record: a press release, an interview, a trade press quote, their own website, their own post | Yes |
| **3** | A dated third-party report that names its own source | Yes, with the caveat recorded in `notes` |
| **4** | An aggregator field, a database entry, an undated page, a "according to sources" line | **No.** A pointer to go and find Tier 1-3, never evidence on its own |

**A company calling itself family owned is Tier 3 at best**, and often Tier 4.
Companies keep that language on the about page for years after a sale. Check the
register.

A fact resting on Tier 4 alone is `Not found`. Not `low`. `Not found`.

---

## 2. Dates

Every piece of evidence carries a date in `YYYY-MM-DD`. Where only a month is
published, use the first of the month and say so in `notes`.

**Undated evidence is Tier 4.** An ownership page with no date, a news item with
no date, a profile with no date: a pointer, not a fact.

The date is what makes the row re-checkable in March, and it is what the
expiry rules below run on.

---

## 3. Quoting

**Quote the words. Never paraphrase inside quotation marks.**

If the source says *"we are exploring options for the next phase"*, that is the
quote. Writing *"the founder is looking to sell"* is a fabrication, and it is
the specific kind that ends up in a letter to the founder.

- Every quote carries a working URL to the page the words are on. Not a domain,
  not a search result
- If the page has changed since capture, the signal is `Not found` and the row
  moves down. The audit checks exactly this and it finds something most runs
- Translate only where necessary, mark it as translated, and keep the original

A quote is the only form of personalization this package will put in front of an
owner. That is why the standard is this high.

---

## 4. Ownership evidence

`ownership_type` is one of: `founder-owned`, `family-owned`, `management-owned`,
`partner-owned`, `ESOP`, `sponsor-owned`, `corporate-subsidiary`, `public`, or
`Not found`.

What counts as establishing it:

| Type | Tier 1 evidence looks like |
|---|---|
| Founder-owned | Register shows the same named officer or shareholder since formation, no share transfers recorded |
| Family-owned | Two or more shareholders or officers sharing a surname across generations, or a documented transfer to a family member |
| Management-owned | A shareholder register of named individuals who hold operating titles |
| Partner-owned | A partnership filing, or a register of named partners |
| ESOP | A trust filing or plan disclosure |
| Sponsor-owned | A fund entity in the register or on the share allocation, a transaction announcement, or a UCC filing naming a sponsor vehicle |
| Corporate subsidiary | The register showing a corporate parent |
| Public | A listing |

`Not found` ownership is a legitimate and common outcome. It caps a row at
WATCH. It never drops one, and it is never filled in with the most likely
answer.

---

## 5. The four signal families

Fit says whether a company belongs in the mandate. A signal says why this
quarter. They are kept separate on purpose, and PRIORITY requires both.

### Leadership and succession

The people who can sell are changing.

- An owner stating age, succession, retirement, or that there is no next
  generation
- A title change: founder to chairman, a non-family CEO or MD appointed
- A death, illness or departure in the ownership group
- A long-tenured second generation taking over, or publicly declining to
- A partner or shareholder exiting the register

*Why it matters:* this family produces more actual transactions than the other
three put together, and it is the one most often mis-read. A quote beats an
inference every single time.

### Financing

Money arriving, or being restructured.

- A new facility, a refinancing, or a new lender of record
- A minority or growth investment
- A sale-leaseback, or property released from the business
- New UCC filings or equivalent security registrations
- A grant, bond or public financing package

*Why it matters:* financing events put a valuation conversation on the table and
usually come with a clock. They also tell you whether a sponsor is already
circling.

### Growth

The company is getting bigger in a way that changes the conversation.

- A new site, depot, plant, branch or region
- Capacity added: fleet, lines, bays, beds, machines
- A named large contract or framework award
- Headcount up materially against a stated earlier number
- A new service line or licence category

*Why it matters:* growth outruns the owner's systems. It is often the moment a
founder starts thinking about whether the next stage is theirs to fund.

### Hiring

Who a company hires tells you what it is about to do.

- A first CFO, finance director or controller
- A first COO, general manager or operations director
- A corporate development, integration or M&A role
- Senior roles posted in a new geography

*Why it matters:* a first professional finance hire at a founder-owned company
is one of the strongest pre-process signals there is. Somebody has decided the
numbers need to be presentable.

*What it is not:* a volume of trade vacancies. These companies are always hiring
tradespeople. That is an industry condition, not a signal.

---

## 6. Strength

| Strength | Test |
|---|---|
| **high** | Tier 1 or 2, inside the window, and about a decision rather than an atmosphere. Quotable to the owner without embarrassment |
| **medium** | Tier 1-3, inside the window, real but indirect. A first controller hire with no stated reason sits here |
| **low** | Inside the window but thin: one job posting, a small headcount move, a vague quote |
| `Not found` | Nothing sourced and dated. The honest and common answer |

---

## 7. Recency windows

Age a signal against its own family, not a single global cutoff.

| Family | Window | After that |
|---|---|---|
| Hiring | 90 days | Expired. A six-month-old job posting is not a signal, it is a vacancy that was probably filled |
| Financing | 12 months | Downgrade one level |
| Growth | 12 months | Downgrade one level |
| Leadership | 24 months | Still usable. Succession moves slowly, and an owner who said two years ago that nobody in the family wanted it probably still means it |

A signal with no date is `Not found`.

---

## 8. Hard rules

**1. One signal per row, the best one.** Extras go in `notes`. A row with five
weak signals is still a weak row, and stacking them is how a WATCH becomes a
PRIORITY it has not earned.

**2. No signal is the normal answer.** Expect `Not found` on most of any
honestly researched list. The sample run found a dated signal on 196 of 524
researched rows. A list where every row has a signal has invented some.

**3. Never infer succession from age alone.** A founder being sixty-four is not
a signal. A founder saying there is nobody in the family to take it on is.

**4. Never infer from a person's private life.** Health, family, finances,
divorce, estate records: out of scope even where technically public. Succession
evidence comes from professional sources or it does not exist.

**5. A signal never changes the fit verdict.** It changes timing only. A loud
signal cannot promote an out-of-mandate company and a missing signal cannot drop
an in-mandate one.

**6. Public sources only, under your real identity.**

**7. Evidence gets re-checked before it is used in a message.** The audit
verifies PRIORITY signals at their source URL, and the drafting step refuses to
quote a signal whose page no longer says it. This is the one error class in the
whole package that reaches an owner, so it is checked twice.
