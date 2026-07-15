# Mneme storage contract for AI news

Mneme is the durable store. Do not add a feed database, JSON archive, vector
store, or separate cache owned by this skill. Follow the installed Mneme
skill when its rules are stricter than this reference.

## Page model

Store durable events as atomic pages and connect them from a digest:

```text
news/
├── events/
│   └── YYYY-MM-DD-short-event-slug.md
└── digests/
    └── <period-key>[-topic].md
sources/
└── papers/
    └── <period-key>/
        └── <versioned-paper-id>.pdf
```

Use a stable, sortable period key. Examples are `2026-07-15` for a calendar
day and `2026-07-13--2026-07-19` for a weekly interval. The configured timezone
defines period boundaries. Do not create a second digest for the same period,
topic, and schedule.

An event page normally uses:

```yaml
---
type: Reference
title: <event title>
description: <one-sentence factual summary>
resource: <canonical primary URL>
tags: [ai-news, <topic tags>]
timestamp: <Mneme page's last meaningful modification time in ISO 8601>
published_at: <source publication time when known>
published_at_raw: <exact publication text shown by the source>
published_precision: <datetime or date>
retrieved_at: <web retrieval time in ISO 8601>
updated_at: <source revision time when explicitly provided>
event_date: <underlying event date when known>
---
```

The fields have distinct meanings:

- `published_at`: when the publisher first released the page;
- `updated_at`: a later publisher revision, only when explicitly identified;
- `event_date`: when the reported event occurred;
- `retrieved_at`: when the agent accessed the page;
- `timestamp`: when the Mneme concept page was last meaningfully modified.

Never derive `published_at` from `retrieved_at`, the local filename, Mneme's
`timestamp`, or the current clock. Keep the exact source text in
`published_at_raw` before normalizing a date or timezone. `published_at`,
`published_at_raw`, `published_precision`, `retrieved_at`, `updated_at`, and
`event_date` are optional OKF extensions. Preserve them and all other unknown
frontmatter keys when editing a page.

Use this body shape when the evidence supports it:

```markdown
# What happened

# Why it matters

# Evidence and caveats

# Citations

1. [Primary source](https://...)
2. [Independent coverage](https://...)
```

The digest uses `type: Summary`, includes `ai-news` and `digest` tags, and
links to event pages with absolute bundle-relative links such as
`/news/events/2026-07-15-example.md`. It summarizes the requested window; it
does not duplicate the full event pages. One configured reporting period has
one digest per topic and schedule. A user-approved refresh edits that page
rather than creating a duplicate. Store no more than the user-confirmed item
count; use 5 to 10 only as an ad hoc default.

## Raw paper PDFs

For every selected paper, save the original public PDF unchanged after the
user approves the Mneme write. Use a versioned identifier in the filename, for
example `2501.12345v2.pdf`, so later revisions do not overwrite earlier bytes.
Store it under `/sources/papers/<period-key>/` and link it from the event page.

Add these optional fields when known:

```yaml
paper_id: <versioned identifier>
paper_pdf: /sources/papers/<period-key>/<versioned-paper-id>.pdf
paper_pdf_url: <canonical public PDF URL>
paper_pdf_sha256: <hash of saved bytes>
```

Verify that the downloaded file is actually a PDF and calculate its SHA-256.
If the destination exists with different bytes, stop and preview a versioned
path; never overwrite a raw source. If there is no lawful public PDF, retain
the paper URL and report the storage gap instead of bypassing access controls.
The PDF is raw evidence, not an agent-readable knowledge page: extract its
important claims, methods, and caveats into the linked event page.

## Deduplication

- Same canonical `resource`: update the existing event page only when the new
  source adds material verified information.
- Same event, several URLs: keep one event page and list useful sources under
  `# Citations`.
- Related but independently meaningful events: keep separate pages and link
  them in prose.
- Uncertain match: preview both choices. Never merge from title similarity,
  search distance, or an embedding threshold alone.

## Pre-write preview

Run Mneme's read-only audit and show:

- resolved bundle path;
- reporting period, timezone, item target, and sources actually read;
- included, excluded, and uncertain events;
- each candidate's quality dimensions and promotional-risk decision;
- verified `published_at`, separate `event_date`, and every canonical URL;
- exact event and digest paths to add or edit;
- raw PDF URL, versioned destination, and paper identifier for each paper;
- proposed frontmatter, tags, canonical URLs, and links;
- planned `index.md` section changes;
- planned newest-first `log.md` entry.

Do not write until the user explicitly approves this concrete scope. A request
to research news is not standing approval for later wiki writes.

## Approved write

After approval, load Mneme's write-side dream workflow and apply only the
approved files. Download approved public paper PDFs unchanged; summarize other
articles rather than copying their full text. Update
`index.md` and prepend a parseable entry such as:

```markdown
## YYYY-MM-DD dream | AI news: <period or topic>
```

Run Mneme lint, rebuild the active disposable index, and rerun the read-only
dream audit. Report validation failures or any scope that still needs judgment.
Never stage, commit, push, archive, merge, or delete automatically.
