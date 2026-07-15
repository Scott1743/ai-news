# AI news quality rubric

Score candidates only after opening and verifying their sources. Keep the
dimension scores in the research notes and show them in the Mneme preview.

## Positive dimensions

Score each dimension from 0 to 3:

| Dimension | 0 | 1 | 2 | 3 |
|---|---|---|---|---|
| Evidence | No accessible evidence | One vague secondary source | Clear primary artifact or solid reporting | Primary artifact plus independent verification |
| Substance | Slogan or opinion only | A few concrete facts | Useful technical, policy, or business detail | Methods, data, documents, code, or reproducible detail |
| Impact | No clear consequence | Narrow or speculative | Material to a defined audience | Broad or strategically important consequence |
| Novelty | Recycled or outside window | Minor update | Meaningful new development | First release, major result, or major policy action |

Score independent corroboration from 0 to 2:

- `0`: issuer or author only;
- `1`: credible secondary context, but no independent confirmation;
- `2`: meaningful independent confirmation or reproducible artifact.

## Promotional-risk penalty

Score from 0 to 3 and subtract it from the positive total:

- `0`: no meaningful promotional signal;
- `1`: vendor-sourced but fact-rich and directly relevant;
- `2`: marketing-heavy, selective evidence, or weakly disclosed commercial
  interest;
- `3`: sponsored or affiliate content, native advertising, lead generation,
  content-farm rewrite, or unsupported superlatives.

`quality_score = evidence + substance + impact + novelty + corroboration - promotional_risk`

The maximum is 14. Normally include candidates scoring at least 8 with
promotional risk no higher than 1. A score never overrides a hard exclusion or
turns a claim into fact.

## Hard exclusions

Exclude an item even if its arithmetic score appears high when:

- its publication date cannot be distinguished from the current retrieval
  date and recency is essential to the request;
- the only evidence is a search snippet, social post, anonymous repost, or
  inaccessible headline;
- it is disclosed sponsorship, affiliate copy, or native advertising;
- it repeats an old release as new;
- it presents benchmarks without enough context to identify the task, baseline,
  data, or evaluator;
- it makes a consequential accusation with no primary evidence or credible
  independent reporting.

## Editorial balance

Do not reserve slots by category. Select the strongest items up to the count
confirmed for the reporting period; use 5 to 10 only as an ad hoc default.
Vendor releases, funding announcements, and product demos
can be news, but they must clear the same evidence and substance bar. Explicitly
label issuer claims, developing stories, preprints, and non-peer-reviewed work.
