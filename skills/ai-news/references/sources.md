# Public AI news sources

Use this as a routing map, not a mandatory crawl list. Recheck availability at
runtime because login walls and site structures change. A page being public
does not make its claims independent or correct.

## Source priority

1. Primary evidence: official announcements, papers, repositories, regulatory
   documents, filings, and benchmark artifacts.
2. Independent reporting: publications that add interviews, verification, or
   material context.
3. Commentary and Chinese-language synthesis: useful for discovery and
   interpretation, but trace important claims back to primary evidence.

## Official labs and vendors

- OpenAI News: <https://openai.com/news/>
- Anthropic News: <https://www.anthropic.com/news>
- Google DeepMind Blog: <https://deepmind.google/discover/blog/>
- Google AI: <https://blog.google/technology/ai/>
- Meta AI Blog: <https://ai.meta.com/blog/>
- Mistral News: <https://mistral.ai/news/>
- Microsoft Research Blog: <https://www.microsoft.com/en-us/research/blog/>
- Hugging Face Blog: <https://huggingface.co/blog>

Use official pages for release facts. Treat performance, safety, adoption, and
competitive claims as vendor claims unless independently supported.

## Research and evaluation

- arXiv Artificial Intelligence: <https://arxiv.org/list/cs.AI/new>
- arXiv Computation and Language: <https://arxiv.org/list/cs.CL/new>
- arXiv Machine Learning: <https://arxiv.org/list/cs.LG/new>
- Hugging Face Daily Papers: <https://huggingface.co/papers>
- Papers with Code: <https://paperswithcode.com/>
- Stanford HAI News: <https://hai.stanford.edu/news>
- Epoch AI: <https://epoch.ai/>

An arXiv paper is a public preprint, not proof that its claims survived peer
review or independent reproduction. Check code, data, evaluation design, and
later revisions when those details matter. Resolve the exact versioned paper
identifier and public PDF URL for every paper selected for storage.

## Open source and engineering

- GitHub Trending: <https://github.com/trending>
- Hugging Face Models: <https://huggingface.co/models>
- Simon Willison's Weblog: <https://simonwillison.net/>
- GitHub release pages for the relevant project

Use repository releases and commits for exact implementation changes. Stars,
likes, downloads, and trending position are popularity signals, not quality
evidence.

## Independent industry coverage

- Ars Technica AI: <https://arstechnica.com/ai/>
- TechCrunch AI: <https://techcrunch.com/category/artificial-intelligence/>
- The Decoder: <https://the-decoder.com/>
- The Verge AI: <https://www.theverge.com/ai-artificial-intelligence>

Use these to discover events and obtain independent context. Trace technical
specifications, legal documents, funding figures, and direct quotations to the
underlying source whenever possible.

## Chinese-language coverage

- 量子位: <https://www.qbitai.com/>
- 机器之心: <https://www.jiqizhixin.com/>
- InfoQ AI: <https://www.infoq.cn/topic/AI>

Use these for Chinese summaries and domestic industry coverage. Exclude paid
or member-only articles when the task requires login-free reading, and follow
important translated claims back to the original source.

## Policy and governance

- NIST AI: <https://www.nist.gov/artificial-intelligence>
- European AI Office: <https://digital-strategy.ec.europa.eu/en/policies/ai-office>
- OECD AI: <https://oecd.ai/>

Prefer the enacted text, official notice, court filing, or regulator statement
over commentary about it. State whether a measure is proposed, adopted, in
force, delayed, or under challenge.

## Discovery-only sources

Social networks, newsletters, aggregators, search snippets, and sites with
unstable paywalls may reveal a lead. Do not cite them as the sole evidence when
the underlying public page can be found. Never bypass a login or paywall.

## Timestamp verification

Prefer a visible byline timestamp corroborated by structured page metadata
when available. Preserve the source's timezone offset. If the page supplies
only a date, store date precision rather than inventing a time. Record an
`updated_at` value separately when the publisher distinguishes it from the
original publication. If no publication date can be verified, mark it unknown
and normally exclude it from a period roundup.
