<div align="center">

#  AI News Radar

**A fact-checking, Mneme-archiving AI news research Agent Skill**

*Today's AI milestones, archived into your knowledge base by tonight.*

[![MIT License](https://img.shields.io/badge/license-MIT-purple.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-0.2.0-pink.svg)](CHANGELOG.md)
[![Skills.sh](https://img.shields.io/badge/skills.sh-available-blue.svg)](https://www.skills.sh/?q=ai-news)

</div>

English | [简体中文](README.md) | [📖 Intro](https://scott1743.github.io/ai-news/)

---

## ✨ Why AI News Radar?

The AI world is drowning in daily noise — clickbait, SEO rewrites, and vendor
press releases all blended together. You don't just need to "see the news";
you need a pipeline that opens the original page, verifies the source, scores
and filters, deduplicates, and archives what actually matters.

**AI News Radar** is not an aggregator. It is a rigorous researcher:

- It never treats a search snippet as evidence
- It never treats a vendor announcement as independent reporting
- It uses a traceable method to settle the AI events that matter into your
  knowledge base

---

## 📡 Core features

### Primary-source verification
Opens first-hand sources first — official announcements, paper PDFs, code
repositories, regulatory filings. Never treats a search-result snippet, social
post, or aggregator summary as evidence.

### Quality scoring
Every candidate is scored on evidence, substance, impact, novelty, and
independent corroboration, then penalized for promotional risk. Sponsorship,
content-farm rewrites, and accusations without primary evidence are hard
excluded.

### Event deduplication
Clusters by real-world event, not by headline. One model release covered by
ten outlets counts as one item; the canonical announcement is the main link
and useful independent reporting goes under citations.

### Mneme archival
Mneme OKF Markdown is the only durable store. Event pages, digest pages, and
raw paper PDFs each have their role, keyed by a stable reporting period. No
second digest is created for the same period.

### Scheduled-task delivery templates
Most users run this skill on a schedule. After the research completes, the
agent fills the Markdown message template and HTML report template under
`templates/` and sends the files to the user — the digest can be pushed
straight to a channel or read in a browser or printed. Delivery is decoupled
from Mneme writes, so the digest arrives without waiting for archive approval.

### Preview before write
Every knowledge-base write must pass a read-only audit and show a complete
change preview — paths, frontmatter, tags, links, log entry — before anything
is written. Only an explicit approval lands the change.

### Safety boundaries
Never bypasses login or paywalls; distinguishes publication time from event
time; keeps opinion and prediction visibly separate from fact; unverifiable
dates are marked unknown and usually excluded.

---

## 📦 Quick start

### Option A: install via skills.sh (recommended)
```bash
npx skills add Scott1743/ai-news/skills/ai-news
```

### Option B: manual install

1. Download the latest release: [ai-news-0.2.0.zip](https://github.com/Scott1743/ai-news/releases/download/v0.2.0/ai-news-0.2.0.zip)
2. Extract it into your Agent skills directory
3. Restart your Agent client to load the skill

---

## 🌱 Usage examples

```
Find today's AI news
```
> Defaults to the previous 24 hours, grouped by event category, 5–10 selected
> items.

```
What major model updates happened this week
```
> Custom time window and topic, with quality scores attached to each item.

```
Store this batch of AI news into Mneme
```
> Shows a complete change preview first; after approval, writes event pages
> and the digest via the Mneme dream workflow.

```
Compile AI news every morning at nine
```
> After confirmation, registers a scheduled task with a deterministic period,
> timezone, item count, and coverage window.

---

## 📝 Version history

The first public release, 0.1.0, establishes the five-stage workflow
(resolve request, research, select and deduplicate, report, Mneme storage)
and the "preview before write" contract. The 0.2.0 release adds scheduled-task
delivery templates: after the research completes, the agent fills the Markdown
message template and HTML report template under `templates/` and sends the
files to the user, so each daily digest can be pushed straight to a channel or
read in a browser. It depends on the installed
[Mneme](https://github.com/Scott1743/mneme) skill for the knowledge base and
read-only audit; this skill never copies or reimplements Mneme, but
collaborates through its public dream workflow.

---

## 📚 Project archive

```
ai-news/
└── skills/
    └── ai-news/
        ├── SKILL.md              # Agent Skill entry and workflow definition
        ├── agents/
        │   └── openai.yaml       # OpenAI-compatible Agent interface config
        ├── templates/            # Scheduled-task delivery templates
        │   ├── digest.md.template   # Channel-push Markdown message template
        │   └── digest.html.template # Visual HTML report template
        └── references/
            ├── sources.md        # Public source routing map
            ├── quality-rubric.md # Quality scoring rubric
            └── mneme-storage.md  # Mneme storage contract
```

---

## 📖 Further reading

- [SKILL workflow definition](skills/ai-news/SKILL.md)
- [Public source routing map](skills/ai-news/references/sources.md)
- [Quality scoring rubric](skills/ai-news/references/quality-rubric.md)
- [Mneme storage contract](skills/ai-news/references/mneme-storage.md)
- [Changelog](CHANGELOG.md)

---

## 📜 Design principles

- **Primary evidence first**: official announcements, papers, code, and
  regulatory filings take precedence over secondary reporting.
- **Traceable**: preserve canonical URLs, named authors, exact publication
  times, and the raw source time text.
- **No auto-write**: a research request is not standing approval for knowledge
  writes; preview and approve every time.
- **No access-control bypass**: login walls and paywalls are never bypassed; if
  no public primary source exists, the item is omitted.
- **No fabrication**: unverifiable dates, citations, and corroboration are
  marked unknown; stale model memory never substitutes for current news.

---

## 📜 License

This project is open-sourced under the [MIT License](LICENSE).

<div align="center">

*May every important AI story of your day be properly verified and archived.*

</div>
