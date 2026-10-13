# The Origination Run — Setup Guide

> A free giveaway. Eleven skills, five agents and one command that take an
> acquisition mandate and run origination end to end: two thousand companies
> enumerated, screened on free facts, researched where it is worth it, ranked
> against a rubric you approve first, then routed, written and staged into a
> queue a human sends by hand.
>
> Follow this guide end to end and you will have it running on your own machine
> in about twenty minutes. No database, no API keys, no signups.

---

## What this actually is

**One command.** You fill in one file and type `/originate`. It runs seven
phases, stops for your approval at each boundary, and resumes where it stopped if
you close the laptop.

**The eleven skills** are what actually runs. You can call any of them directly.

| Skill | What it does |
|---|---|
| `origination-intake` | Checks your mandate, runs the principal-buyer gate, rewrites untestable must-haves, sets the enumeration target and the research caps from the conversations you can hold |
| `segment-mapping` | Maps the segment: boundary, fragmentation, segment economics, the typical owner, who is consolidating, where the companies are findable. Ends with a verdict |
| `population-sourcing` | Enumerates the whole population, one source at a time, with a ledger, honest cap reporting and a coverage log |
| `desk-screening` | The free pass over every row. Drops on facts that are false, never on facts that are absent |
| `ownership-and-size` | Ownership, the sponsor screen, labeled revenue and EBITDA, the platform or add-on call |
| `signal-detection` | Leadership, financing, growth and hiring signals, quoted, sourced, dated, aged |
| `fit-ranking` | Builds the rubric, gets it approved, ranks every row identically, audits itself |
| `owner-contact-routing` | The person who can sell, and an honest route. Never a guessed address |
| `owner-outreach-drafting` | First touch plus two follow-ups, short and plain, specific from the row |
| `outreach-queue` | Capacity, per-metro caps, suppression re-check, send-after dates |
| `pipeline-operations` | Replies logged, overdue first, the weekly read that names the constraint |

**The five agents** are the team. You talk to them like people.

| Agent | Owns |
|---|---|
| `origination-sourcer` | mandate, map, population, screen |
| `target-analyst` | ownership, sponsor screen, size, role, signals |
| `fit-ranker` | rubric, ranking, audit |
| `outreach-builder` | routes, drafts, queue. Sends nothing |
| `pipeline-keeper` | the pipeline, from the first touch onward |

Everything runs through conversation. Your data stays in local files on your
machine.

**Want to see the output first?** Read
[`samples/sample-run.md`](./samples/sample-run.md). It is a complete finished
run, invented end to end, and it will take you five minutes.

---

## What you need

| Thing | Cost | Required? |
|---|---|---|
| [Claude Code](https://www.anthropic.com/claude-code) | Claude subscription or API usage | **Yes** |
| A folder on your computer | Free | **Yes** |
| A written mandate | Free, and fifteen minutes | **Yes** |
| Everything else | — | No |

That is the whole list. There is deliberately no database, no MCP server, no
sending tool and no API key to configure.

---

# Part 1 — Install Claude Code

Claude Code is Anthropic's official terminal app for Claude. It runs everything
here.

Follow the official instructions at
**[anthropic.com/claude-code](https://www.anthropic.com/claude-code)**. macOS,
Windows and Linux are all supported.

Then check it works:

```bash
claude
```

You should get a welcome screen and a prompt. Type `/login` and authenticate if
you have not already. Exit with Ctrl+C twice.

---

# Part 2 — Install the package

Two steps: clone the repo, then copy the pieces where Claude Code looks for them.

### macOS / Linux

```bash
git clone https://github.com/corebits-io/origination-run.git
mkdir -p ~/.claude/skills ~/.claude/agents ~/.claude/commands
cp -r origination-run/skills/* ~/.claude/skills/
cp -r origination-run/agents/* ~/.claude/agents/
cp -r origination-run/commands/* ~/.claude/commands/
```

### Windows (PowerShell)

```powershell
git clone https://github.com/corebits-io/origination-run.git
New-Item -ItemType Directory -Force "$HOME\.claude\skills", "$HOME\.claude\agents", "$HOME\.claude\commands"
Copy-Item -Recurse -Force "origination-run\skills\*" "$HOME\.claude\skills\"
Copy-Item -Recurse -Force "origination-run\agents\*" "$HOME\.claude\agents\"
Copy-Item -Recurse -Force "origination-run\commands\*" "$HOME\.claude\commands\"
```

### Keep the cloned folder

Do not delete it. The skills read the `references/` files from it, and you will
copy the `templates/` in a moment.

### Verify

Start Claude Code and run:

```
/skills
```

You should see all eleven: `origination-intake`, `segment-mapping`,
`population-sourcing`, `desk-screening`, `ownership-and-size`,
`signal-detection`, `fit-ranking`, `owner-contact-routing`,
`owner-outreach-drafting`, `outreach-queue`, `pipeline-operations`.

Then:

```
/agents
```

You should see `origination-sourcer`, `target-analyst`, `fit-ranker`,
`outreach-builder`, `pipeline-keeper`.

If either list is short, see Troubleshooting below.

---

# Part 3 — Set up your workspace

This is where your actual data lives. Keep it separate from the cloned repo.

```bash
mkdir -p ~/my-run
cd ~/my-run
cp ~/origination-run/templates/MANDATE.md .
cp ~/origination-run/templates/*.csv .
mkdir run
```

Windows:

```powershell
New-Item -ItemType Directory -Force "$HOME\my-run\run"
Set-Location "$HOME\my-run"
Copy-Item "$HOME\origination-run\templates\MANDATE.md" .
Copy-Item "$HOME\origination-run\templates\*.csv" .
```

You should now have `MANDATE.md`, `targets.csv`, `outreach.csv`, `pipeline.csv`,
`suppression.csv`, `source-ledger.csv`, and an empty `run/` folder for the state
file and the log.

> **Never put this folder in a public repository.** It will contain company
> names, owner names, contact details, drafted letters and the reasoning behind
> a live acquisition thesis. Owner names and contact details are personal data
> and are regulated in most jurisdictions.

Delete the example row from each CSV before you start. They are there to show you
what a correctly filled row looks like.

---

# Part 4 — Fill out your mandate

**This is the most important step in the whole guide.** Do not skip it and do not
rush it.

`MANDATE.md` is the file every skill reads. It is where the system learns what you
buy, what size, where, which ownership types are actionable, what you will never
touch, which platforms an add-on could attach to, which timing signals matter,
how much research you can afford, who may sign a letter, and what each of them
may truthfully claim.

Open it and fill it out honestly. Fifteen minutes here decides whether the run
returns a dozen real conversations or two thousand plausible-looking rows.

**Three rules while filling it in:**

1. If something does not apply, write `N/A`
2. If you do not know yet, write `TBD`. The system will ask rather than invent
3. **Answer section 1 properly.** If you are a fee-based intermediary rather than
   a principal buyer, the intake skill will stop and tell you to talk to counsel
   about broker-dealer registration before researching anybody. That gate is
   deliberate and has no override

**Four sections people skip, and should not:**

- **Section 2, the named platforms.** If you want add-ons, name the existing
  platforms they would attach to, with the geography and the capability gap for
  each. Without them, "add-on" is a label with no test behind it and every add-on
  verdict on your list is a guess
- **Section 6, the must-haves.** Three to five real requirements beats twelve
  aspirations, and make them testable. "Strong management team" is not a test. "A
  named second-tier manager who is not the owner and not a family member" is.
  Intake will push back on the ones that are not, but it is faster if you do it
  first
- **Section 10, the volume numbers.** Specifically: how many owner conversations
  you can actually hold at once. That number is the constraint the whole run is
  sized from, and almost nobody writes it down
- **Section 11, the senders.** One row per person whose name will appear on a
  letter, and the true sentence about each of them that an owner would care
  about. No message can be drafted until this exists, because there would be
  nobody for it to be true about

**Stuck?** Read [`templates/MANDATE-example.md`](./templates/MANDATE-example.md).
It is a complete worked mandate for a fictional fund, and it is the fastest way
to see the level of specificity that works.

Or do it conversationally. Start Claude Code in the folder and say:

```
help me fill out my mandate
```

Sections 4, 9 and 10 will improve after your first run. That is expected. Come
back and update them.

### Load your suppression list now

Put every name you already know into `suppression.csv` before the run starts:
anybody who has asked not to be contacted, portfolio conflicts, your platforms'
subcontractors, companies you have already worked, and the relationships you want
routed as a warm introduction rather than a cold letter (scope `cold-only`).

The run checks that file at depth 1, again at routing, and a third time before
anything is queued.

---

# Part 5 — Your first run

Start Claude Code from your workspace folder:

```bash
cd ~/my-run
claude
```

Then:

```
/originate
```

That runs the whole chain. Here is what happens at each gate, so you know what
you are approving.

### 1. Intake

It reads your mandate, runs the principal-buyer gate, challenges anything that
cannot be tested, and does the funnel arithmetic **backwards from the number of
conversations you can hold**. Expect it to rewrite a must-have or two, to tell
you if you have too many, and to propose an enumeration target rather than
accept one.

It also tells you what the run will cost in hours before you spend them.

**You approve:** the run plan and the caps.

### 2. Segment map

It maps the segment your mandate implies before enumerating a single company.
Fragmentation, the typical owner, who is already consolidating, where these
companies are findable, and — the part that matters most — the segment economics:
revenue per head and typical EBITDA margin, sourced and dated. Every revenue
estimate later in the run rests on those two numbers.

It ends with a verdict, and the verdict is sometimes **do not source this
segment**: too few operators inside your size box, mostly sponsor-owned already,
no public ownership information, or no source that enumerates the population.
That verdict is worth more than a list.

**You approve:** the map and the verdict.

### 3. Sourcing, then the screen

It enumerates the population from the sources the map named, one source at a
time, Tier 1 first. Licence rosters and registries before association
directories, and aggregators used only as a pointer, never as a row. Every row
carries a source string specific enough to re-run, and every pull gets a ledger
entry saying whether it capped.

Then the free screen runs over every row: suppression, not-a-company, geography,
segment, licence, public. Six checks, each binary, each recorded.

**You approve:** the counts, the coverage log, fifteen sample rows — then the
drop counts, the carry rate, and ten carries and ten drops in full.

> Expect a chunk of rows with no website at all, and expect them to carry
> forward. A thin website is not a negative signal in this system. The companies
> with no marketing budget are the ones no banker has called, and deleting them
> in the cheapest step is the most expensive mistake available here.

### 4. Ownership, size and signals

The expensive part, and about sixty percent of the run. Ownership first, from
filings and registers, with the four-part sponsor screen on every row. Then
revenue and EBITDA ranges with the basis attached in the same cell. Then the
platform or add-on call against your named platforms. Then the four signal
families.

Runs in batches of 20 to 30 with a report between each, and stops at your depth 2
cap rather than quietly spending another month of budget.

**You approve:** each depth.

> The most valuable line in this step is usually the list of companies a sponsor
> already owns that still describe themselves as family owned on their own
> website. The sample run found thirty-seven. Each one is a letter that does not
> get written to an owner who sold three years ago.

### 5. Ranking

It writes the rubric out in full — every criterion, the mandate section it came
from, the test, the bucket effect — and gets your approval **before ranking a
single row**.

Then it ranks every row in the same fixed order, including the fourteen hundred
dropped at depth 1, and runs the five-part audit: verify PRIORITY signals at
their source URLs, re-check thirty random cheap drops, re-check twenty researched
PASS rows, re-screen the keep pile for sponsors, check the distribution.

**You approve:** the rubric. Then the ranked list and the audit.

### 6. Routes and drafts

For the PRIORITY rows only, it finds the person who can actually sell and an
honest route to them. Warm introduction if one exists, then published or verified
email, then a posted letter, and never a guessed address.

Then it writes a first touch and two follow-ups: under 120 words, no em dashes,
no banned phrases, no valuation implied, personalization taken from the row with
the field named, and every quote re-confirmed at its URL that day. Where there is
nothing specific and true to say, it says so instead of inventing something.

**You approve:** every draft, in full.

### 7. The queue

Sender capacity, five companies per metro per week, the suppression check run a
third time, send-after dates, and follow-ups scheduled conditional on no reply.

**You approve:** the queue. Then you send it yourself, by hand.

### What you end up with

- `targets.csv` — every row with a verdict and the rule that produced it
- `outreach.csv` — the approved queue with dates. Nothing sent
- `pipeline.csv` — seeded, one row per conversation
- `source-ledger.csv` — every pull, with its caps
- `segment-map-[run]-[date].md` and `rubric-[run]-[date].md`
- `run/state.json` and `run/log.md`

For a two-thousand-row run, expect 20 to 40 PRIORITY rows and 15 to 25 letters
worth writing. If you get three hundred PRIORITY rows, the rubric is flattering
you and the system will say so.

---

# Resuming, which you will need

A two-thousand-row run takes days, and it will be interrupted.

Just type `/originate` again. It reads `run/state.json`, **recounts from the
CSV**, tells you where the run actually is, re-presents any gate that was waiting,
redoes any half-finished batch, and carries on. Nothing is researched twice.

To see where things stand without continuing:

```
/run-status
```

That is read-only. It gives you the funnel, what is awaiting your approval, what
is overdue in the pipeline, how much of your research budget is left, and the
cheapest next move.

---

# Working with the agents directly

You do not have to use the command. Talk to the agents.

```
> use origination-sourcer to map and enumerate commercial electrical
  contractors in Georgia and Tennessee against my mandate

> ask target-analyst to run the sponsor screen on everything in targets.csv

> fit-ranker, re-rank the list — I have widened the EBITDA floor to $900k

> outreach-builder, route and draft the top 20 WATCH rows

> pipeline-keeper, what is overdue
```

Two of those are worth calling out.

**Re-ranking is cheap.** If you change the size box or a must-have, `fit-ranker`
re-ranks the existing research. You do not re-source anything.

**You can bring your own list.** If you already have a CSV from a database or a
broker, map your columns to `templates/targets.csv`, then run `target-analyst`
and `fit-ranker` over it. Ranking somebody else's list against your own rubric is
one of the more useful things here, and the audit usually finds something. Every
email address on an imported list is flagged `inferred-DO-NOT-USE` until it is
independently verified.

You can also call a single skill:

```
> run segment-mapping on Midwest commercial refrigeration service
```

---

# The safety rails

These are not configurable, and each one exists because breaking it produces a
specific and expensive failure.

**The principal-buyer gate.** If you earn a fee for arranging a transaction you
are not a party to, the run stops and tells you to talk to securities counsel.
Saying it is fine does not change the answer.

**Nothing writes without showing you first.** Every skill has a hard gate before
it writes.

**Depth is earned.** No row gets expensive research until it has survived the free
screen. That is what makes the volume affordable.

**Drops need a fact that is false, not one that is absent.** No website, no
headcount, no LinkedIn, no founding year, an estimate outside the box: all carry.

**Estimates are labeled, always**, and a labeled estimate outside your size box
makes a row WATCH, never a drop. Only a verified figure excludes on economics.
Excluding a real target because a headcount proxy landed fifteen percent under
your floor is the most expensive routine error in origination, and it happens
silently.

**Sponsor-owned is always PASS**, on every row, including the obviously
founder-owned ones.

**Signals are quoted verbatim or they do not exist.** No paraphrase inside
quotation marks, ever, and every quote is re-verified at its URL before it goes
into a letter. A fabricated quote is the one error in this whole package that
reaches an owner.

**Nothing about a person's private life.** Age, health, family, finances: not in
the research, not in the notes, and never in an opener.

**No guessed email addresses.** Not once. Pattern-guessing at volume ends your
ability to send email at all.

**The volume caps hold.** Twenty first touches per sender per week, five
companies per metro per week, one contact per company, three touches then stop.
Owners in one segment and one metro know each other and talk.

**Nothing sends.** The package stages a queue. You send it.

**The audit runs every time and gets reported whether or not it is clean.**

---

# Troubleshooting

### `/skills` does not show the eleven skills

Check the files landed in the right place. Each skill needs to be its own folder
containing a `SKILL.md`:

```bash
ls ~/.claude/skills/
# desk-screening  fit-ranking  origination-intake  outreach-queue
# owner-contact-routing  owner-outreach-drafting  ownership-and-size
# pipeline-operations  population-sourcing  segment-mapping  signal-detection

ls ~/.claude/skills/fit-ranking/
# SKILL.md
```

If you see a `skills` folder inside `skills`, you copied the folder instead of
its contents. Note the `/*` at the end of the copy command. Restart Claude Code
after copying.

### `/agents` does not show the five agents

```bash
ls ~/.claude/agents/
# fit-ranker.md  origination-sourcer.md  outreach-builder.md
# pipeline-keeper.md  target-analyst.md
```

These are flat `.md` files, not folders.

### `/originate` is not there

```bash
ls ~/.claude/commands/
# originate.md  run-status.md
```

Restart Claude Code. If it still does not appear, run the chain by talking to the
agents instead — see the section above.

### "It cannot find my references files"

The skills read `references/` from the cloned repo, not from your workspace. Tell
it where the clone is:

```
> the references folder is at ~/origination-run/references
```

Or copy the folder into your workspace. Either works.

### It stopped and asked about broker-dealer registration

Because section 1 of your mandate says you earn a fee for arranging transactions
you are not a party to. That is a real regulatory question in the US and the
rules differ by state and by fee structure. Talk to securities counsel. If you
are buying as a principal, correct section 1.

### The screen dropped far too many rows

Check three things in order. Is your geography marked **hard** when it is really
a preference? Does your mandate require a licence the segment does not actually
use? Did sourcing pull from the wrong licence classes? A carry rate under 15% is
a population problem, not a screen problem, and the run should have stopped and
said so.

### The screen dropped a company I know is good

Tell it which one. Then look at `screen_reason`. The three recurring false
positives are a registered-agent address read as out-of-geography, a company
whose one-page website undersells what it does, and a licence renewed under a new
entity name. The audit hunts exactly these, which is why it re-checks thirty
random drops every run.

### It keeps saying `Not found` instead of giving me data

Working as intended. A blank is honest; an invented ownership type or a made-up
revenue figure silently corrupts every verdict downstream.

If it is `Not found` on almost everything, the usual cause is that the segment map
came back without economics. Without a sourced revenue-per-head range there is no
honest way to size anything, and the map will have said so.

### The ranking gave me almost no PRIORITY rows

Four usual causes, in order of likelihood:

1. **The signals pass has not run.** PRIORITY requires a signal, so everything
   clean lands at WATCH, which is correct
2. **Too many must-haves.** Twelve requirements means nothing survives. Three to
   five
3. **The size box is above the market.** The map will have told you this
4. **Sourcing is aimed at the wrong population.** Over 70% PASS means fixing
   sourcing, not the rubric

### The ranking gave me far too many PRIORITY rows

Above 25% of researched rows means the rubric is flattering you or the signals
are being read generously. Check that `Not found` ownership rows are capped at
WATCH, and reread the `high` strength signals. A job posting is not a `high`.

### It refuses to write a letter for a row I like

Read the refusal reason. It is one of: nothing specific and true is known, the
only personalization available was something about the owner as a person, the
quoted signal could not be re-confirmed at its URL today, ownership is `Not
found`, the company is on the suppression list, or a retained banker is running a
process. Each refusal says what research would fix it.

### It will not send the emails

Correct, and deliberate. There is no send step in this package. It stages a queue
with dates and you send it, by hand, after reading it. If you want to send from
your own tool, ask for the export — and switch that tool's follow-up automation
off, because the "a reply cancels the sequence" rule lives here and not there.

### My run got interrupted

Type `/originate` again. It reads the state file, recounts from the CSV, and
carries on from the last completed batch. Nothing is researched twice.

### It is slow

A two-thousand-row run with ownership research, signals and drafting is hours of
Claude Code spread over days, not minutes, and roughly sixty percent of it is the
ownership and size pass. It is replacing about a month of associate work that
produces a worse list. Run it in batches and let it report between them.

### Windows path problems

Use `$HOME` in PowerShell, not `~`. Quote any path with a space in it. If a copy
silently does nothing, check you included the `\*` at the end of the source path.

---

# FAQ

### Do I need to pay for anything beyond Claude Code?

No. No database, no API keys, no data subscriptions, no sending tool. If you
already pay for an M&A database you can feed its export in as a cross-find, but
the whole design assumes you do not have one.

### Is "2,000 targets with a single prompt" real?

The enumeration is real and so is the single prompt. What is not real, in any
system, is two thousand *deeply researched* companies in an afternoon. The run
enumerates two thousand, screens them all on free facts, deeply researches the
seven or eight hundred that survive, and ends with twenty or so letters worth
writing. That takes hours of compute spread over days, and the setup guide says
so before you start rather than after.

### Why does it only contact twenty-odd companies?

Because that is what the research is for. Private segments are small towns: the
owners sit on the same association board, use the same bonding agent, and forward
things to each other. A campaign that reads as a mail merge in one inbox reads as
a mail merge in forty. The caps are the most valuable part of the outreach half.

### Why three verdicts instead of a score out of 100?

Because a score invites an argument about whether a 71 beats a 68 and tells
nobody what to do on Monday. PRIORITY, WATCH and PASS each say exactly what
happens next.

### What happens to the 494 WATCH rows?

They are next quarter's pipeline, and they are the cheapest asset the run
produces. Hiring signals expire at 90 days, so a signals re-read on the top of
the WATCH pile refills the top of the funnel for a fraction of what a new
enumeration costs. `pipeline-keeper` tells you when to do it.

### Can it send the emails for me?

No, and it will not be persuaded. See the troubleshooting entry above.

### Is my data safe?

Everything stays in local files on your machine. The `.gitignore` keeps your
workspace out of version control. Personal data is only collected for the rows
you will actually contact, not for all two thousand. Do not put your workspace
folder in a public repository or a shared drive by accident.

### Can I use this outside the US?

Yes, and the UK is in some ways easier: Companies House publishes accounts and
officer histories for free, which means more `verified` revenue figures and more
Tier 1 ownership evidence than any US run will produce. The EU varies sharply by
country. The map step tells you whether ownership and size are publicly
establishable in your geography before the run commits to it.

Note that the email rules follow the **recipient**, not you. CASL and the EU and
UK positions are materially stricter than CAN-SPAM. Read
[`references/compliance.md`](./references/compliance.md), then talk to counsel.

### What if I already have a list?

Skip sourcing. Map your columns to `templates/targets.csv`, then run
`target-analyst` and `fit-ranker` over it. Every address on it gets flagged
`inferred-DO-NOT-USE` until independently verified.

### Can I change the rules?

The mandate is yours — change it freely and the system re-ranks. The files in
`references/` are the rules the skills enforce, and you can edit those too. Be
careful with five of them:

- unknown is not failed
- drops need a fact that is false, not one that is absent
- estimates never exclude on their own
- signals are quoted verbatim
- nothing sends

Each of those protects you from a specific failure that is invisible when it
happens.

### Eleven skills seems like a lot

It is five jobs: find, research, rank, route and write, then keep. The skills are
the seams where a gate belongs, and the gates are the reason you can let a run
touch two thousand companies without wondering what it did.

---

# When you outgrow files

Files are the right answer for one mandate and one run. Signs you have outgrown
them:

- More than one mandate running at once, with overlapping geographies
- More than one person needing the same ranked list
- You want the WATCH rows re-read every quarter automatically, because hiring
  signals expire at 90 days and a six-month-old ranking has a stale timing column
- You want the do-not-contact register enforced across several people's sending
- More than a few thousand live rows

At that point you want a database, a scheduled re-read, and somebody accountable
for the pipeline rather than the list.

---

# What's next

Run it on one segment. Not three. Get the mandate right, write down the number of
conversations you can actually hold, accept the map's verdict even when it is
unhelpful, and read the audit properly — especially the thirty re-checked cheap
drops, because that is where a real target hides.

Then write the twenty letters. That part is still yours, and it should be.

---

Free and MIT licensed. Built by [Corebits](https://corebits.io).
