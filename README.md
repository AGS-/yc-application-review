# yc-review

A Claude Code skill that critiques your Y Combinator application like a YC partner would. Terse, blunt, no participation trophies. Tells you whether the draft gets you an interview or gets archived, and the three things to fix.

> *"Praise is reserved for genuinely strong answers. If a section is fine, say 'fine, move on.'"* — from the skill

## What it does

You write a draft of your YC application in `YC_APPLICATION.md`. You run `/yc-review`. The skill:

1. Reads the draft.
2. Picks a posture — Dalton Caldwell, Garry Tan, or Michael Seibel — and stays in character.
3. Runs your draft through a rubric grounded in YC partner talks and the questions partners actually ask.
4. Returns a verdict (`INTERVIEW` / `BORDERLINE` / `ARCHIVE`), the top 3 fixes, and the single hardest question your draft hasn't answered.

Two modes:

- **Partner mode (default)** — under-500-word triage, the kind of notes a YC partner actually writes.
- **Coach mode** — section-by-section, scored 0–10, with rewrites for any answer below 7.

## Install

Requires [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

```bash
git clone https://github.com/YOUR_USERNAME/yc-application-review.git ~/.claude/skills/yc-review
```

Restart Claude Code. The skill is now available as `/yc-review` in any project.

## Use

From any project (or any directory):

```bash
# Option 1: drop a blank template
/yc-review
# → choose option (c). Skill writes YC_APPLICATION.md into your CWD.
# Fill it out. Re-run.

# Option 2: walk through the questions one at a time
/yc-review
# → choose option (b). Skill interviews you and writes the file as you go.

# Option 3: paste your existing draft into YC_APPLICATION.md, then run
/yc-review
```

The skill defaults to partner mode. To get section-by-section rewrites:

```
/yc-review coach
```

For an iterative improvement workflow:

```
/yc-review loop
```

Loop mode runs partner-mode review → asks targeted clarifying questions → rewrites `YC_APPLICATION.md` from your answers → re-runs the review. Repeats until the verdict hits `INTERVIEW` or three rounds, whichever comes first. Interactive only — won't work via the headless wrapper.

## Headless mode (`bin/yc-review`)

For one-shot reviews from a script or pipeline, use the bash wrapper. It works directly from this repo with no install step — it inlines `SKILL.md` via `claude --append-system-prompt`.

```bash
# Prose review (partner mode):
./bin/yc-review path/to/draft.md

# Coach mode (section-by-section, scored, with rewrites):
./bin/yc-review --coach path/to/draft.md

# JSON output (parseable, no prose, no markdown fence):
./bin/yc-review --json path/to/draft.md | jq .
```

Try it against the bundled synthetic sample (a deliberately weak draft used to smoke-test the rubric):

```bash
./bin/yc-review application-samples/synthetic/flowsync-weak.md
./bin/yc-review --json application-samples/synthetic/flowsync-weak.md | jq .
```

The `--json` flag returns a fixed shape (`verdict`, `verdict_reason`, `what_works`, `what_doesnt[]`, `top_3_fixes`, `the_one_question`, `tarpit_flag`) — useful for building eval suites against published YC applications.

Requirements: bash and `claude` on `PATH`. No Node, Python, or other runtimes.

## What you get

```
## YC Application Review — Hi Finance

Verdict: BORDERLINE — strong founder-market fit, but no evidence
of real demand. This reads like a deck, not a usage report.

### What's working
- Founder background is concrete and relevant.
- "Why now" answer ties to a specific regulatory change.

### What's not
- "Describe in detail" — *"democratizing access to financial tools"*
  is a tagline, not a description. Specificity / clarity.
- "Are people using your product?" — "We have a waitlist of 500"
  is interest, not demand. Demand evidence.
- "Competitors" — "We have no direct competitors" is almost
  always false. Market awareness.

### Top 3 fixes
1. Replace the waitlist number with named active users + what
   they did this week without the product.
2. Name 3-5 real competitors. State one specific thing they're
   wrong about.
3. Rewrite the detail paragraph to lead with what is shipped
   today, not the vision.

### The one question
Who is the *single named user* who would be most upset if you
shut this down tomorrow? What did they do yesterday with it?
```

## Why this exists

I was about to apply to YC for [Hi Finance](https://example.com) and looked for an existing tool. Closest I found was a [one-day NextJS chatbot](https://judy-webdecoded.medium.com/how-i-built-an-ai-app-to-review-yc-applications-in-a-day-92e2921a6f6b) and [jona/ycombinator-skills](https://github.com/jona/ycombinator-skills), which has 19 YC-flavored framework skills but no application reviewer.

This skill is grounded in:

- **Dalton Caldwell** — *How to Apply and Succeed at Y Combinator* ([YC Library](https://www.ycombinator.com/library/6t-how-to-apply-and-succeed-at-y-combinator))
- **Garry Tan** — *Three tips for applying to YC* ([YC Library](https://www.ycombinator.com/library/J7-garry-tan-s-tips-for-applying-to-yc))
- **andiai.com** — [*What YC Partners Actually Ask*](https://andiai.com/blogs/essay-yc-application-advice-office-hours-actually-20260319-1131)
- The current YC application form ([apply.ycombinator.com](https://apply.ycombinator.com))
- YC's published tarpit list and partner posts on rejection patterns

It does not predict whether you'll get in. YC selection has too much noise.

## What it does not do

- It does not write your application from scratch. It improves a draft.
- It does not replace talking to real YC alumni or doing user research. Both matter more.
- It does not flatter.

## Files

```
yc-application-review/
├── SKILL.md                  # the skill itself (the prompt)
├── README.md                 # this file
├── LICENSE                   # MIT
├── bin/
│   └── yc-review             # headless bash wrapper (claude -p)
├── templates/
│   └── YC_APPLICATION.md     # blank template with the current YC questions
├── application-samples/      # sample drafts for testing / evals
│   ├── README.md             # what's in here, how to add more, methodology
│   ├── synthetic/            # synthetic drafts (expected outcomes)
│   ├── accepted/             # publicly-shared YC-accepted applications
│   └── rejected/             # publicly-shared YC-rejected applications
└── evals/                    # rubric eval suite
    └── README.md             # methodology, how to run, how to interpret
```

## Eval suite

`bin/run-evals` runs `bin/yc-review --json` against every application in
`application-samples/{accepted,rejected,synthetic}/` and writes results to
a timestamped directory under `evals/results/`. See `evals/README.md` for
methodology and how to interpret a run.

```bash
# Run against everything
./bin/run-evals

# Run against one or more specific apps
./bin/run-evals --apps dropbox-s07,buffer-2011
```

## Contributing

The rubric is opinionated. If you've been a YC partner, alum, or have read enough applications to have informed opinions on what's wrong here — open an issue or PR. Particularly useful:

- Updates when the YC application form changes between batches
- New tarpits worth flagging
- Better forcing questions for sections where the current rubric is weak

## License

MIT. Use it, fork it, ship it.
