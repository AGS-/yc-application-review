# evals

A small eval suite that runs the `yc-review` rubric against a corpus of
publicly-shared YC applications (accepted + rejected) and one synthetic
draft built to fail the rubric. The point is to **stress-test the rubric**,
not to declare it correct.

## What this is

For each application in `application-samples/{accepted,rejected,synthetic}/`,
`bin/run-evals` calls `bin/yc-review --json <file>` and saves the JSON
output. After every app finishes, it writes a `summary.md` table comparing
the rubric's verdict to the known truth label and prints aggregate stats.

## What this is NOT

- **Not a predictor of YC acceptance.** YC's selection function has too
  much noise. A "rejected" app can be technically excellent (Buffer kept
  growing without YC) and an "accepted" app can be sloppy on paper but
  win on team or timing.
- **Not a benchmark you should optimize against.** The corpus is small
  (single digits) and unbalanced, and the form changed substantively
  between batches. Tuning the rubric to maximize the match rate against
  this set would overfit.
- **Not a comparison across rubric revisions.** The skill calls a
  non-deterministic LLM. Two runs of the same app on the same rubric will
  not always produce identical JSON. Treat any single-run result as
  noisy.

## What it IS

A directional sanity check. If the rubric were upside-down — if it
verdicted accepted apps ARCHIVE and rejected apps INTERVIEW — that would
be a strong signal something is wrong with the rubric. If most accepted
apps come back INTERVIEW or BORDERLINE and most rejected ones come back
ARCHIVE or BORDERLINE, the rubric is at least pointing the right way.

## Caveats

- **Form drift.** Pre-2015 YC applications are missing several questions
  the current rubric scores against — most importantly "Are people using
  your product? How many?" Verdicts on old applications should be read
  as approximations. Each application's frontmatter records the
  `form_version` it was written against.
- **Truncated text.** A few sources only published partial answers (e.g.
  ycombinator.com/apply/dropbox displays the application in a structured
  form that abbreviates some fields). Where this is true, `partial: true`
  is set in the frontmatter.
- **Selection bias.** Founders publish their successful applications more
  often than their rejected ones. The rejected set is small and skewed
  toward founders confident enough to publish.
- **Tarpit-list staleness.** YC's published tarpit list evolves. The
  rubric in `SKILL.md` is calibrated against the current public list as
  of the most recent skill update.

## How to run

```bash
# Run against everything in application-samples/
bin/run-evals

# Run against a subset by slug (filename without .md)
bin/run-evals --apps dropbox-s07,buffer-2011

# One app at a time during iteration
bin/run-evals --apps flowsync-weak
```

Each `claude -p` call costs a few cents; a 6-app run is well under a
dollar. **Do not** wire this up to fan out to hundreds of apps without
explicit approval.

## How to read a run

After a run, `evals/results/<UTC-timestamp>/` contains:

- `<subdir>/<slug>.json` — raw skill output (parseable JSON object).
- `<subdir>/<slug>.error.txt` — present only if the run failed for that
  app. Contains stderr from `claude -p` and any stdout that didn't parse
  as JSON.
- `summary.md` — table of (truth label, verdict, match?, tarpit_flag) plus
  aggregate stats.

The `Match?` column uses these rules:

| Truth label | Match if verdict is |
|-------------|---------------------|
| `accepted` | `INTERVIEW` or `BORDERLINE` |
| `rejected` | `ARCHIVE` or `BORDERLINE` |
| `synthetic-weak` | `ARCHIVE` or `BORDERLINE` |
| anything else | n/a (`—`) |

## How to add an application

See `application-samples/README.md`. Briefly: drop the file in the right
subdirectory with frontmatter, and the next `bin/run-evals` will pick it
up automatically.

## Where to look when results are surprising

- **Accepted came back ARCHIVE.** Read the application. Is the rubric
  right that the application was weak (and YC accepted them despite the
  weak application — possible) or is the rubric over-penalizing
  something the partners didn't care about (e.g. the 2007 Dropbox form
  has no "Are people using your product?" answer)?
- **Rejected came back INTERVIEW.** Was the application actually strong
  on paper but YC passed for non-paper reasons (team, market timing,
  competing batch applicants)? Or is the rubric missing a category that
  partners weight heavily?
- **Synthetic-weak came back INTERVIEW.** That's a real rubric failure.
  The synthetic was built to trip every anti-pattern in `SKILL.md`; if
  the model misses them, the rubric isn't strict enough or isn't
  surfacing them.

## Repo layout

```
evals/
├── README.md       # this file
└── results/        # gitignored — one subdir per timestamped run
    └── <UTC-ts>/
        ├── synthetic/<slug>.json
        ├── accepted/<slug>.json
        ├── rejected/<slug>.json
        └── summary.md
```
