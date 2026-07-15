---
name: ai-news
version: 0.2.0
description: Find, verify, summarize, and curate current AI news from public web pages, then prepare approved results for storage in a Mneme OKF wiki. Use for requests such as "查今天的 AI 新闻", "最近一周大模型有什么更新", "整理某个 AI 主题的新闻", "核实一条 AI 新闻", or "把这批 AI 新闻存进 Mneme". Prefer login-free primary sources, deduplicate by event, and preserve Mneme's preview-before-write contract.
---

# AI News

Run a focused news-research agent workflow. Use the host's available web
search and browser tools; do not create a subscription, daemon, or separate
news database. Treat Mneme Markdown as the only durable store. Design each
scheduled workflow as one idempotent run per configured reporting period.
Never install or change a schedule unless the user explicitly requests it.

## Resolve the request

Determine the topic, time range, language, and desired depth from the request.
Use the user's local timezone. When the user says only "today" or "recent",
search the previous 24 hours. When no topic is given, cover general AI.

Default to the full workflow: research, report, and prepare a Mneme write
preview. For an ad hoc request with no count, suggest or use 5 to 10 selected
items. Never pad the result to reach a target. If the user explicitly asks for
read-only research, stop after the report.

For a scheduled run, derive a stable period key from the configured interval
and timezone. Before searching, check for that period's digest in the resolved
Mneme bundle. If it already exists, return it and do not duplicate the run.
Refresh only when explicitly requested, and preview an edit to the existing
period digest.

## Configure a schedule

When the user asks to create or change a scheduled task, align with them before
creating it. At minimum confirm:

- reporting period or cadence, including exact run time and timezone;
- number of selected items per period;
- coverage window, normally the interval since the previous scheduled run.

Also resolve the topic scope and Mneme bundle when they are not already clear.
Do not silently convert a weekly request into daily runs or assume 5 to 10
items for an automation. After agreement, use the host's supported scheduling
mechanism. Put the confirmed cadence, count, timezone, coverage window, topic,
and bundle path into the scheduled prompt so later runs remain deterministic.

## Research

Read `references/sources.md` before a general roundup or whenever source
selection is unclear.

1. Search primary sources first, then use independent coverage to add context.
2. For a general roundup, inspect several relevant source groups rather than
   relying on one publisher or one search query.
3. Open the actual page. Never treat a search-result snippet, social post, or
   generated aggregator summary as evidence.
4. Verify and retain the canonical URL, named organization or authors, exact
   source publication time, and the specific claim being reported. Publication
   time is not retrieval time, storage time, or event time.
5. Prefer pages readable without login. If the original is blocked, locate a
   public primary document or omit the item; do not bypass access controls.
6. Distinguish publication date from the date the underlying event occurred.
7. For consequential or disputed claims, require a primary source plus an
   independent source. Label single-source claims and uncertainty explicitly.
8. When an included item is a paper, locate its public canonical PDF and note
   the exact paper identifier and version. Do not substitute an abstract page,
   HTML rendering, or generated summary for the raw PDF.

## Select and deduplicate

Cluster URLs by real-world event, not by headline. One model release covered
by ten sites is one item. Prefer the canonical announcement as the main URL and
retain secondary URLs only when they add independent reporting or analysis.

Rank items by:

1. Confirmed technical or product change.
2. Material impact on users, developers, research, policy, or the market.
3. Novelty within the requested time window.
4. Quality and independence of evidence.

Score every serious candidate using `references/quality-rubric.md`. Use the
score to support editorial judgment, not to automate truth. Reject disclosed
sponsorship, affiliate copy, content-farm rewrites, and promotional pieces with
no independently useful facts. A vendor announcement may remain only when the
release itself is material and supported by concrete artifacts such as docs, a
model card, a paper, a repository, or independently checkable changes; label it
as vendor-sourced.

Exclude rumor-only items, recycled announcements, SEO summaries, unverifiable
benchmark claims, and articles whose only accessible content is a headline.
For scheduled work, select no more than the confirmed per-period count. For ad
hoc work, use the requested count or the 5-to-10 default. If fewer candidates
pass the bar, report fewer and explain the coverage gap instead of adding
filler.

## Report

Group the answer by event category, not publisher. For each included item give:

- source publication time, event date when different, and concise title;
- what happened, separated from commentary;
- why it matters;
- quality score and promotional-risk label;
- confidence: `confirmed`, `single-source`, or `developing`;
- primary and useful independent links.

End with the reporting period, source groups checked, and important coverage gaps.
Keep facts attributable to the linked pages. Do not imply that vendor claims
are independently verified.

## Deliver output via templates

Users most often run this skill on a schedule. After the report is ready,
deliver it as a file the user can read or forward, using the templates in
`templates/`. This is independent of Mneme storage: deliver the digest even
when the user has not yet approved a wiki write, and never block delivery on
bundle approval.

Read both templates before filling. They are plain-text templates with
`{{variable}}` placeholders and a `{{#items}} ... {{/items}}` loop repeated
once per included news item. Fill every placeholder from the verified report
data only; write `未知` (unknown) for any field that cannot be confirmed
rather than fabricating a value. Escape HTML special characters in the HTML
template. Do not alter template structure or styling.

- `templates/digest.md.template` — Markdown message suited to an IM or channel
  push. Save as `digest-<period-key>.md` and send it to the user, or paste the
  rendered content directly into a channel message.
- `templates/digest.html.template` — a styled visual report. Save as
  `digest-<period-key>.html` and send the file; the user can open it in a
  browser or print it to PDF.

Required placeholders for both templates: `period_label`, `report_date`,
`topic`, `item_count`, `timezone`, and the `items` loop. Each item carries
`index`, `title`, `category`, `confidence` (with a human-readable
`confidence_label`), `quality_score`, `published_at`, `summary`,
`why_it_matters`, `primary_url` (and `primary_url_host` for the HTML link
text), plus optional `event_date` and `secondary_url`. End with
`source_groups` and `coverage_gaps`.

Use the stable period key as the filename suffix so a later refresh of the
same period overwrites the same file instead of producing duplicates. For a
scheduled run, deliver the filled Markdown digest as the default channel
message and offer the HTML report when the user wants a visual copy or a
printable archive.

## Prepare Mneme storage

Read `references/mneme-storage.md`. For any paper, also read its raw-PDF rules.
Locate and use the installed `mneme` skill;
do not copy or reimplement Mneme. Resolve its bundle using Mneme's own rules.

Before any wiki write:

1. Read the bundle `index.md` and search for matching canonical URLs, titles,
   and events.
2. Run Mneme's read-only dream audit.
3. Prepare a concrete change preview covering new or edited event pages, the
   digest page, tags and links, plus `index.md` and `log.md` updates.
4. Show the news report, audit result, and complete change preview.
5. Require explicit user approval for every bundle write.

After approval, follow the installed Mneme skill's dream workflow exactly.
Load its mandatory write-side reference before editing. Apply only the approved
scope, then lint and reindex through Mneme. Never automatically stage, commit,
push, merge, archive, delete, or overwrite knowledge.

## Safety and fidelity

- Preserve titles, dates, URLs, names, and quantitative claims accurately.
- Summarize copyrighted pages; do not mirror full articles into the wiki.
- Keep opinion and prediction visibly separate from reported facts.
- Do not fabricate access, citations, publication dates, or corroboration.
- If current web access is unavailable, say so and do not substitute stale
  model knowledge for a current-news result.
