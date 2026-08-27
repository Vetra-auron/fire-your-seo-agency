# 🔥 fire-your-seo-agency — Evidence-first v1.2

[한국어](./README.ko.md) · **English**

> A Claude Code skill for SEO and AI-search visibility that separates **official guidance, observed behavior, and experimental hypotheses**.

This fork builds on `leopard627/fire-your-seo-agency`. v1.2 adds an operational contract for a repeatable Search Visibility Agent.
It keeps the original audit → implement → measure workflow and its Korea/Naver focus,
while replacing overly rigid SEO/GEO claims with an evidence-first operating model.

## What changed

1. Every recommendation is labeled **[OFFICIAL] / [OBSERVED] / [EXPERIMENTAL]**
2. Search crawlers and model-development crawlers are treated separately
3. `llms.txt` is optional/experimental, not a required Google AI-search signal
4. "one question = one page" and fixed answer-length rules are heuristics, not requirements
5. fixed title/meta-description character counts are treated as heuristics
6. FAQ structured data is not treated as a direct AI-citation lever
7. official Naver guidance is separated from AI Briefing observations
8. 14 days is a measurement checkpoint, not a guaranteed response window
9. technical implementation and business/search outcomes are reported separately
10. reports include uncertainty, rollback, and follow-up measurement

## Five lanes

| Lane | Target | Core question |
|---|---|---|
| SEO | traditional search | Can systems discover, crawl, index and understand the site? |
| AEO | answer-style search | Does the page provide useful, verifiable answers? |
| GEO | ChatGPT/Perplexity/Claude search | Can search crawlers access and discover the site as a source? |
| LLMO | brand/entity consistency | Are public brand facts consistent and accurate? |
| NEO | Naver Search / AI Briefing | Are official Naver basics and experimental AI-source tactics managed separately? |

## Install

Current main fork:

```bash
git clone https://github.com/Vetra-auron/fire-your-seo-agency.git .claude/skills/fire-your-seo-agency
```

Evidence-first development branch:

```bash
git clone -b evidence-first-v1.1 https://github.com/Vetra-auron/fire-your-seo-agency.git .claude/skills/fire-your-seo-agency
```

Then:

```text
/fire-your-seo-agency audit my site
```

## v1.2 operational layer

- audit / plan / fix / verify / measure / full modes
- 0–100 readiness score + confidence + BLOCKED/AT_RISK/READY/UNKNOWN state
- P0–P3 prioritization
- JSON Schema for machine-readable results
- persistent baseline/follow-up measurement convention
- 12 behavioral regression scenarios

## Structure

```text
SKILL.md
references/
  evidence-policy.md
  crawlers.md
  seo.md
  aeo.md
  geo.md
  llmo.md
  neo-naver.md
  measure.md
  scoring.md
  execution.md
  output-contract.md
schemas/
  audit-result.schema.json
examples/
  audit-result.example.json
tests/
  scenarios.md
```

## Operating principles

- people-first content
- current platform documentation before folklore
- original data and non-commodity value
- no ranking/traffic/citation guarantees
- technical change ≠ proven outcome
- explicit uncertainty and rollback
- measurement before success claims

## Evidence date

Primary policy references checked: **2026-08-27**.

See `references/evidence-policy.md` for source links.

## Original & license

Original project: https://github.com/leopard627/fire-your-seo-agency

MIT License. Preserve the original copyright and license notice.
