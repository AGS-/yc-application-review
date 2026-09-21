# application-samples

Real and synthetic YC applications used to stress-test the `yc-review`
rubric. The companion `bin/run-evals` script runs the skill in `--json`
mode against everything here and writes a summary to `evals/results/`.

## Layout

```
application-samples/
├── README.md
├── synthetic/      # made-up drafts with known expected outcomes
├── accepted/       # publicly-shared applications from companies YC accepted
└── rejected/       # publicly-shared applications from companies YC rejected
```

## Frontmatter schema

Every file starts with a YAML frontmatter block. `bin/yc-review` strips it
before passing the draft to the model, so it doesn't contaminate the
review. `bin/run-evals` parses it to know the truth label.

```yaml
---
company: Dropbox
batch: S07                  # YC batch (S07, W15, W21, …) or "rejected" / "synthetic"
outcome: accepted           # accepted | rejected | synthetic-weak | unknown
source_url: https://…       # where the application text was published
form_version: 2007          # year of the YC form, or "current" if it matches
                            # today's (currently W2027)
verbatim: true              # true if the text is exactly as the founder shared it
partial: false              # true if some answers are missing or truncated
notes: |
  Free-form provenance / caveats. Note when the form was different from
  today's, when answers are redacted, when the founder paraphrased, etc.
---
```

`outcome` values:

- `accepted` — YC funded the company.
- `rejected` — YC declined the application (or it advanced to interview but
  was passed on).
- `synthetic-weak` — synthetic draft built to fail the rubric. Expected
  verdict: ARCHIVE or BORDERLINE.
- `synthetic-strong` — (not yet used) synthetic draft built to pass.
- `unknown` — outcome can't be verified from public sources.

## How `bin/yc-review` handles the frontmatter

The wrapper strips a leading `---` … `---` block before sending the file
to `claude -p`. Decision rationale: the rubric doesn't need to see the
metadata, and stripping in the wrapper means real users can also tag
their own `YC_APPLICATION.md` with frontmatter (e.g. for versioning) and
not pay for those tokens. Files without frontmatter pass through
untouched.

## How to add a new application

1. Find the application text. Verbatim only — do not paraphrase, do not
   summarize, do not fabricate. If you can only find a partial transcript,
   capture what's there and set `partial: true` in the frontmatter with a
   note about what's missing.
2. Pick the right subdirectory: `accepted/`, `rejected/`, or `synthetic/`.
3. Save as `<slug>.md` where the slug is lowercase, hyphenated, and
   typically `<company>-<batch>` (e.g. `dropbox-s07`, `buffer-2011`).
4. Write the frontmatter block. Be honest about `verbatim`, `partial`,
   and `form_version`. The eval is only useful if these are accurate.
5. Format the body to match the current YC question structure where
   possible (`## Founders`, `## Founder Video`, `## Company`,
   `## Progress`, `## Idea`, `## Equity`, `## Curious`,
   `## Batch Preference`). If the original used different headings — common
   for pre-2015 applications — preserve the original structure and explain
   in `notes:`.

## What's currently here

| File | Outcome | Batch | Source |
|------|---------|-------|--------|
| `synthetic/flowsync-weak.md` | synthetic-weak | — | (made up) |
| `accepted/dropbox-s07.md` | accepted | S07 | ycombinator.com/apply/dropbox |
| `accepted/lago-w21.md` | accepted | W21 | getlago.com/blog/how-we-got-into-yc |
| `accepted/bedrock-s13.md` | accepted | S13 | blog.zactownsend.com/our-yc-s13-application |
| `accepted/gitlab-w15.md` | accepted | W15 | about.gitlab.com/blog/gitlabs-application-for-y-combinator-winter-2015 |
| `rejected/buffer-2011.md` | rejected | (S11) | buffer.com/resources/buffers-y-combinator-application |

## A note on form versions

The YC application form has changed substantively over time. Before ~2015
it was much shorter, didn't ask "Are people using your product?" as a
distinct question, and didn't require a 50-character description. The
current rubric in `SKILL.md` is calibrated for the **W2027** form, which
dropped "Anything else you would like us to know," "Tell us something
surprising or amusing," and the category dropdown, and added questions
about who writes the code, AI models and AI coding tools, prior
accelerators, and the Equity block. Treat verdicts on older applications
as approximations: a 2007 application with no demand-evidence answer is
missing data, not failing the rubric.
